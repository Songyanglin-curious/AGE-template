# 文档维护检查表

## 目的

在变更落地后使用此文件，检查仓库记忆是否保持同步。

## 非琐碎代码变更后始终审查

1. `docs/architecture/` 中的相关所有者文档
2. `docs/logs/` 中的每日日志
3. 任何受影响的需求、计划、错误说明或测试记录
4. 当建立了有意义的完整验证基线时，`docs/testing/known-good-baselines.md`

## 变更触发器

### 架构或边界变更

审查：

- `docs/architecture/system-baseline.md`
- `docs/architecture/module-boundaries.md`
- 如果路由变更，`docs/index.md`

### 产品意图或范围变更

审查：

- 如果源材料本身发生更改，则审查 `docs/input/` 中的相关文件
- 如果需求解释发生更改，则审查 `docs/discussions/` 中的相关文件
- `docs/requirements/` 中的相关文件
- 如果变会影响长期方向，则审查 `docs/architecture/project-vision.md`

### 应用层功能或流程变更

审查：

- `docs/design/` 中最相关的文件
- 如果面向用户的范围发生更改，则审查 `docs/requirements/`
- 如果需要手动/探索性证明，则审查 `docs/testing/`

### 非琐碎实现切片

审查：

- `docs/plans/` 下的活动计划
- 如果审计是该切片的一部分，则审查 `docs/audits/` 下的相关文件
- `docs/logs/YYYY/MM-DD.md`
- 如果需要探索性/手动证明，则审查 `docs/testing/`

创建的计划需要在实施前进行计划审计，在完成前进行关闭审计。

### 细微回归或根本原因发现

审查：

- `docs/bugs/`
- 如果问题暴露了流程或需求缺陷，则审查 `docs/retrospectives/`
- 任何受影响的所有者文档

## 验证基线

使用 `docs/context/project-context.md` 中的真实项目命令。

如果该文件仍包含占位符，请在声称验证成功之前填写它。
