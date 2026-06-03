# Stage Transition Gates

## Discovery to Structuring

Allowed when:

- Decision readiness is High.
- Requirement goal is clear.
- Core user is clear.
- Core scenario is clear.
- Main boundary is clear.
- Remaining unknowns are listed and do not change the requirement direction.

If readiness is Low or Medium, continue Discovery Conversation instead of producing a final Requirement Brief.

## Structuring Regression to Discovery

Return to Discovery only when a newly discovered gap changes one of these:

- Requirement goal.
- Core user.
- Core scenario.
- Main boundary.
- MVP / blueprint direction.

If the gap only affects flow branch, status, permission, page state, exception handling, or rule detail, keep it in Structuring and handle it with `stages/02-structuring/scenario-gap-handler.md`.

## Structuring to Handoff

Allowed when:

- Scope is explicit.
- Main flow and exception branches are captured.
- State machine and permission needs are decided.
- Prototype/page implications are summarized.
- Scenario gaps are classified as in-boundary, out-of-scope, or direction-changing.
- Open questions are impact-rated.

## Handoff to Write PRD

Allowed when:

- User asks to write a PRD, or accepts the handoff package as ready.
- Missing information is visible.
- Assumptions are not mixed with confirmed decisions.
