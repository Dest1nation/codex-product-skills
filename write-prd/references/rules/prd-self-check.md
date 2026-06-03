# PRD Self-Check

Use this rule after rendering a PRD and before final output. The self-check is an internal quality gate: it improves the final PRD but is not shown to the user by default.

## When to Run

Run the self-check after the PRD has been rendered from the generation plan.

Use it for:

- New PRDs generated from a PRD input package or prepared product design materials
- Material revisions to an existing PRD
- PRD reviews where the user asks to improve the generated document

Do not use it to reopen requirement discovery. If product input is missing, repair by making explicit assumptions or adding "待确认事项"; only ask the user when a missing decision blocks scope, page structure, state flow, permissions, data rules, or acceptance criteria.

## Self-Check Checklist

### 1. Template Module Completeness

Check that every section selected by the generation plan appears in the PRD.

Required checks:

- Planned document metadata is present when the output is a formal PRD.
- Planned overview, scope, and out-of-scope boundaries are rendered.
- Planned system flow, state machine, page details, permissions, non-functional requirements, acceptance criteria, and open questions are present.
- Omitted sections are not accidentally reintroduced unless the plan is revised.

### 2. Plan Adherence

Check that the PRD follows the generation plan instead of re-deciding structure during prose writing.

Required checks:

- No unplanned scenario module, diagram type, permission matrix, status-action mapping, or broad section was added during rendering.
- No planned artifact was skipped.
- Rule ownership follows the plan and module ownership rules.
- Acceptance criteria verify planned behavior instead of restating full rules.

### 3. Status and State Machine

Check whether business statuses are fully represented.

Required checks:

- If statuses affect page display, labels, filters, row actions, permissions, risk counts, scheduled scans, notifications, downstream results, or business decisions, the PRD includes a `stateDiagram-v2`.
- If statuses are computed from dates, records, risk rules, scheduled scans, or upstream data, the PRD includes a lightweight state machine plus a status calculation/priority table.
- Status-action visibility is present when operations vary by status.
- Status priority, recalculation triggers, terminal states, rollback, and exception paths are either specified or listed under "待确认事项".

### 4. System Flow

Check whether system processing is visible enough for implementation.

Required checks:

- If the requirement includes sync, scheduled jobs, notifications, permission checks, status recalculation, data writes, upstream/downstream interaction, retries, or logs, include a system flow.
- System flow should show trigger, permission or field validation, business rule validation, data read/write, status or metric recalculation, external-system handling, and success/failure outcome when applicable.
- Backend interaction timing details should remain in technical design unless the user explicitly requested them in the PRD.

### 5. Scope and Dependency Consistency

Check for contradictions between scope, out-of-scope, involved systems, data dependencies, and open questions.

Required checks:

- If a dependency says sync, push, pull, receive, notify, or write-back, the scope must say whether that capability is in scope.
- If a capability is out of scope, related dependencies should be described as future, external, or "待确认" instead of implementation commitments.
- If historical data, import/export, attachment handling, or downstream recognition affects launch correctness, include the relevant non-functional or data rule.

### 6. Page and Operation Implementability

Check whether page-level behavior is actionable.

For each page or drawer, confirm:

- Page goal and entry are clear.
- Tabs, filters, list fields, and row actions are specified when planned.
- Page-level operations have a concrete page form such as drawer, modal, new page, or inline area.

For each operation, confirm:

- Entry point
- Actor or role
- Preconditions
- Fields and controls
- Required/optional rules
- Validation
- Success feedback
- Failure feedback
- Data or status impact
- Permission behavior

Avoid unresolved implementation choices in the PRD body, such as "drawer or page", "depending on actual implementation", or "recommended but optional". Move unresolved choices to "待确认事项".

### 7. Permission Coverage

Check whether permissions cover every visible surface that changes access.

Required checks:

- Menu permission exists when a new menu is created.
- Button/action permissions exist for sensitive operations.
- Data permissions define list-page visibility and filtering rules when applicable.
- Detail-page entry is controlled by button/action permissions; detail field display and business explanations belong to page details, not data permissions.
- No-permission behavior is specified as hidden, disabled, blocked, empty state, or no-permission page.
- Permission changes after page load are handled when they materially affect save or submit behavior.
- Permission sections should describe permission-system configuration points: menu permissions, button/function permissions, and list-page data permissions.
- If the permission section is written as a role responsibility table, such as "HR can initiate" or "Finance can reject", move those business rules to user analysis, state-action mapping, or page operation details.

### 7.1 Multi-Terminal and Non-Functional Placement

Check whether terminal-specific pages and non-functional requirements are placed under the correct owner.

Required checks:

