# 索引路由审计提示

当需要审计文档目录的索引结构是否达成其路由目标时，使用此提示。

典型触发场景：

- 新建或重构了文档树
- 现有索引已过时或与所指向的文件不一致
- 代理或人工反复无法通过索引找到正确的文档
- 在将此模板复制到新项目之前，用于验证复制后的索引路由是否仍然正确

## 审计提示

```text
You are auditing the routing effectiveness of a documentation index structure.

## Step 1 — Read the index

Read the top-level index file (e.g. `INDEX.md` or `docs/index.md`) and every sub-index or README that it links to.

For each indexed entry, record:
- the stated purpose or task scenario
- the path it points to
- whether the target file exists and its content roughly matches the stated purpose

Return a coverage table with columns: | entry | stated purpose | target path | exists | matches purpose | notes |

Flag any entry where:
- the target file does not exist
- the target exists but its content does not match the stated purpose
- the stated purpose is vague enough that a reader cannot decide if it is relevant
- multiple entries point to the same target but describe it differently
- an existing document that should be indexed is missing from the index

## Step 2 — Persona-based routing test

For each persona below, simulate a realistic information need, then trace the shortest path from the index to the answer. Record whether the persona succeeds and how many hops it takes.

Persona A — New developer joining the project:
- Need: "How do I set up my dev environment and run the project?"
- Need: "Where is the code for [main feature area]?"

Persona B — AI agent starting a non-trivial task:
- Need: "What are the current rules I must follow before writing code?"
- Need: "Where do I find the owner doc for [technical area]?"

Persona C — Reviewer auditing a completed slice:
- Need: "Where is the plan for the current work and what were its closure gates?"
- Need: "Where are recent implementation logs?"

Persona D — Maintainer updating documentation:
- Need: "What is the rule for when to update the index versus when to add a new document?"
- Need: "Which documents are known to be stale or low-confidence?"

For each persona need, return:
| persona | need | starting point | hops | found | path taken | problem |

If a persona cannot reach the answer through the index alone, record the failure point and what was missing.

## Step 3 — Structural quality checks

Check for:
- orphan files: files in the directory tree that are not reachable from any index entry
- stale references: index entries pointing to moved, renamed, or deleted files
- depth imbalance: paths that require more than 3 hops from the top-level index to reach actionable content
- duplication: the same rule or knowledge stated in multiple indexed files without cross-reference
- category confusion: documents whose content belongs in a different directory than where the index places them
- missing intermediate indexes: directories with more than ~10 files that lack their own README or catalog

## Step 4 — Return findings

Return findings ordered by severity:

For each finding include:
- title
- affected index entry or file path
- current gap
- impact on routing effectiveness
- recommendation

If no findings remain, say that explicitly and note residual risks.
```

## 自定义说明

复制此模板到实际项目后：

- 将角色需求替换为匹配项目领域和常见任务类型的实际问题。
- 添加项目特定的结构规则（例如，最大索引深度、目录文件数超过 N 时需有子索引）。
- 若项目采用分层索引模式（摘要目录 → 分类目录 → 单个文档），增加一项检查，确认每一层的大小和颗粒度是否合适。
- 根据项目实际的文档深度，调整跳数阈值。
