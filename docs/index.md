# <project-name> 文档索引

## 目的

该 `docs/` 树是 `<project-name>` 的持久记忆与路由界面。

- 在更改工作流、需求、设计或实现之前，请先查阅此处
- 优先选择能回答当前问题的最小文件
- 将持久结论保留在文件中，而不仅仅是在聊天里

## 路由权限

此文件是顶级文档路由器。

- `docs/index.md` 负责导航和目录职责
- `AGENTS.md` 负责代理工作流规则和执行期望
- `docs/design/` 和 `docs/architecture/` 负责稳定的项目吸引子

## 请先阅读

| 如果你需要……                                 | 先阅读这份内容                                      | 然后阅读以下内容                                                                                                                       |
| -------------------------------------------- | --------------------------------------------------- | -------------------------------------------------------------------------------------------------------------------------------------- |
| 了解强制性的 AI 上下文和当前项目状态         | `docs/context/README.md`                            | `docs/context/project-context.md`, `docs/context/ai-autonomy-policy.md`, `docs/context/codebase-map.md`                                |
| 了解轻量级默认开发工作流                     | `docs/process/application-development-workflow.md`  | `AGENTS.md`                                                                                                                            |
| 选择下一个 AI 就绪的工作项                   | `docs/backlog/README.md`                            | `docs/context/ai-autonomy-policy.md`、活跃需求与负责人文档                                                                             |
| 阅读原始 PM、原型、文章或卡片集输入材料      | `docs/input/README.md`                              | `docs/input/` 中的活跃文件                                                                                                             |
| 阅读说明性方法论文档                         | `docs/articles/README.md`                           | `docs/articles/` 下的相关文章                                                                                                          |
| 澄清模糊的需求                               | `docs/discussions/README.md`                        | `docs/requirements/00-requirement-synthesis-guide.md`                                                                                  |
| 在编码前对任务进行路由                       | `AGENTS.md`                                         | `docs/skills/README.md`、相关负责人文档以及 `docs/plans/00-plan-authoring-and-execution-guide.md`                                      |
| 判断现有技能是否适用                         | `docs/skills/README.md`                             | 相关负责人文档和活跃需求                                                                                                               |
| 了解项目目标和产品形态                       | `docs/architecture/project-vision.md`               | `docs/design/app-overview.md`                                                                                                          |
| 了解当前应用层基线                           | `docs/design/app-overview.md`                       | `docs/design/feature-inventory.md`, `docs/design/roles-and-permissions.md`                                                             |
| 了解当前技术基线                             | `docs/architecture/system-baseline.md`              | `docs/architecture/module-boundaries.md`                                                                                               |
| 了解负责人文档的优先级和唯一事实来源边界     | `docs/context/source-of-truth-and-precedence.md`    | 相关负责人文档                                                                                                                         |
| 开始或审查一项重要实现                       | `AGENTS.md`                                         | `docs/skills/README.md`, `docs/plans/00-plan-authoring-and-execution-guide.md`、活跃计划以及 `docs/audits/00-audit-execution-guide.md` |
| 审查审计工作流或所需的计划/收尾审计          | `docs/audits/00-audit-execution-guide.md`           | `docs/skills/` 中的相关提示                                                                                                            |
| 了解哪些文档应使用带日期的文件名而非固定名称 | `docs/references/document-naming-and-timeliness.md` | 目标目录中的相关指南                                                                                                                   |
| 快速复制新版带日期文档的推荐文件名模式       | `docs/references/document-naming-and-timeliness.md` | `Quick Copy Set` 小节                                                                                                                  |
| 复制现成的带日期文档框架                     | `docs/examples/README.md`                           | 重命名最接近的 `.example.md` 文件                                                                                                      |
| 查看一个真实的小功能演示                     | `docs/examples/complete-small-app-walkthrough.md`   | 然后从 `docs/examples/` 复制最接近的框架                                                                                               |
| 诊断 E2E 测试失败（Playwright）              | `docs/references/playwright-e2e-guide.md`           | `playwright.config.ts`                                                                                                                 |
| 检查变更后必须更新哪些文档                   | `docs/references/maintenance-checklist.md`          | `docs/design/` 或 `docs/architecture/` 中最相关的文件                                                                                  |
| 查看近期实现历史                             | `docs/logs/index.md`                                | 最新的带日期日志文件                                                                                                                   |
| 查找过去微小的回滚问题                       | `docs/bugs/00-bug-fix-note-writing-guide.md`        | `docs/bugs/` 中的相关文件                                                                                                              |
| 记录或审查探索性/手动测试                    | `docs/testing/index.md`                             | 相关的带日期测试笔记                                                                                                                   |
| 检查最新已知的良好验证状态                   | `docs/testing/known-good-baselines.md`              | 最新的带日期测试或日志笔记                                                                                                             |
| 审查权衡或开放性的设计调研                   | `docs/analysis/README.md`                           | 相关的分析笔记                                                                                                                         |
| 阅读持久可复用的工程经验教训                 | `docs/lessons/README.md`                            | 相关编号的经验教训文档                                                                                                                 |
| 阅读可供实施的详细需求                       | `docs/requirements/README.md`                       | 活跃的需求文件                                                                                                                         |
| 审查为何已上线结果仍未达到预期               | `docs/retrospectives/README.md`                     | 相关的回顾笔记                                                                                                                         |

