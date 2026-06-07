# Playwright E2E 测试诊断指南

技术选型：**Playwright** 是固定的 e2e 测试框架，不要引入其他替代方案。

## 为什么 E2E 诊断成本高昂

历史分析 AI 辅助的 e2e 会话表明存在三个主要的时间消耗点：

| 模式                                                          | 根本原因             |
| ------------------------------------------------------------- | -------------------- |
| **盲目重试** — 在未调查原因的情况下重新运行相同的失败测试     | Agent 将重试当作调查 |
| **超时循环** — 45s 超时 → 重试 → 再次超时                     | 异步渲染竞争，未检查 |
| **针对部分变更运行完整套件** — 修复一个小部件后就运行全部测试 | 没有针对性的验证策略 |

**关键原则**：_先检查，再重试。_ 一个两分钟的诊断脚本可以节省 30 分钟的盲目重跑。

---

## 诊断决策树

当测试失败时，按以下顺序执行：

```
1. Is the dev server alive?
   ├── NO → Start it. Check port conflicts. Re-run once.
   └── YES → continue

2. Is the target element in the DOM at all?
   ├── NO → Component not rendering
   │   ├── Check browser console for errors
   │   ├── Check component registration / import
   │   └── Check routing: does the URL resolve to the expected page?
   └── YES → Element exists but wrong state
       ├── Check getComputedStyle for display:none / visibility:hidden
       ├── Check if async data has loaded (network tab / waitForResponse)
       └── Check if CSS classes are generated (Tailwind / build pipeline)

3. Is the failure consistent or flaky?
   ├── Consistent → code or test bug. Fix and re-run once.
   └── Flaky (passes on retry without code change)
       ├── Check for race conditions (replace waitForTimeout with waitForSelector / waitForResponse)
       ├── Check for test state leakage (global state between tests)
       └── Check for dev server stale cache (restart server)
```

---

## 内联诊断脚本模板

**不要**为诊断创建临时的 `.spec.ts` 文件，请使用内联脚本：

```bash
pnpm exec node -e "const { chromium } = require('@playwright/test'); (async () => {
  const browser = await chromium.launch({ headless: true });
  const page = await browser.newPage();
  const errors = [];
  page.on('console', msg => { if (msg.type() === 'error') errors.push(msg.text()); });
  page.on('pageerror', err => errors.push(err.message));
  await page.goto('http://127.0.0.1:<PORT>/<PATH>', { waitUntil: 'domcontentloaded', timeout: 30000 });
  await page.waitForTimeout(2000);
  const text = await page.textContent('body');
  console.log(JSON.stringify({ errors, text: text?.substring(0, 500) }, null, 2));
  await browser.close();
})();"
```

根据你的项目自定义 `<PORT>` 和 `<PATH>`。根据需要添加项目特定的运行时检查（调试器 API、状态转储等）。

---

## 分层验证策略

**永远不要为了验证一个修复而运行整个测试套件。** 请按以下升级路径操作：

```
Level 0: Single failing line
  playwright test "path/to/test.spec.ts:LINE" --workers=1

Level 1: Single spec file
  playwright test "path/to/test.spec.ts" --workers=1

Level 2: Related spec files
  playwright test tests/e2e/<feature-area>/*.spec.ts --workers=1

Level 3: Full suite (only before commit / PR)
  playwright test
```

| 变更范围                        | 验证层级        |
| ------------------------------- | --------------- |
| 单个组件/页面                   | 级别 0 → 级别 1 |
| 共享基础设施 (路由、状态、认证) | 级别 1 → 级别 2 |
| CSS/构建流水线/配置             | 级别 1 → 级别 2 |
| 提交或发起 PR 前                | 级别 3          |

---

## 常见失败模式

### 超时 / 元素不可见

**症状**： `toBeVisible()` 失败，`Test timeout of Xms exceeded`

**根本原因（按可能性排序）**：

| 原因               | 如何识别                                                | 修复                                                                                         |
| ------------------ | ------------------------------------------------------- | -------------------------------------------------------------------------------------------- |
| **异步数据未加载** | 检查网络标签页；元素存在但内容是占位符                  | `await page.waitForResponse(...)` 或 `await expect(locator).toBeVisible({ timeout: 10000 })` |
| **竞争条件**       | 未修改代码情况下，重试后测试通过                        | 将 `waitForTimeout(N)` 替换为对异步条件的显式等待                                            |
| **CSS 类未生成**   | 元素在 DOM 中，类已应用，但 `getComputedStyle` 没有效果 | 检查构建流水线（Tailwind `@source`、PostCSS 配置等）                                         |
| **组件未渲染**     | 目标元素根本不在 DOM 中                                 | 检查控制台错误；验证组件注册/路由                                                            |

### 端口冲突

**症状**：`Error: Port XXXX is already in use`

