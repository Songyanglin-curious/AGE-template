# 需求缺口回溯提示

在实施之后，当原始需求或原型无法完全覆盖实际交付需求时，请使用此提示。

```text
Read the original source files under `docs/input/`, the relevant `docs/discussions/`, the final requirement files, the related design docs, the implementation plan, and the landed code/logs.

Analyze why the original requirement baseline failed to fully cover the final implementation reality.

Focus on:
- which source inputs were incomplete
- which assumptions remained implicit too long
- where prototype fidelity was mistaken for requirement completeness
- where PM-to-implementation handoff lacked intermediate analysis
- what should move earlier into requirement synthesis or design
- what reusable skill, audit rule, or workflow change should be created

Produce a retrospective-ready analysis with:
- summary
- root causes
- missed signals
- process improvements
- candidate reusable skills or audit prompts
```
