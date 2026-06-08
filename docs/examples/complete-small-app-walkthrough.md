# 完整简单应用演练

本示例展示了一个小型功能切片的预期形态。

它有意保持精简。重点在于展示具体内容，而非一个庞大的流程。

## 1. 原始输入

目标文件：

- `docs/input/source-pm-user-management.md`

```md
# PM 备注 - 用户管理

需要一个面向管理员的后台用户管理页面。

管理员应能查看用户列表，按姓名或邮箱搜索，并可禁用某个用户。
被禁用的用户将无法登录。
首个版本中，我们不需要创建/编辑用户资料的功能。
```

## 2. 需求

目标文件：

- `docs/requirements/2026-05-21-user-management.md`

```md
# 用户管理需求

## 目标

管理员可查看用户、搜索用户并禁用启用的用户。

## 范围内

- 用户列表页面
- 按姓名或邮箱搜索
- 对启用用户的禁用操作
- 禁用用户无法登录

## 范围外

- 创建用户
- 编辑用户资料
- 批量操作

## 业务规则

- 仅管理员可访问该页面
- 禁用用户在登录时被阻止
- 对于已禁用的用户，不显示可用的禁用操作

## 角色 / 权限

- 管理员：可访问该页面并禁用启用的用户。
- 非管理员：无法访问该页面。

## 数据 / 模型影响

- 现有用户模型须暴露 `id`、`name`、`email` 和 `status` 字段。
- 禁用操作会将用户状态从 `active` 改为 `disabled`。
- 此切片无需新增数据库表。

## API / 集成影响

- 需要一个用户列表查询端点。
- 需要一个禁用用户的命令端点。
- 此切片无需外部系统集成。

## 状态

- 空状态：无匹配用户时显示空状态界面。
- 加载中：获取用户列表时显示加载状态。
- 错误：若用户列表查询失败，显示可重试的错误提示。
- 权限拒绝：非管理员用户看到的是访问被拒绝的提示，而非用户列表。

## 待解决问题

- 无阻塞首版切片的问题。

## 验收标准

- [ ] 管理员可打开用户列表页面
- [ ] 可按姓名或邮箱进行搜索过滤
- [ ] 管理员可禁用某个启用的用户
- [ ] 被禁用的用户无法登录
- [ ] 非管理员无法访问该页面
```

## 3. 负责人文档更新

目标文件：

- `docs/design/app-overview.md`

示例更新：

```md
## Main Surfaces

- User Management: admin-only surface for listing, searching, and disabling users.

## Roles

- Admin: can access User Management and disable active users.
- Non-admin: cannot access User Management.
```

## 4. 待办事项条目

目标文件：

- `docs/backlog/README.md`

示例行：

```md
| P0 | User Management first slice | `docs/requirements/2026-05-21-user-management.md` | `docs/design/app-overview.md` | `docs/plans/2026-05-21-user-management-plan.md` | `ready` | `plan-first` | `none` |
```

由于此切片变更了授权可见的管理员行为，并涉及页面、API、权限和测试，因此它是 `plan-first`，需要独立的计划和结项审计。

## 5. 计划

目标文件：

- `docs/plans/2026-05-21-user-management-plan.md`

```md
# User Management Plan

> Plan Status: planned
> Last Reviewed: 2026-05-21
> Source: `docs/requirements/2026-05-21-user-management.md`
> Audit: required

## Current Baseline

- app has authentication
- app has admin role checks
- no user management page exists yet

## Goals

- land the first supported user list/search/disable slice

## Non-Goals

- user creation
- profile editing
- bulk actions

## Task Route

- Type: `implementation-only change`
- Owner Docs: `docs/design/app-overview.md`
- Skill Selection Basis: `plan-audit-prompt.md` and `closure-audit-prompt.md` apply as review methods; delivery phase uses `Skill: none`

## Infrastructure And Config Prereqs

- No infra prereqs beyond existing baseline

## Execution Plan

### Phase 1 - Land The Core Slice

Status: planned
Targets: `apps/...`, `packages/...`, `docs/...`
Skill: `none`

- Item Types: `Add | Proof`
- Prereqs: none

- [ ] add user list route/page
  - Skill: `none`
- [ ] wire search behavior
  - Skill: `none`
- [ ] add disable action
  - Skill: `none`
- [ ] enforce admin access
  - Skill: `none`
- [ ] add tests for search, disable, and non-admin access
  - Skill: `none`

Exit Criteria:

- [ ] user list/search/disable behavior lands for admins
- [ ] affected owner docs updated or `No owner-doc update required`
- [ ] `docs/logs/` updated

## Plan Audit

- Status: pending
- Reviewer / Agent: `<independent reviewer or subagent>`
- Evidence: `<audit file or task id>`

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

None.

## Closure

Status Note: complete only after plan and closure audits both pass.

Closure Audit Evidence:

- Reviewer / Agent: `<independent reviewer or subagent>`
- Evidence: `<task id / log link / audit file>`

Follow-up:

- none
```

## 6. 日志条目

目标文件：

- `docs/logs/2026/05-21.md`

```md
# Development Log - 2026-05-21

### 2026-05-21

- Implemented first User Management slice from `docs/requirements/2026-05-21-user-management.md`.
- Added admin-only user list, name/email search, and disable action.
- Updated `docs/design/app-overview.md` with the supported User Management surface.
- Verification: `<real test command>` passed for user list/search/disable and non-admin access.
```

## 7. 结项审计说明

此切片已制定计划，因此在计划标记为完成之前需要进行结项审计。

若审计内容复杂、存在争议或对未来会话有用，请使用单独的审计文件。否则，将独立审查者/子代理的证据记录在计划和每日日志中。
