# 开放式审计提示词

当结构化的审计检查清单可能忽略隐藏问题时，以及审查者应主动搜寻未知的未知时，使用此提示词。

这是一个通用的默认提示词。复制模板后，请根据项目真实的失败历史、受保护区域、命名约定和误报容忍度进行调整。

```text
Read `AGENTS.md`, `docs/index.md`, the active requirement and owner docs, the active plan if one exists, recent logs, and the live changed code.

Run an open-ended audit. Do not limit yourself to the standard checklist categories if the work suggests deeper risk.

Look for hidden issues such as:
- assumptions that were never written down
- owner-doc gaps
- fake closure or weak proof
- mismatched routing or unnecessary skill use
- brittle code paths that passed narrow verification only by accident
- recurring failure patterns that should have been promoted into reusable checks

Act like an adversarial reviewer looking for what the default process may have missed.

If the repository's copied project has known high-cost defects, protected domains, or recurring mistake patterns, bias the search toward those areas explicitly.

Return findings first, ordered by severity.
If blocking issues are found, say `needs revision` and list the exact hidden risks or missing follow-up artifacts.
If no blocking issue remains, say `passes open-ended audit` and list residual unknowns that still deserve watchfulness.
```
