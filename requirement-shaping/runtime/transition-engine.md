# Transition Engine

Use this before moving between stages.

## Transition Checklist

1. Identify current IR and target IR.
2. Check the target gate in `policy/stage-transition-gates.policy.md`.
3. Apply the correct mapping file from `mappings/`.
4. Preserve assumptions, rejected options, and open questions.
5. Tell the user what is moving forward and what remains unresolved.

## Stop Conditions

Do not transition out of Discovery if the user has not reached decision readiness, unless the user explicitly asks to package the current incomplete thinking.

For Discovery to Structuring, block transition only when a missing answer changes the requirement goal, core user, core scenario, or main boundary. Missing flow, state, permission, page, or prototype details should move into Structuring as structural gaps.

For Structuring to Handoff, block transition when flow, state, permission, page, prototype, or rule gaps remain unhandled. A gap is handled only when it is completed, explicitly assumed, classified as out of scope, or recorded as an unresolved in-boundary scenario gap with PRD handling.

Direction-changing gaps must not move to Handoff. Route them back to Discovery Conversation.
