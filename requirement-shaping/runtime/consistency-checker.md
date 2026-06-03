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
- Scenario gaps that were found but not classified as in-boundary, out-of-scope, or direction-changing.
- Direction-changing gaps that were handled inside Structuring instead of being routed back to Discovery.

If issues exist, list them under `一致性检查结果` and recommend whether to continue, assume, or return to a prior stage.
