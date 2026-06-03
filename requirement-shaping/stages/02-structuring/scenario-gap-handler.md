# Scenario Gap Handler

Use this when Structuring reveals a missing scenario, branch, rule, status, permission, or page state.

The goal is to keep Structuring responsible for structural completeness without reopening Discovery unnecessarily.

## Gap Classification

| Gap Type | Meaning | Action |
| --- | --- | --- |
| In-boundary structural gap | Missing detail inside the accepted requirement boundary | Stay in Structuring and add it to flow, state, permission, rules, or prototype |
| Out-of-scope scenario | Valuable scenario outside the accepted boundary | Record as out of scope or future phase |
| Direction-changing gap | New information changes goal, core user, core scenario, or main boundary | Pause Structuring and route back to Discovery Conversation |

## Handling Flow

```text
发现遗漏场景
↓
判断是否在已接受边界内
↓
边界内：补入结构设计
边界外：记录 out of scope / later
改变方向：退回 Discovery
```

## Structuring Gaps

Keep these in Structuring:

- Rejection, cancellation, timeout, rollback, retry.
- Sync failure, duplicate submission, missing data, validation failure.
- Status mapping, terminal state, abnormal state.
- Role action, data visibility, override authority.
- Empty, loading, error, no-permission, disabled, archived states.

## Discovery Regression Triggers

Return to Discovery only when the gap changes:

- Requirement goal.
- Core user.
- Core scenario.
- Main boundary.
- MVP / blueprint direction.

## Output Template

```markdown
| 遗漏场景 | 分类 | 处理方式 | 进入哪个结构 |
| --- | --- | --- | --- |
```
