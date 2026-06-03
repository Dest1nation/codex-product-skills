# Decision Reducer

Use this when implementation options, rule designs, flow treatments, state treatments, permission treatments, or prototype treatments compete inside the accepted requirement boundary.

Do not use this to decide product direction or requirement scope. If a competing option changes the goal, core user, core scenario, or main boundary, send it to `scenario-gap-handler.md` as a possible direction-changing gap.

## Reduction Criteria

- Business value
- Implementation cost
- Time to validate
- Risk and reversibility
- Impact on flows, states, permissions, and pages
- Fit with the accepted boundary

## Output Template

```markdown
| 选项 | 价值 | 成本 | 风险 | 影响范围 | 建议 |
| --- | --- | --- | --- | --- | --- |
```

Record the chosen path in `memory/decision-log.md` when the decision is important.
