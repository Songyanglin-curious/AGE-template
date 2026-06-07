# 计划编写与执行指南

## 目标

`docs/plans/` 用于非简单的执行片段，这些片段需要明确的范围、关闭标准和证明。

## 何时编写计划

在以下情况下编写计划：

- 更改 API、数据库/模型、认证、集成、部署或公共契约行为
- 更改跨多个功能界面的用户可见行为
- 涉及多个模块并更改共享行为
- 预计需要多个 AI 会话
- 修改超过 5 个文件或可能超过约 200 行更改
- 需要分阶段实施或在关闭前进行明确证明

仅当本地低风险编辑（如文案更改、小型样式修复、仅测试清理以及具有明确现有测试的单文件行为修复）时，才跳过正式计划。

## 计划决策表

| 范围                                                                               | 计划级别 | 审计规则                       | 示例                                                                |
| ---------------------------------------------------------------------------------- | -------- | ------------------------------ | ------------------------------------------------------------------- |
| 简单的本地编辑                                                                     | 无需计划 | 无计划审计                     | 拼写错误/文案更改、单个样式微调、仅测试清理                         |
| 非简单的跟踪工作                                                                   | 完整计划 | 需要独立计划审计和独立关闭审计 | 带有文档/测试更新的小型 UI 打磨、具有明确现有测试的简单本地错误修复 |
| 合约、数据/模型、API、认证、权限、集成、部署、跨界面、陈旧文档冲突或明显高风险范围 | 完整计划 | 需要独立计划审计和独立关闭审计 | 结账流程、登录行为、数据迁移、外部 webhook、多模块重构              |

如果不确定，请使用完整计划。

## 最低规则

1. **从现有基线开始。** 首先阅读代码仓库，再编写 `Current Baseline`。不要依赖记忆或旧计划。对于全新功能，基线必须盘点该功能将触及或冲突的所有现有代码——硬编码值、缺失的钩子、不兼容的模式。盘点不是可选项。
2. **明确目标与非目标。** 如果任一不清晰，计划边界就尚未就绪。
3. **使用复选框进行执行和收尾。** 未勾选的项目意味着工作未完成，直至收尾。
4. **一个计划，一个成果面。** 如果计划需要多个独立的收尾标准，则范围过宽。应拆分。共享相同行为契约和收尾标准的多模块提取或迁移，仍属于单一成果面——不要过度拆分。
5. **收尾前提供证明。** 在仓库包含每个退出标准的可验证证明之前，不得将计划标记为完成。
6. **不要转储代码设计。** 计划应包含范围、证明和收尾逻辑，而非低级实现细节。例外：重构和提取计划必须包含提取模块之间的接口契约——这些是结构边界定义，而非实现伪代码。
7. **为项目标注类型。** 每个执行项目必须标注为 `Fix`、`Add`、`Decision`、`Proof` 或 `Follow-up`。`Fix` 表示缺陷修复；`Add` 表示全新代码或配置。一个项目可以有多个类型（例如，`Decision | Add`）；此时所有隐含义务均适用。已确认的线上缺陷或契约偏离必须标记为 `Fix`，而非 `Follow-up`。当某个阶段 80% 以上的项目共享同一类型时，应在阶段级别声明统一类型，而非逐项声明（例如，`Phase 1 — Fix-heavy (8/10 items tagged Fix)`）。
8. **有意识地记录技能使用。** 对于可复用技能发挥作用的每个阶段或项目，记录 `Skill: <name>` 或 `Skill: none`。技能选择工作方法，而非业务真相。如果指定了技能，则其所需输入和预期输出必须从 `docs/skills/README.md` 和引用的负责人文档中清晰可见。
9. **记录决策及理由。** 每个 `Decision` 项目必须记录所选方案、考虑过的替代方案以及残余风险（若有）。将理由写入计划或引用的文档中。如果决策需要先进行原型设计或探索，则添加一个临时的 `Explore` 项目，该项目必须在 `Decision` 解决之前完成。由框架强制或显而易见的决策（例如，“必须匹配现有框架模式”）可标记为受约束，无需进行全面替代方案分析。
10. **收尾前检查清单完整性。** 在将计划标记为完成之前，范围内任何清单项目不得保持未勾选状态。要么完成它，要么明确将其移出范围并附上书面理由。计划批准后缩小范围属于范围变更，必须记录理由；无声无息地将项目移出范围是违规行为。
11. **收尾前检查文本一致性。** 在收尾前，确认 `Plan Status`、每个阶段的 `Status`、每个阶段的 `Exit Criteria`、`Closure Gates` 和 `docs/logs/` 条目均保持一致。不能上面写着 `completed` 而内部某个阶段仍写着 `planned`。
12. **独立的计划与收尾审计。** 不要实现刚创建出来的计划，除非它已通过计划审计；不要因为完成了最后一块实现就顺便将其标记为完成。应使用独立的审查环节。受保护区域、未解决的产品风险以及单一事实来源冲突需要人工/子代理审查或保持开放状态。
13. **不可降级的项目** 不能降级为非阻塞的后续工作：已确认的线上缺陷、已确认的契约偏离、已确认的负责人文档偏离以及仓库中已修复的 CI/lint 规则。

### 反松懈规则

收尾前，每个范围内项目必须正好处于以下状态之一：`landed`、`adjudicated as residual-risk-only`、`moved to explicit successor ownership` 或 `removed from scope with recorded reason`。

