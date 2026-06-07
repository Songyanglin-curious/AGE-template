# 错误修复说明编写指南

## 目的

对于非显而易见的回归、微妙的根本原因以及应影响未来审查的修复，请使用 `docs/bugs/`。

目标不是重复完整的差异。目标是保留出了什么问题、它是如何被发现的、为什么会发生，以及如何防止其再次出现。

## 何时编写错误说明

当至少满足以下条件之一时编写一个说明：

- 错误具有非显而易见的根本原因
- 错误跨越了模块或包边界
- 错误表面看起来像一件事，但实际是由另一层引起的
- 修复添加或更改了回归测试
- 未来的重构很容易重新引入相同的问题

不要为每个微小的拼写错误或琐碎的单行修复编写说明。

## 必需部分

每个错误说明应包含这些部分。保持各部分简短。

### 1. 问题

用2-5行描述观察到的症状。包括什么被破坏了、破坏位置、最小的可重现行为，以及影响或严重性（受影响的用户、数据完整性、影响范围）。

### 重现

描述所需的环境状态和触发操作，以便未来的读者可以重现。包括确切的步骤、任何前提条件（例如，“必须以管理员身份登录”、“需要2000个并发请求”），以及如果适用的话，一个最小的重现脚本。

### 2. 诊断方法

此部分为必填。描述如何定位问题，而不仅仅是最终的根因。

包括：

- 是什么使诊断变得困难
- 首先检查了什么以及为什么
- 测试并排除了哪些假设（如果诊断非平凡，则为必填）
- 哪些直接证据确认了真正的原因

如果诊断很直接（单一的“确凿证据”指标或日志），明确说明这一点并解释为什么不需要迭代——例如，“崩溃堆栈跟踪恰好指向我们代码中的返回语句（第2帧是我们的代码）”。否则，至少包括一个已排除的替代路径。

### 3. 根本原因

用1-3个要点解释真正的原因。提及涉及的实际模块或子系统。如果错误有多个原因，请清楚地分开它们。

**边界规则：** 诊断方法涵盖调查*过程*和证据链。根本原因涵盖从系统内部角度解释错误为何发生的机制*解释*。这两个部分不应重复相同的信息。对于调查直接揭示机制的bug（因果联系即证据链），这两个部分可以合并到 `*Diagnosis & Root Cause` 下，并附上解释原因的注释。

### 4. 修复

从设计意图的角度解释解决方案，而不是逐行代码更改。包括更改了什么、在哪里更改，以及为什么它能解决根本原因。

### 5. 测试

列出添加或更新的回归测试覆盖。包括测试文件路径、测试保护的内容以及测试级别（单元/组件/集成/e2e）。对于仅e2e覆盖的情况，说明为什么较低级别不可行。

如果自动化测试不切实际（竞态条件、时序、第三方依赖），请记录手动验证过程，并明确说明为什么没有添加自动化测试。

### 6. 受影响的工件

列出更改的代码文件、配置文件、部署清单或基础设施定义。使用 `path/to/file.ts:line-numbers` 格式并附上简短注释。不要粘贴大的差异。

### 7. 对未来重构的说明

添加1-3个要点，描述未来的更改应注意不要破坏什么。在受影响的工件中命名一个具体的代码模式和一个具体的错误场景（例如，“如果有人更换了池库，新驱动程序可能依赖 `finalize()` 而不是显式的 `close()`”）。这一部分很重要，因为这些说明的主要价值在于长期记忆。

### 8. 预防缺口（可选）

添加1-2个要点，说明缺少了哪个审查、测试或流程步骤导致了此错误的发布。这是关于系统性缺口，而不是个人指责。示例：“没有负载测试覆盖2000个并发请求的路径”或“此页面没有基于路由的导航测试”。

## 推荐模板

```md
# 0X Short Bug Fix Title

## Problem

- what broke
- where it broke
- minimal visible symptom
- impact or severity

## Reproduction

- environment and preconditions
- triggering steps
- minimal reproduction script if applicable

## Diagnostic Method

- diagnosis difficulty (why this was hard, or "straightforward")
- investigation path (what was checked first)
- rejected hypotheses (if diagnosis was non-trivial)
- decisive evidence that confirmed the issue

## Root Cause

- actual cause 1
- actual cause 2
- (may merge with Diagnostic Method as `*Diagnosis & Root Cause` if the evidence trail IS the mechanism)

## Fix

- main change 1
- main change 2

## Tests

- `path/to/test-file` - what it verifies (level: unit/component/integration/e2e)
- if no automated test: manual verification steps and reason

## Affected Artifacts

- `path/to/file:lines` - annotation

## Notes For Future Refactors

- risk or invariant 1 (concrete pattern + concrete mistake scenario)
- risk or invariant 2

## Prevention Gap (optional)

- what review/test/process step was missing
```

## 文件命名指南

对于中小型项目，两种风格都可以接受：

- 编号式： `docs/bugs/01-short-bug-name.md`
- 日期式： `docs/bugs/YYYY-MM-DD-short-bug-name.md`

如果您预期错误说明会成为长期参考库，请优先使用编号式文件名。

## 验证清单

在提交错误说明之前，请验证：

- [ ] 问题包括影响或严重性
- [ ] 重现包括环境、触发条件和最小步骤
- [ ] 诊断方法描述调查*过程*，而不仅仅是原因
- [ ] 诊断方法包括被排除的假设（或明确说明“直接”并给出理由）
- [ ] 根本原因指出特定的模块或子系统；或者合并的部分已注释
- [ ] 修复解释更改*为什么*有效，而不仅仅是*什么*被更改
- [ ] 测试包括测试级别（单元/组件/集成/e2e），或记录手动验证并给出明确理由
- [ ] 对未来重构的说明命名一个具体的模式和一个具体的错误场景

## 其他规则

- 每个非平凡的bug修复都应添加或更新自动化测试覆盖。
- 如果创建了错误说明，请包含测试证明路径或验证证据。
- 使用 `docs/architecture/` 记录当前设计真相，使用 `docs/bugs/` 记住重要的失败以及修复存在的原因。
