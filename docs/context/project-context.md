# 项目上下文

## 目的

保留此文件为 AI 代理在执行有价值工作前所需的最短当前快照。

原地更新。不要创建带日期的副本。

## 项目标识

- 项目名称：
- 产品类型：
- 主要用户：
- 当前里程碑：
- 文档新鲜度：`<fresh | partially stale | stale | unknown>`

## 当前工作

- 当前需求：`docs/requirements/<path-or-none>`
- 当前主责文档：`docs/design/<path>` 或 `docs/architecture/<path>`
- 当前计划：`docs/plans/<path-or-none>`
- 当前待办事项：`docs/backlog/README.md#<item-or-none>`
- AI 自主权：`<implement | plan-first | ask-first | research-only | blocked>`
- 当前阻碍：`<none | describe>`

规则：

- 如果当前需求为 `none`，代理可协助创建或澄清需求和上下文，但不得实现产品行为。
- 如果 AI 自主权不是 `implement`，代理在更改产品行为前必须遵循 `docs/context/ai-autonomy-policy.md`。
- 如果文档新鲜度为 `stale` 或 `unknown`，代理可进行研究、审计和起草对齐文档，但在基线重建或人类确认预期行为之前，不得实现产品行为。
- 如果文档新鲜度为 `partially stale`，代理只能实现那些当前需求、主责文档、代码库映射路径和相关代码区域已经验证为新鲜的切片；否则将该切片视为 `plan-first` 或 `research-only`。

## 当前技术基线

- 前端技术栈：
- 后端技术栈：
- 数据库/模型源：

## 验证命令

在开始实现工作之前，替换所有占位符。

| 目的                | 命令                          |
| ------------------- | ----------------------------- |
| 安装依赖            | `<fill real command>`         |
| 本地运行应用        | `<fill real command>`         |
| 类型检查 / 编译检查 | `<fill real command or none>` |
| 构建                | `<fill real command or none>` |
| Lint / 静态检查     | `<fill real command or none>` |
| 单元测试            | `<fill real command or none>` |
| 端到端 / 集成测试   | `<fill real command or none>` |

## 当前可选层

仅标记本项目实际维护的可选层。

- [ ] `docs/discussions/`
- [ ] `docs/audits/`
- [ ] `docs/testing/`
- [ ] `docs/skills/`
- [ ] `docs/analysis/`
- [ ] `docs/retrospectives/`
- [ ] `docs/lessons/`

## AI 阻止条件

出现以下情况时，AI 必须停止并等待人类输入后才能继续：

- 所有验证命令都是占位符，且无法从项目中推断
- 任何更改涉及支付或数据删除路径，但没有现有测试覆盖，且没有描述预期行为的主责文档

除了 `AGENTS.md`、`docs/context/ai-autonomy-policy.md`、单一真实来源冲突规则以及所需的计划/关闭审计规则之外，上述均为项目特定的硬性停止。

对于不影响用户可见行为、契约、受保护区域或关闭证据的模糊性，可将假设写入相关文档，并根据自主权策略继续。显式标记不确定的假设，以便人类稍后审阅。

## AI 代理注意事项

- 如果此文件为空或过时，在进行大规模实现工作前，请求或创建上下文更新。
- AI 可根据实时仓库证据纠正事实性上下文，但不得在没有人类确认或人类批准的主责文档证据的情况下放宽自主权、移除阻碍、将过时文档标记为新鲜或降低受保护区域的级别。
- 不要仅从聊天中推断当前里程碑或当前计划。
- 在命令仍包含 `<fill real command>` 占位符时，不要报告验证成功。
