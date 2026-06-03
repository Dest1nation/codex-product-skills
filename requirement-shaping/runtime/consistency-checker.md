# Consistency Checker

Run before finalizing a structured artifact or handoff package.

Check for:

- Scope conflicts with scenarios.
- Flow steps missing actors or systems.
- Statuses without triggers, actions, or terminal handling.
- Actions that lack permission rules.
- Prototype operations that are not supported by flow or state rules.
- Assumptions presented as confirmed facts.
- Open questions that should block PRD writing.
- Scenario gaps that were found but not classified as Structural Gap, Backtrack, Regression, or out of scope.
- Backtrack patches that were not absorbed into structure, listed as open questions, marked out of scope, or escalated.
- Regression candidates that were handled inside Structuring without explicit user confirmation.
- Direction-changing main-boundary or MVP changes that were not classified as Regression candidates.

If issues exist, list them under `一致性检查结果` and recommend whether to continue, assume, backtrack, regress, or hand off.
