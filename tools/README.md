# 工具工作区

`tools/` 是一个独立的 pnpm 子项目，用于存放仓库本地的工程实用工具。

模板根目录特意设计为非 Node.js 项目。这样既能保证复制后的模板可用于非 Node 仓库，同时又允许可选的基于 Node 的工具。

此目录中的脚本会检查父仓库。

## 安装

从 `tools/` 运行：

```bash
pnpm install
```

## 工具选择规则

此目录中保留的文件应至少满足以下条件之一：

- 足够通用，可用于多个复制出来的项目
- 足够具有代表性，可作为可复用的示例模式

不要保留一次性迁移脚本、特定仓库的清理脚本，或主要编码了某个团队命名策略的工具。

## 核心工具

- `check-active-doc-code-anchors.mjs`：验证当前文档中引用的仓库路径
- `check-oversized-code-files.mjs`：标记超出行数阈值的已跟踪代码文件
- `check-docs-garbled.mjs`：扫描文档中的可疑 Unicode 字符和乱码

这些工具轻量、通用，适合默认保持启用。

## 示例工具

- `check-duplicates.mjs`：封装 `jscpd`，用于复制粘贴检测
- `code-stats.mjs`：输出代码与文档统计信息
- `audit/`：基于规则的审查扫描器示例及起始规则

这些工具作为可复用工具模式的代表性示例保留，并非每个复制项目都必须遵循的强制策略。

## 常用命令

从 `tools/` 运行：

```bash
pnpm check
pnpm stats
pnpm check:duplicates
pnpm audit:suspects
```

## 配置

- `check-active-doc-code-anchors.mjs`
  使用 `AGE_REPO_ROOT`、`AGE_ACTIVE_DOC_ROOTS` 和 `AGE_ACTIVE_DOC_FILES`。
- `check-oversized-code-files.mjs`
  使用 `AGE_OVERSIZED_WARN_LINES`、`AGE_OVERSIZED_ERROR_LINES` 和 `AGE_CODE_ROOT_PREFIXES`。
- `check-duplicates.mjs`
  使用 `AGE_DUPLICATE_SCAN_ROOTS`。
- `audit/`
  使用 `AGE_AUDIT_ROOTS`。
