# 待办事项

## 用途

使用此文件列出 AI 可能检查或执行的候选工作项。

待办事项列表不能替代需求文档、负责人文档或计划。它仅用于帮助选择下一个工作切片。

## 工作项

| 优先级 | 工作项          | 需求                       | 负责人文档           | 计划                        | 状态                | AI 自主性 | 阻塞项                               | 上次检查       |
| ------ | --------------- | -------------------------- | -------------------- | --------------------------- | ------------------- | --------- | ------------------------------------ | -------------- |
| P0     | `<first slice>` | `docs/requirements/<path>` | `docs/design/<path>` | `docs/plans/<path-or-none>` | `needs-requirement` | `blocked` | `template placeholders not replaced` | `<YYYY-MM-DD>` |

## 就绪不变条件

`ready` 表示以下所有条件均为真：

- 需求路径存在且具有可测试的验收标准
- 负责人文档路径存在，且针对此切片未被标记为过时
- `docs/context/project-context.md` 中的验证命令是真实的
- 不存在阻塞性的开放问题，或已明确为非阻塞性
- 已在 `docs/context/ai-autonomy-policy.md` 中配置受保护区域
- 已检查规划触发器

`Plan: none` 仅在项目明确符合 `docs/plans/00-plan-authoring-and-execution-guide.md` 中的无计划路径时有效。如果需要计划，请将 AI 自主性设置为 `plan-first`，直到计划审核通过。

代理可凭借证据将过时的行从 `ready` 降级为 `needs-*` 或 `blocked`。代理不得将行升级到 `ready`，不得将自主性更改为 `implement`，也不得在未经人类确认或未经人类批准的负责人文档证据的情况下清除阻塞项。

设置后就绪行的示例：

```md
| P0 | User Management first slice | `docs/requirements/2026-05-21-user-management.md` | `docs/design/app-overview.md` | `docs/plans/2026-05-21-user-management-plan.md` | `ready` | `plan-first` | `none` | `2026-05-21` |
```

## 状态值

- `idea` - 未准备好实施
- `needs-requirement` - 存在原始输入，但不存在可供实施的需求
- `needs-design` - 需求存在，但负责人文档缺失或过时
- `ready` - AI 可根据自主性标签继续工作
- `in-progress` - 当前正在实施或规划中
- `blocked` - 在解决阻塞项之前无法继续
- `done` - 已完成并验证

## AI 自主性值

使用 `docs/context/ai-autonomy-policy.md` 中的值：

- `implement`
- `plan-first`
- `ask-first`
- `research-only`
- `blocked`

## 选择规则

当被要求在没有指定任务的情况下继续时，请选择优先级最高的 `ready` 工作项，其 `AI Autonomy` 为 `implement`，且其 `Blocker` 为 `none`。

在实施之前，请确认关联的需求、负责人文档、计划字段、自主性策略和规划触发器仍然有效。不要仅凭聊天推断就绪状态。

如果表格过时，降级该行或在实施前询问。