对于范围内项目，以下词语禁止使用：`optional`、`if time permits`、`consider`、`maybe`、`nice to have`、`as needed`。如果某项确实可选，应明确将其移出范围，而非将其留在模糊状态。

`Follow-up` 项目必须指明将其提升到范围内的触发条件（例如，“当用户数超过 1 万时”）。`Deferred But Adjudicated` 项目必须指明重新开启它的事件或决定（例如，“如果新 API 被采用，本工作可能变得多余”）。

## 执行期间

1. 实施前，记录计划审计证据。
2. 开始一个切片时，将其 `Status` 更新为 `in progress`。
3. 完成一个切片时，将其 `Status` 更新为 `completed`，并勾选其所有执行项目和退出标准。
4. 执行某个阶段前，确认列出的 `Skill` 仍与任务和可用输入匹配。若不匹配，先更新计划再继续。
5. 如果切片改变了现有基线或公共契约，其退出标准必须包含文档更新步骤。若无需文档更新，明确写上 `No owner-doc update required`。
6. 不要因为函数签名存在就将切片标记为完成。要验证行为、错误处理和测试覆盖也已到位。
7. 如果某项无法完成，将其移至 `Deferred But Adjudicated` 并附上分类和理由。不要让它留在执行清单中未勾选。
8. 保持 `docs/logs/` 与计划进度同步。当所有阶段在同一冲刺中覆盖同一功能时，计划收尾时一条汇总日志条目即可；仅当阶段跨越不同日期或不同交付物时，才需要单独为每个阶段记录条目。

## 收尾时

在设置 `Plan Status: completed` 之前，完成以下所有事项：

**所有创建的计划：**

1. 检查每个阶段 `Exit Criteria` — 每一个都必须 `[x]`。
2. 检查每个 `Closure Gates` 项 — 每一个都必须 `[x]`。
3. 验证文本一致性：顶部状态、阶段状态、退出标准、关闭关卡和日志条目全部一致。
4. 区分“接口存在”与“行为完整”。通过测试或演示验证实际的运行时行为，而不仅仅是类型签名。
5. 对仓库运行真实的验证命令。对于主要成果面是视觉、行为或 UX 驱动的计划，在计划中明确说明理由，自定义验证关卡。
6. 执行独立的关闭审计。

**完全关闭**（多会话、多模块或高风险计划 — 添加以下内容）：

7. 从头重读整个计划，而不仅仅是最近的部分。
8. 在计划的 `Closure` 部分记录独立审计证据，并在 `docs/audits/` 下链接任何存储的审计文件。

如果其中任何一项失败，计划保持开放。

## Template

```md
# <plan-id> <title>

> Plan Status: planned
> Last Reviewed: YYYY-MM-DD
> Source: <requirement / bug / analysis / request>
> Related: <related plans, optional>
> Audit: required

## Current Baseline

- <what is true today>
- <what gap remains>

## Goals

- <result to achieve>

## Non-Goals

- <explicitly excluded work>

## Task Route

- Type: `<requirement clarification | app-layer design change | architecture change | implementation-only change | bug investigation | verification or audit work>`
- Owner Docs: `<paths>`
- Skill Selection Basis: `<why these skills or none apply>`

## Infrastructure And Config Prereqs

- <ports, env vars, CORS, secrets, .env, external services this feature depends on>
- <if none, write "No infra prereqs beyond existing baseline">
- <for data-migration plans: include rollback strategy or script path>

## Execution Plan

### Phase 1 - <name>

Status: planned
Targets: `<paths>`
Skill: `<skill-name | none>`

- Item Types: `Fix | Decision | Proof | Follow-up`
- Prereqs: <phases or external dependencies that must complete first>

- [ ] <implementation item>
          - Skill: `<skill-name | none>`
- [ ] <Decision: record rationale and alternatives in the item or a referenced doc>
  - Skill: `<skill-name | none>`
- [ ] <Proof: specify test strategy (unit/integration/e2e) and exact verification commands>
  - Skill: `<skill-name | none>`

Exit Criteria:

- [ ] <behavior lands — specify success and failure modes>
- [ ] <relevant docs updated, or No owner-doc update required>
- [ ] `docs/logs/` updated

## Plan Audit

- Status: <pending | passed>
- Reviewer / Agent: <independent reviewer, subagent, or cold-replay proxy>
- Evidence: <task id / audit file>

## Closure Gates

- [ ] in-scope behavior is complete
- [ ] relevant docs are aligned
- [ ] verification has run (specify which commands; customize for visual/UX domains if needed)
- [ ] no in-scope item downgraded to deferred/follow-up
- [ ] plan audit passed before implementation
- [ ] text consistency verified: status, phases, gates, and log all agree
- [ ] closure audit was independent
- [ ] closure evidence exists in files

## Deferred But Adjudicated

### <item name>

- Classification: `watch-only residual | optimization candidate | out-of-scope improvement`
- Why Not Blocking Closure: <reason>
- Successor Required: `yes | no`

## Closure

Status Note: <why the plan can close>

Closure Audit Evidence:

- Reviewer / Agent: <independent reviewer or cold-replay proxy>
- Evidence: <task id / log link / walkthrough record>

Follow-up:

- <non-blocking follow-up items only; confirmed defects must not appear here>
```
