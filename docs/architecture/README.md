# 架构文档索引

## 目的

`docs/architecture/` 定义了 `<project-name>` 的稳定的横切技术基线。

使用 `docs/design/` 进行应用层功能与业务设计。使用 `docs/architecture/` 定义跨多个功能的技术结构。

## 建议阅读顺序

1. `project-vision.md`
2. `system-baseline.md`
3. `module-boundaries.md`
4. 随着项目发展，进一步阅读更具体的所有者文档

## 所有者文档规则

- 每个文档只负责一个稳定主题
- 解释当前的理由与约束，而非逐步的历史过程
- 当实现更改底层架构时，在同一变更中更新所有者文档
- 将被否决的方案和探索笔记移至 `docs/analysis/`
- 当技术规则是为了支持具体产品行为而存在时，在 `docs/design/` 下引用相关应用层所有者文档

## 优先级边界

- `docs/design/` 负责应用行为和功能语义
- `docs/architecture/` 负责技术结构和横切实现规则
- 如果问题涉及持久化或数据模型真相，模型/模式文件本身为权威来源

## 初始所有者文档

- `project-vision.md` - 产品与系统意图
- `system-baseline.md` - 当前技术栈与运行时基线
- `module-boundaries.md` - 包/模块/领域所有权边界
