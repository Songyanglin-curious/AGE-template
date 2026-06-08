# 文档审计提示

在实施前审计需求和设计文档时使用此提示。

```text
阅读 `AGENTS.md`、`docs/index.md`、`docs/process/application-development-workflow.md`，以及 `docs/input/`、`docs/requirements/`、`docs/design/` 和 `docs/architecture/` 下的活跃文件。

针对应用层实现任务，审计当前的文档基线。

关注要点：
- 缺失的范围边界
- 伪装成已定需求的未决问题
- 原始输入与合成需求之间的不匹配
- 需求与负责人文档之间的不匹配
- 将原型误当作完整需求来源的情况

首先按严重性排序反馈发现的问题。
对每项发现，包含：
- 标题
- 受影响文件
- 当前缺口
- 对实现的风险
- 建议

若没有遗留发现，需明确说明并注明残余风险。
```
