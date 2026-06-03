# Stage Router

Use this router at the start of each turn.

## Route to Discovery

Choose Discovery when the user gives an idea, complaint, opportunity, scattered notes, unclear scope, or asks to discuss, explore, clarify, or form a requirement.

Primary files:

- `stages/01-discovery/discovery-controller.md`
- `stages/01-discovery/discovery-conversation.md`
- `stages/01-discovery/requirement-interview.md`
- `stages/01-discovery/hypothesis-builder.md`
- `stages/01-discovery/exploration-tracker.md`
- `stages/01-discovery/decision-readiness-checker.md`
- `stages/01-discovery/discovery-summary.md`

## Route to Structuring

Choose Structuring when the user asks for business flow, system flow, status design, permissions, prototype, page fields, rules, or implementation-oriented product design.

Structuring requires a ready or explicitly accepted partial Discovery Summary. If goal, core user, core scenario, or main boundary is still unclear, route to Discovery even if the user asks for a flow.

Primary files:

- `stages/02-structuring/structuring-controller.md`
- `stages/02-structuring/flow-builder.md`
- `stages/02-structuring/scenario-gap-handler.md`
- `stages/02-structuring/state-machine-designer.md`
- `stages/02-structuring/permission-modeler.md`
- `stages/02-structuring/decision-reducer.md`

## Route to Handoff

Choose Handoff when the user asks to prepare PRD materials, package design outputs, resolve conflicts before PRD, extract open questions, or move to `write-prd`.

Primary files:

- `stages/03-handoff/handoff-controller.md`
- `stages/03-handoff/prd-schema-mapper.md`
- `stages/03-handoff/conflict-resolver.md`
- `stages/03-handoff/open-question-extractor.md`

## Ambiguous Requests

If multiple stages match, use the earliest stage that still contains unresolved risk. State the routing assumption briefly.

Boundary rule: Discovery confirms product boundary. Structuring translates an accepted boundary into flow, state, permission, rule, and page structure. Structuring handles scenario gaps unless they change goal, core user, core scenario, or main boundary.
