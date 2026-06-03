# IR Evolution Rules

## Discovery IR to Structured IR

Move only when the user has reached decision readiness. Discovery is a thinking facilitation stage, not an information collection stage.

Required signals:

- The user can state the requirement goal in their own words.
- Core user is explicit.
- Core scenario is explicit.
- Main boundary is explicit enough to discuss scope.
- Remaining unknowns are gap-filling, not direction-forming.

If these signals are missing, continue Discovery Conversation:

- Ask a focused question.
- Reflect contradictions.
- Challenge assumptions.
- Help the user compare options.
- Check what is still unclear before summarizing.

## Structured IR to Handoff IR

Move only when the product structure is complete enough for PRD writing or the user explicitly asks to package current progress.

Required signals:

- Scope, roles, flows, and key rules are captured.
- State machine need is decided.
- Permission impact is captured or ruled out.
- Prototype/page implications are clear.

## Regression

If new information invalidates a later-stage decision, move back to the earliest affected IR state and record the change in `memory/decision-log.md`.
