# Scenario Gap Handler

Use this when Structuring reveals a missing scenario, branch, rule, status, permission, page state, or new information.

The goal is to keep Structuring responsible for structural completeness while allowing focused exploration without resetting accepted structure.

## Gap Classification

| Gap Type | Meaning | Action |
| --- | --- | --- |
| Structural Gap | Missing detail inside the accepted requirement boundary | Stay in Structuring and add it to flow, state, permission, rules, prototype, or open questions |
| Backtrack / 回溯 | New information needs a focused Discovery-style sub-question but does not change accepted goal or core user | Ask one focused question, preserve Structured IR, then return with a Backtrack patch |
| Regression / 回退 | New information changes accepted goal or core user, or invalidates the accepted baseline | Pause Structuring, explain impact, and ask for explicit confirmation before resetting downstream IR |
| Out-of-scope Scenario | Valuable scenario outside the accepted boundary | Record as out of scope or future phase |

## Handling Flow

```text
发现遗漏场景或新信息
↓
判断是否改变核心目标或核心用户
↓
是：回退候选，需明确确认后重置后续 IR
否：判断是否只是结构细节
↓
结构细节：留在 Structuring 补结构
需要补问但不改目标/用户：回溯，问一个 Discovery-style 子问题并产出补丁
超出边界：记录 out of scope / later
```

## Structuring Gaps

Keep these in Structuring:

- Rejection, cancellation, timeout, rollback, retry.
- Sync failure, duplicate submission, missing data, validation failure.
- Status mapping, terminal state, abnormal state.
- Role action, data visibility, override authority.
- Empty, loading, error, no-permission, disabled, archived states.
- Page entry, row action, operation feedback, and rule placement.

## Backtrack Triggers

Use Backtrack when the new information needs product clarification but does not change accepted goal or core user:

- New scenario branch may or may not be in version one.
- New role appears as an affected or secondary participant.
- Boundary detail needs clarification but the main direction remains stable.
- A business exception needs the user to decide whether it is in scope, out of scope, or a PRD open question.

Backtrack must ask one focused question and then produce:

```markdown
## 回溯补丁
- 新增事实 / 澄清：
- 不改变的基线：
- 影响模块：
- 处理方式：更新结构 / 列为待确认 / 标记 out of scope / 升级为回退
```

## Regression Triggers

Use Regression only when the accepted baseline is no longer valid:

- Requirement goal changes.
- Core user changes.
- MVP / blueprint direction changes.
- Main boundary changes enough to invalidate current structure.

Regression requires explicit user confirmation before downstream IR is reset.

## Output Template

```markdown
| 遗漏场景 / 新信息 | 分类 | 处理方式 | 影响模块 |
| --- | --- | --- | --- |
```
