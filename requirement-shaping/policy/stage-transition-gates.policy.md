# Stage Transition Gates

Use this file only when a task needs detailed transition review. Core transition rules live in `SKILL.md`.

## Discovery to Structuring

Allowed when:

- Decision readiness is High.
- Requirement goal is clear.
- Core user is clear.
- Core scenario is clear.
- Main boundary is clear.
- Remaining unknowns are listed and do not change the requirement direction.

If readiness is Low or Medium, continue Discovery Conversation unless the user explicitly asks to move forward with a partial boundary. For partial movement, mark assumptions and open questions before entering Structuring.

## Structuring Gap Response

When Structuring reveals new information, classify it before changing stages.

| Type | Trigger | Action | Reset Downstream IR |
| --- | --- | --- | --- |
| Structural Gap | Missing flow, state, permission, page, rule, validation, exception, retry, rollback, or page state inside the accepted boundary | Stay in Structuring and update the relevant structure | No |
| Backtrack / 回溯 | New information needs a focused Discovery-style sub-question but does not change accepted goal or core user | Ask one focused sub-question, then return to Structuring with a patch | No |
| Regression / 回退 | New information changes accepted goal or core user, or invalidates the accepted baseline | Ask for explicit confirmation; reset Structured/Handoff IR only after confirmation | Yes, after confirmation |

Scenario and boundary changes require impact classification:

- New branch or boundary detail within the same goal: Structural Gap or Backtrack.
- MVP / blueprint / main-boundary direction changes: Regression candidate.
- Accepted goal or core user changes: Regression.

## Backtrack Patch Gate

Backtrack is not a stage reset. Each Backtrack must produce a patch:

- New fact or clarification.
- Baseline that remains unchanged.
- Affected flow, state, permission, page, rule, prototype, or handoff section.
- Handling: update structure, add open question, mark out of scope, or escalate to Regression.

Unresolved Backtrack patches cannot move to Handoff.

## Structuring to Handoff

Allowed when:

- Scope is explicit.
- Main flow and exception branches are captured.
- State machine and permission needs are decided or listed as impact-rated open questions.
- Prototype/page implications are summarized.
- Structural gaps are completed, assumed, out of scope, or recorded as open questions with PRD handling.
- Backtrack patches are handled.
- Regression candidates are confirmed, dismissed, or resolved.

## Handoff to Write PRD

Allowed when:

- User asks to write a PRD, or accepts the handoff package as ready.
- Missing information is visible.
- Assumptions are not mixed with confirmed decisions.
- No unresolved Regression candidate remains.
