# 文档命名与时效性

## 目的

本指南用于区分稳定的长期文档与有时效性的过程记录。

对于中小型项目，这样可以在不强制所有文件采用统一命名风格的前提下，保持仓库的易用性。

## 两种类别

### 1. 稳定长期文档

这类文档描述当前支持的基准状态，通常应保持不含日期的稳定名称。

使用稳定名称的场景：

- `docs/process/`
- `docs/architecture/`
- `docs/design/`
- `docs/references/`
- `docs/skills/`
- 长生命周期的需求基线文件，例如 `docs/requirements/product-scope.md` 和 `docs/requirements/mvp.md`

示例：

- `docs/design/app-overview.md`
- `docs/architecture/system-baseline.md`
- `docs/process/application-development-workflow.md`

规则：

- 这类文件应在原地更新
- 不要仅因内容有变化就创建带日期的新版本

### 2. 有时效性的记录

这类文件用于记录执行历史、调查背景或标有日期的决策。

这些文件通常应在路径或文件名中包含日期。

使用带日期命名的场景：

- `docs/logs/`
- `docs/testing/`
- `docs/discussions/`
- `docs/analysis/`
- `docs/audits/`
- `docs/retrospectives/`
- 大多数一次性需求综合文件和实施方案

## 推荐路径规范

### 日志

- `docs/logs/YYYY/MM-DD.md`

### 测试笔记

- `docs/testing/YYYY/MM-DD.md`

### 讨论

- `docs/discussions/YYYY-MM-DD-topic.md`

示例：

- `docs/discussions/2026-05-21-user-management-scope.md`
- `docs/discussions/2026-05-21-order-status-rules.md`
- `docs/discussions/2026-05-21-prototype-gap-checkout-flow.md`

### 分析

- `docs/analysis/YYYY-MM-DD-topic.md`

示例：

- `docs/analysis/2026-05-21-menu-structure-options.md`
- `docs/analysis/2026-05-21-prototype-feasibility-review.md`
- `docs/analysis/2026-05-21-auth-strategy-comparison.md`

### 审计

- `docs/audits/YYYY-MM-DD-<kind>-<topic>.md`

示例：

- `docs/audits/2026-05-21-document-audit-user-management.md`
- `docs/audits/2026-05-21-closure-audit-order-list.md`

### 回顾

- `docs/retrospectives/YYYY-MM-DD-topic.md`

示例：

- `docs/retrospectives/2026-05-21-checkout-prototype-gap.md`
- `docs/retrospectives/2026-05-21-pm-handoff-missing-analysis.md`

### 计划

对于中小型项目，建议使用简单的带日期计划名称：

- `docs/plans/YYYY-MM-DD-topic-plan.md`

示例：

- `docs/plans/2026-05-21-user-list-plan.md`
- `docs/plans/2026-05-21-role-permission-alignment-plan.md`

如果项目后续计划累积较多，需要更强的索引时，可添加数字前缀：

- `docs/plans/NNN-YYYY-MM-DD-topic-plan.md`

示例：

- `docs/plans/012-2026-05-21-user-list-plan.md`
- `docs/plans/013-2026-05-21-checkout-validation-plan.md`

### 一次性需求综合文件

若文件为一次性产出而非稳定基线文档，建议使用带日期的名称：

- `docs/requirements/YYYY-MM-DD-feature-name.md`

示例：

- `docs/requirements/2026-05-21-user-management.md`
- `docs/requirements/2026-05-21-order-refund-flow.md`
- `docs/requirements/2026-05-21-dashboard-homepage.md`

## 缺陷备忘

缺陷备忘属于历史记录，但通常通过问题 ID 而非日期来引用。

对于中小型项目，以下两种方式均可接受：

- `docs/bugs/01-short-bug-name.md`
- `docs/bugs/YYYY-MM-DD-short-bug-name.md`

示例：

- `docs/bugs/01-order-status-double-submit.md`
- `docs/bugs/2026-05-21-login-token-refresh-loop.md`

建议：

- 若缺陷备忘会发展为长期维护的资料库，建议使用编号文件名
- 若缺陷备忘数量较少，主要供团队内部追溯，则基于日期的文件名也可接受

## 简要判断法则

- 若文件回答“当前支持的基准是什么？” → 使用稳定名称
- 若文件回答“本轮/当天/这次调查发生了什么？” → 使用带日期名称

## 快速参考模板

可直接套用以下现成模式：

```text
docs/logs/2026/05-21.md
docs/testing/2026/05-21.md
docs/discussions/2026-05-21-user-management-scope.md
docs/analysis/2026-05-21-auth-strategy-comparison.md
docs/audits/2026-05-21-document-audit-user-management.md
docs/plans/2026-05-21-user-list-plan.md
docs/requirements/2026-05-21-order-refund-flow.md
docs/retrospectives/2026-05-21-checkout-prototype-gap.md
docs/bugs/01-order-status-double-submit.md
```
