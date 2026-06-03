# Open Question Extractor

Extract unresolved questions before PRD handoff.

## Classification

| Level | Meaning | PRD Handling |
| --- | --- | --- |
| Regression / 回退 | Changes accepted goal or core user, or invalidates the accepted baseline | Do not hand off; ask for explicit confirmation before resetting downstream IR |
| Backtrack / 回溯 | Needs a focused Discovery-style sub-question without changing accepted goal or core user | Do not hand off until the Backtrack patch is absorbed, listed as open question, marked out of scope, or escalated |
| Blocking structural | Unresolved in-boundary gap that changes flow, state, permission, page structure, prototype, or acceptance | Confirm before final PRD or mark explicit assumption |
| Important | Affects rules, copy, fields, acceptance, or system integration without changing the accepted boundary | Include in PRD待确认事项 |
| Out of scope | Valuable scenario outside the accepted boundary | Record as future phase / 暂不包含 |
| Minor | Does not block core design | Track as follow-up |

## Scenario Gap Handling

- Regression candidates must be resolved before Handoff IR is finalized.
- Backtrack patches must be handled before Handoff IR is finalized.
- Unresolved in-boundary structural gaps may be handed off only with explicit PRD handling.
- Out-of-scope scenarios should not expand the PRD scope silently.

## Output Template

```markdown
| 问题 | 分类 | 影响 | 建议确认对象 | PRD 处理方式 |
| --- | --- | --- | --- | --- |
```