- If the input explicitly mentions PC, mobile, employee portal, mini program, or another terminal with distinct users, entries, page goals, display, or operation differences, the functional details section includes the corresponding page or page subsection.
- Mobile, employee-side, mini-program, or other terminal-specific functional pages are not placed in non-functional requirements.
- Enterprise WeChat, SMS, email, or other notification capabilities are placed under system dependencies, functional rules, or acceptance criteria, not non-functional requirements.
- Business-caliber questions, data-source questions, and notification-node questions are placed under "待确认事项", not non-functional requirements.
- Non-functional requirements are activated only for historical data handling, data snapshots, audit, compliance, launch initialization, or similar extra development/launch handling beyond the core business flow.
- If non-functional requirements contain no historical data, snapshot, audit, compliance, or launch-initialization content and only restate functional behavior, remove or relocate the section.

### 8. Acceptance Coverage

Check whether acceptance criteria cover implementation-critical behavior.

Acceptance criteria should include:

- Core happy path for each activated page or operation.
- Required validation rules.
- Required status transitions or computed status outcomes.
- Permission behavior.
- Integration, scheduled job, notification, retry, or failure behavior when planned.
- Material edge cases from the generation plan.

Acceptance criteria should be concise verification points, not duplicated business-rule prose.

### 9. Open Question Closure

Check that unresolved decisions in the PRD body are captured under "待确认事项".

Required checks:

- Every "待确认", "待业务确认", "字段待确认", or unresolved option in the body has a matching open question.
- Each open question includes impact and suggested owner or confirmation object when possible.
- Open questions do not hide decisions that are necessary for the current PRD to be implementable.

### 10. Anti-Duplication

Check that each rule has one primary owner.

Required checks:

- State machine owns status transitions and lifecycle.
- Page or operation details own fields, validation, feedback, and local edge cases.
- Permissions own visibility and access.
- Data/system dependencies own sync, retry, reconciliation, logs, and external interactions.
- Acceptance criteria verify behavior without re-explaining the full rules.

When a rule appears in multiple sections, keep the owning section detailed and make other mentions short references.

### 11. Human Readability

Check whether the PRD can be comfortably read by product, business, design, development, and testing reviewers.

Required checks:

- Language is concrete, business-readable, and implementation-oriented.
- Sentences are not overly long, nested, or abstract.
- AI-like filler, generic optimization language, and unexplained technical terms are removed or rewritten.
- Technical terms are used only when they help implementation; otherwise rewrite them into business-facing effect descriptions.
- Tables are not overloaded with dense prose that should be split into shorter rows or focused explanations.
- Mermaid node labels are short and readable; detailed rules remain in tables.
- Acceptance criteria are observable and easy to verify, not broad slogans.

If readability is low, polish the PRD before final output without changing the requirement meaning, business rules, scope, or planned structure.

## Repair Rules

Use these repair rules before final output.

Self-check repairs must follow the generation plan. If a repair requires an unplanned module, section, diagram, permission matrix, state machine, status-action mapping, or table, return to the planning layer first, revise the generation plan, and then re-render the affected sections. Do not insert unplanned structural content directly into the PRD body.

| Finding Type | Repair Action |
| --- | --- |
| Small omission | Patch the PRD directly, such as adding a missing feedback rule, validation note, or acceptance criterion |
| Structural gap | Return to the planning layer, revise the generation plan, and re-render the affected PRD sections |
| Business undecided | Do not invent the decision; add it to "待确认事项" with impact and owner |
| Conflict between sections | Resolve by source priority or list as "待确认事项" if unresolved |
| Duplicate rule | Keep the primary owner section detailed and shorten or remove duplicate copies elsewhere |
| Unplanned module needed | Revise the generation plan first, then render the module |
| Low readability | Rewrite dense, AI-like, or technical-heavy wording into clearer business-readable language without changing meaning |

## Do Not Output by Default

Do not show the self-check checklist, pass/fail notes, or repair log in the final answer unless the user explicitly asks for the self-check result.

The final answer should be the corrected PRD or requested PRD section.

If the user asks for a review instead of a revised PRD, present findings first and order them by severity.

## Common Failure Patterns

Use these examples to catch common PRD quality issues:

| Failure Pattern | Self-Check Response |
| --- | --- |
| Status rules exist, but no state machine | Add a state machine or lightweight state machine if the status affects display, actions, notifications, risk, or downstream results |
| Scheduled notification exists, but no system flow | Add a system flow showing scan trigger, recipient resolution, send action, success/failure logging, and landing behavior |
| Dependency implies sync, but scope omits sync | Clarify scope or add an open question |
| Operation says "drawer or page" | Choose the planned page form or move the unresolved choice to "待确认事项" |
| Acceptance criteria only cover happy path | Add validation, permission, status, integration, and planned edge-case checks |
| Permission section only says "by permission system" | Specify menu, button/action, data, detail, attachment/export, and no-permission behavior as applicable |
| Same rule is repeated in scope, function list, page details, and acceptance | Keep detail under the primary owner and shorten repeated mentions |
| Output reads like AI-generated filler | Replace generic phrases with concrete business effects, measurable rules, and reviewer-friendly wording |
| Technical terms overwhelm business readers | Explain the user-visible effect or move technical detail to "待确认事项" / technical design when not required in the PRD |