## 推荐的默认路径

对于大多数中小型项目，默认路径为：

1. `docs/context/`
2. 选择工作时 `docs/backlog/`
3. `docs/input/`
4. `docs/requirements/`
5. `docs/design/` 与 `docs/architecture/`
6. 任务路由并选择候选可复用技能
7. 应用规划触发器时 `docs/plans/`
8. 对于必需的方案/收尾审计或已存审计证据，使用 `docs/audits/`
9. `docs/logs/`
10. 需要时 `docs/bugs/`

仅当任务复杂性或模糊性需要时，才使用 `docs/discussions/`、额外的 `docs/testing/` 笔记、`docs/skills/`、`docs/analysis/` 和 `docs/retrospectives/`。

## 技能路由

| 如果任务是...            | 先阅读此内容                                          | 然后决定                                                                                   |
| ------------------------ | ----------------------------------------------------- | ------------------------------------------------------------------------------------------ |
| 需求不明确               | `docs/requirements/00-requirement-synthesis-guide.md` | 是否需要先准备需求文件或讨论文件                                                           |
| 非平凡实现               | `AGENTS.md`                                           | 每个阶段或事项需要哪些技能，然后使用 `docs/plans/00-plan-authoring-and-execution-guide.md` |
| 文档、方案或收尾验证     | `docs/skills/README.md`                               | 适用哪个审计提示或评审技能                                                                 |
| 重复的已知方法或评审模式 | 相关所有者文档                                        | 现有技能是否适用，还是需要创建新技能                                                       |

技能选择工作方法。它们不会取代需求、设计、架构或所有者文档路由。

## 目录角色

- `docs/process/` - 工作流程和操作过程文档
- `docs/context/` - 强制性的 AI 上下文、所有者优先级和项目全局约定
- `docs/backlog/` - 带优先级的候选工作项和 AI 就绪的后续操作
- `docs/input/` - 原始外部输入和复制的源材料
- `docs/discussions/` - 可选的需求澄清和未解决问题记录
- `docs/requirements/` - 综合的、可实施就绪的需求文档
- `docs/design/` - 稳定的应用层特性和业务流程所有者文档
- `docs/architecture/` - 稳定的技术基线和模块边界文档
- `docs/lessons/` - 从重复问题和恢复中提取的持久工程经验
- `docs/references/` - 稳定的查找指南和维护辅助
- `docs/articles/` - 面向外部的方法论和说明文章
- `docs/examples/` - 用于含日期工作文档的小型可复制骨架
- `docs/plans/` - 带收尾标准的执行方案
- `docs/audits/` - 审计方法和审计记录，包括为已创建方案所需的方案/收尾审计证据
- `docs/skills/` - 可选的可重用 AI 提示和审计/评审手册
- `docs/logs/` - 带有日期的实施记忆
- `docs/testing/` - 可选的探索性测试和手动测试笔记
- `docs/bugs/` - 复杂的回归历史记录和根因笔记
- `docs/analysis/` - 可选的调查、比较和设计权衡
- `docs/retrospectives/` - 可选的事后交付差距分析和流程改进
- `docs/archive/` - 由人工决定移至此处的不活跃文档；保留作历史参考

## 核心原则

使用文件保存持久事实。

- 输入捕获需求来源
- 上下文捕获强制性项目规则和事实来源优先级
- 待办捕获带优先级的后续操作和自主性标签
- 讨论捕获不明确之处
- 需求捕获应构建的内容
- 设计和架构捕获必须保持不变的内容
- 事实来源优先级指明每个问题中哪个工件胜出
- 方案捕获如何收尾一个非平凡的切片
- 审计捕获如何质疑声明
- 日志、测试和缺陷笔记保存证据和记忆
- 回顾解释为何上一次迭代仍未达标

## 命名规则

- 稳定的所有者文档保持稳定名称
- 时效性记录通常应包含日期
- 参见 `docs/references/document-naming-and-timeliness.md`