**原因**：之前的开发服务器仍在运行。

**修复**：在启动测试前关闭旧的服务器进程。**不要**通过递增端口号来规避冲突——这会导致产生孤立的进程。

```bash
# Linux / macOS
lsof -ti :4173 | xargs kill -9 2>/dev/null

# Windows
for /f "tokens=5" %a in ('netstat -aon ^| findstr ":4173"') do taskkill /F /PID %a 2>nul
```

在 `playwright.config.ts` 中设置 `reuseExistingServer: !process.env.CI`，使本地运行复用已启动的服务器。

### 不稳定/间歇性失败

**症状**：同一个测试有时通过，有时失败。更改端口能“修复”它。

| 原因                      | 证据                           | 修复                                                              |
| ------------------------- | ------------------------------ | ----------------------------------------------------------------- |
| **陈旧的开发服务器/缓存** | 重启服务器能修复               | 终止并重启；如果适用，清除构建缓存                                |
| **竞争条件**              | 第一次运行失败，立即重试通过   | 为异步依赖添加显式的 `waitFor`                                    |
| **测试执行顺序依赖**      | 单独运行通过，在完整套件中失败 | 使用 `--workers=1` 运行；检查 `beforeAll`/`afterAll` 中的全局状态 |

### 测试状态泄露

**症状**：使用 `--workers=1` 时通过，但并行 worker 时失败。或者单独运行时通过，但在完整套件中失败。

**修复**：确保每个测试都导航到一个干净的页面。不要依赖在 `beforeAll` 中设置的、后续测试所依赖的全局状态。每个测试都应能独立运行。

---

## 反模式

1. **盲目重试循环**：在没有进行任何调查的情况下，将同一个失败的测试重试超过 2 次。每次重试会消耗服务器启动时间 + 测试执行时间。在整个会话中可能浪费数小时。

2. **端口递增**：递增端口号以避免冲突，但留下了 N 个孤立的开发服务器进程。应关闭陈旧的服务器。

3. **对部分变更运行完整套件**：在更改一个组件后运行 `playwright test`（所有 spec）。应先只运行受影响的 spec。

4. **基于截图的调试**：检查 Playwright 失败截图来猜测原因。应使用 `page.evaluate()`、`page.locator().innerHTML()` 和 `getComputedStyle` 进行程序化检查。

5. **创建临时诊断 spec**：编写 `tmp-*.spec.ts` 或 `diag-*.spec.ts` 文件且从不清理。应使用内联 `node -e` 脚本来进行一次性诊断。

---

## Playwright 配置基线

推荐的 `playwright.config.ts` 结构：

```typescript
import { defineConfig, devices } from "@playwright/test";

const port = parseInt(process.env.PLAYWRIGHT_PORT || "4173", 10);
const baseUrl = `http://127.0.0.1:${port}`;

export default defineConfig({
  testDir: "./tests/e2e",
  timeout: 45_000,
  fullyParallel: true,
  forbidOnly: !!process.env.CI,
  workers: 2,
  retries: 0,
  reporter: "list",
  use: {
    baseURL: baseUrl,
    trace: "retain-on-failure",
    screenshot: "only-on-failure",
  },
  projects: [
    {
      name: "chromium",
      use: { ...devices["Desktop Chrome"] },
    },
  ],
  webServer: {
    command: `pnpm dev --host 127.0.0.1 --port ${port} --strictPort`,
    url: baseUrl,
    reuseExistingServer: !process.env.CI,
    timeout: 120_000,
  },
});
```

关键决策：

- `retries: 0` — 不稳定的测试应该被修复，而不是通过重试来掩盖
- `trace: 'retain-on-failure'` — 仅在失败时捕获跟踪信息，以保持 CI 快速
- `PLAYWRIGHT_PORT` 环境变量 — 允许在调试时切换端口
- `reuseExistingServer: !process.env.CI` — 复用本地服务器，在 CI 中全新启动

---

## 推荐的诊断工作流程

```
1. Test fails
   ↓
2. Inspect (inline node -e script, not a new .spec.ts)
   ↓
3. Classify: code bug | test bug | environment flakiness
   ↓
4. Fix
   ↓
5. Verify: single test line (Level 0)
   ↓
6. Expand: full spec file (Level 1)
   ↓
7. If infrastructure change: related specs (Level 2)
   ↓
8. Full suite only before commit (Level 3)
```

---

## 复制后检查清单

复制此模板后，请自定义以下内容：

- [ ] `playwright.config.ts` 中的端口号及所有脚本
- [ ] `webServer.command` 中的开发服务器启动命令
- [ ] `testDir` 路径
- [ ] 添加项目特定的运行时检查钩子（调试器 API、状态转储）
- [ ] 将项目特定的失败模式添加到“常见失败模式”部分
- [ ] 将项目特定的测试文件及其已知问题添加到本地附录
