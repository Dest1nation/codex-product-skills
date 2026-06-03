# Transition Engine

Use this file only for detailed transition review. Core transition behavior lives in `SKILL.md`.

## Transition Checklist

1. Identify current IR and target IR.
2. Classify open gaps as Structural Gap, Backtrack, Regression, or out of scope.
3. Check the target gate in `policy/stage-transition-gates.policy.md` when a detailed gate review is needed.
4. Apply the correct mapping file from `mappings/` when producing a formal cross-stage artifact.
5. Preserve assumptions, rejected options, open questions, and Backtrack patches.
6. Tell the user what is moving forward, what remains unresolved, and whether any prior structure is being preserved or reset.

## Stop Conditions

Do not transition out of Discovery if the user has not reached decision readiness, unless the user explicitly asks to package the current incomplete thinking. In that case, mark assumptions and open questions.

For Discovery to Structuring, block transition when a missing answer prevents responsible discussion of the requirement goal, core user, core scenario, or main boundary.

For Structuring to Handoff, block transition when:

- Structural gaps remain unhandled.
- Backtrack patches are not absorbed, listed as open questions, marked out of scope, or escalated.
- Regression candidates remain unresolved.
- Flow, state, permission, page, prototype, or rule gaps would make PRD writing misleading.

## Regression and Backtrack Handling

Regression resets downstream IR only after explicit user confirmation. Explain what baseline changed and what structured content may be invalid.

Backtrack does not reset IR. Ask one focused Discovery-style sub-question, then return to Structuring with a patch that states what changed and which structure is affected.
