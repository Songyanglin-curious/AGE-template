# 复制后从此处开始

复制模板到新项目后立即使用此检查清单。

在要求 AI 实现功能之前执行此操作。

## 首次 AI 编码前必须完成

- [ ] 替换 `<project-name>` 和其他占位符。
- [ ] 用真实项目身份、活动工作和验证命令填写 `docs/context/project-context.md`。
- [ ] 用真实保护区范围和 AI 自主默认值填写 `docs/context/ai-autonomy-policy.md`。
- [ ] 用真实入口点、常见变更路线和易出问题文件填写 `docs/context/codebase-map.md`。
- [ ] 用第一个就绪或受阻的工作项填写 `docs/backlog/README.md`。
- [ ] 将 `docs/context/project-context.md` 中的 `Documentation freshness` 设置为 `fresh`、`partially stale`、`stale` 或 `unknown`。
- [ ] 在 `docs/context/ai-autonomy-policy.md` 中设置审查者可用性。
- [ ] 选择第一个活动需求文件并将其记录在 `docs/context/project-context.md` 中。
- [ ] 确保活动需求具有具体的验收标准。
- [ ] 选择第一个活动所有者文档并将其记录在 `docs/context/project-context.md` 中。
- [ ] 确保验证命令是本仓库的真实命令。
- [ ] 为当前年份创建 `docs/logs/{year}/` 目录（例如 `docs/logs/2026/`）。有关日志约定，请参见 `docs/logs/00-log-writing-guide.md`。

对于直接本地的低风险编辑，如果活动需求/所有者文档的含义显而易见且验证命令真实，则不要因待办事项列表不完善或代码库地图而阻塞。保护区、过时文档、缺失验证或用户可见行为不明确仍然会阻塞编码。

## 逐步填写

在需要时立即填写这些内容。不要为了编写完善的基线文档而阻塞第一个小功能。

- [ ] 用长期产品方向和非目标填写 `docs/architecture/project-vision.md`。
- [ ] 用真实技术栈和模型/数据库源填写 `docs/architecture/system-baseline.md`。
- [ ] 用当前应用界面、角色和核心工作流填写 `docs/design/app-overview.md`。
- [ ] 用当前里程碑范围填写 `docs/requirements/product-scope.md` 和 `docs/requirements/mvp.md`。
- [ ] 当真实命令通过时，将第一个已知良好的验证行添加到 `docs/testing/known-good-baselines.md`。
- [ ] 通过勾选 `docs/context/project-context.md` 中的复选框来决定激活哪些可选层。
- [ ] 删除或忽略暂时不维护的可选目录。

## 编码前的最低要求

- [ ] 活动需求具有具体的验收标准。
- [ ] 活动所有者文档已列在 `docs/context/project-context.md` 中。
- [ ] AI 自主权为 `implement`，或工作明确为 `plan-first` 且只会编写计划。
- [ ] 保护区占位符已替换为真实条目或明确标识为 `none`。
- [ ] 文档新鲜度不是 `stale` 或 `unknown`，除非第一个任务仅为研究或基线对齐。
- [ ] 验证命令是本仓库的真实命令。
- [ ] 原始输入、需求、所有者文档和实际代码之间的任何冲突均已解决或明确阻塞。

## 遇到以下情况不要开始

- `docs/context/project-context.md` 仍为空白。
- 验证命令是占位符。
- 保护区占位符仍然存在，且任务涉及认证、权限、支付、数据删除、模型/模式、部署或外部集成。
- 活动需求为 `none`。
- AI 自主权为 `ask-first`、`research-only` 或 `blocked`，且没有人类决策更改它。
- 文档新鲜度为 `stale` 或 `unknown`，且任务会改变产品行为，而不是审计或对齐基线。
- 活动需求不够明确，以至于实现需要猜测用户可见行为。
- 任务涉及数据库/API/认证/集成行为的更改，但未确定所有者文档或模型来源。
