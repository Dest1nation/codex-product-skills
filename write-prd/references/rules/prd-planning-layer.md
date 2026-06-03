# PRD Planning Layer

Use this rule layer after reading the user's prepared product input and before drafting the final PRD. The planning layer is an internal rule engine: it converts product input into a typed PRD generation plan.

Do not show this plan unless the user asks for planning output. The final answer should normally be the PRD itself.

## Planner-Owned Decisions

These decisions belong to the planner, not the renderer:

- Scenario selection
- Section activation
- Diagram requirements
- Ownership resolution
- Status-action mapping requirements
- Permission matrix requirements
- Edge-case expansion
- Default assumptions
- Acceptance strategy
- Conflict resolution

The renderer must follow these decisions from the generation plan instead of re-deciding them during natural-language drafting.

## Typed Planner Output

Use `references/rules/prd-plan-schema.md` as the planner-to-renderer contract. Populate the schema internally before drafting so the renderer receives a stable, machine-readable plan instead of a prose-only plan.

Use empty arrays for unused optional fields. Do not add ad hoc top-level fields during planning; use intentional schema extension for new top-level needs.

## Accepted Inputs

The planner can consume any of these inputs:

- PRD input package from `product-design-process`
- Requirement input brief
- Business or system flow
- State machine design
- Product prototype specification
- Existing PRD draft
- Clear implementation-ready notes

If the input is a machine-readable package or IR, use it directly. If the input is plain Markdown or conversation notes, normalize it internally into the same fields without requiring the user to rewrite it.

Use the normalized internal requirement model as the primary planning input. Once normalization is complete, avoid re-interpreting raw conversational context unless a conflict, gap, or user correction requires it.

## Source Conflict Resolution

For conflicting product inputs, resolve them in this priority:

1. Finalized requirement brief
2. Approved prototype
3. Existing PRD
4. Supplementary notes

List unresolved conflicts under "待确认事项". Do not silently merge inconsistent rules.

## Internal Requirement Model

Extract only what is present or strongly implied:

| Field | Meaning |
| --- | --- |
| `business_context` | Background, current problem, trigger, goals |
| `users_and_roles` | User roles, scenarios, usage frequency, core goals |
| `scope` | In-scope, out-of-scope, systems, menus, pages |
| `pages` | Page list, page goal, entry, tabs, filters, fields, actions, forms |
| `operations` | Create, edit, submit, approve, import, export, sync, cancel, rollback, download, upload |
| `state_machine` | Business statuses, computed/derived statuses, transitions, triggers, roles, conditions, terminal states |
| `permissions` | Menu, button/action, data visibility, sensitive attachment or export rules |
| `data_rules` | Data source, calculation rules, validation, snapshot, import/export fields, field mapping |
| `integrations` | Upstream/downstream systems, triggers, frequency, retries, reconciliation, logs |
| `non_functional` | Historical data, launch scope, compliance, audit, user-visible performance, acceptance needs |
| `open_questions` | Unknowns or assumptions that materially affect implementation |

Do not invent fields just to fill the model. Missing optional fields should usually result in omitted PRD sections, not extra questions.

## Scenario Selection

Pick one primary scenario and optional secondary scenarios:

| Signal | Scenario |
| --- | --- |
| Mainly query, metrics, cards, filters, export, readonly data | Report / Display |
| User creates, edits, submits, imports, exports, or maintains records | Forms / Operations |
| List page has row-level actions or status-dependent actions | List With Row Actions |
| Statuses affect display, actions, permissions, approval, automation, scheduled checks, risk calculation, notifications, or downstream results | Approval / Lifecycle |
| Cross-system data exchange, scheduled jobs, idempotency, retry, reconciliation, logs | Integration / Sync |
| Main change is menu/button/data/attachment visibility | Permissions Only |
| Multiple signals materially affect implementation | Mixed |

Lifecycle or computed business status affecting actions, permissions, display, risk calculation, scheduled processing, notifications, automation, or downstream processing selects Approval / Lifecycle even when the feature also has list or form pages.

## Planning Activation Rules

Apply these activation rules after building the internal requirement model:

| Condition | Required Planning Decision |
| --- | --- |
| Lifecycle states affect actions, permissions, approvals, automation, or downstream processing | Include a state machine and a status-action mapping |
| Computed or derived business statuses affect page display, risk counts, scheduled scans, reminders, notifications, or downstream results | Include a lightweight state machine and a status calculation/priority table |
| Page behavior varies by business status | Include status Tabs and add "适用状态/Tab" columns to affected filters, list fields, and row actions |
| Integrations include retries, reconciliation, downstream sync, or scheduled processing | Include `系统功能描述 > 数据 / 系统依赖` and specify retry/reconciliation rules |
| Permissions affect visible data scope | Include list-page data permission rules; detail entry is controlled by button permissions and detail display rules belong to page details |
| Operations change lifecycle status | Put lifecycle ownership in the state machine, not in operation summaries |
| Approval flow exists | Include an approval flow diagram and approval operation sections |
| Import has field validation or partial failure handling | Include import operation rules, validation rules, and failure result handling |
| Export has permission, field, range, or async constraints | Include export operation rules with export range, fields, format, permission, and async handling |
| Destructive or irreversible operations exist | Include confirmation, permission, failure handling, and applicable audit/recording rules |
| Historical data affects launch, query, export, approval, or downstream display | Include historical data handling under non-functional requirements |

If multiple conditions apply, activate all relevant modules but keep each rule under its primary owner.

### Lightweight State Machine Rule

Some business statuses are not moved by explicit user approval actions. They may be computed from dates, records, risk rules, scheduled scans, or upstream data. Treat them as lightweight business state machines when the computed status affects implementable behavior.

Include a lightweight state machine when computed statuses affect any of:

- Page labels, badges, tabs, filters, or risk buttons
- Row visibility or list grouping
- Scheduled scans, reminders, or notifications
- Risk counts, priority ordering, or dashboard metrics
- Available operations or validation requirements
- Downstream system recognition or business decisions

Examples:

| Computed Status Pattern | State Machine Shape |
| --- | --- |
| Validity period | 无记录/无效 -> 有效 -> 临期 -> 过期; 新增/更新有效记录 can return to 有效 |
| Inventory/stock risk | 正常 -> 预警 -> 缺货; 补货 can return to 正常 |
| Sync health | 未同步 -> 同步中 -> 同步成功 / 同步失败; 重试 can return to 同步中 |
| Eligibility/risk | 不符合 -> 符合 / 风险; data changes can recalculate the state |

For lightweight state machines, render both:

1. A concise `stateDiagram-v2` showing computed status movement or recalculation paths.
2. A status calculation/priority table carrying formulas, date windows, risk priority, and exception rules.

## Edge-Case Expansion Rules

Expand edge cases during planning when they materially affect implementation, permissions, data correctness, or acceptance.

| Signal | Planned Edge Cases |
| --- | --- |
| Form or operation has validation rules | Required/conditional fields, invalid values, duplicate submissions, save/submit failure |
| Import exists | Empty file, wrong template, field validation failure, partial success, duplicate data, retry after failure |
| Export exists | No data, large result set, permission-filtered data, async timeout, download expiry |
| Approval or lifecycle exists | Rejection, withdrawal, cancellation, timeout, resubmission, terminal states, rollback limits |
| Integration or sync exists | Retry exhaustion, idempotency, downstream failure, reconciliation mismatch, manual correction |
| Permissions affect access | No menu permission, no button permission, no data permission, permission changes after page load |
| Historical data is involved | Missing fields, inconsistent legacy status, migration failure, business confirmation gaps |

Do not add edge cases for every possible failure. Include only cases that change page behavior, business rules, data handling, permissions, or acceptance criteria.

## Section Planning Rules

Start from `references/templates/prd-template.md` as a menu, then keep only useful sections:

| Section | Activation Condition |
| --- | --- |
| 文档信息 | Useful for formal PRD delivery or provided by user |
| 需求整体描述 | Always, unless the user asks for only a partial section |
| 需求分析 | User roles, business attachments, or business flow add implementation decisions |
| 系统功能描述 | System flow, state machine, lifecycle, or functional list clarifies cross-page behavior |
| 功能性需求细节讲解 | Any user-facing page, operation, list, form, import/export, or interaction exists |
| 权限管理 | Menu permissions, button/function permissions, list-page data permissions, or no-permission behavior affect implementation |
| 非功能性需求描述 | Historical data, data snapshot, audit, compliance, or launch initialization requires extra development or business-side handling |
| 验收标准 | Always for implementation-ready PRDs unless the user asks for a draft outline only |
| 待确认事项 | Any assumption or unresolved decision remains |

Omit sections that repeat the same decision without adding implementable detail.

## Module Ownership Rules

Use one primary owner for each decision:

| Decision | Primary Owner |
| --- | --- |
| Delivery boundary | Scope |
| End-to-end cross-page process | Business/system flow |
| Business lifecycle, computed business statuses, and status transitions | State machine |
| Page structure, filters, lists, row actions, form controls, feedback | Page/operation details |
| Multi-terminal pages, mobile pages, employee/user portals, and terminal-specific display or operation rules | Page/operation details |
| Detail-page field display, detail status prompts, and detail business explanations | Page/operation details |
| Validation and business rules tied to an operation | The operation subsection |
| List data visibility | List data permissions |
| Detail-page entry availability | Button permissions |
| Button or action availability | Button permissions or operation rules |
| Export content and range | Export operation |
| Integration timing, mapping, retry, reconciliation | 系统功能描述 > 数据 / 系统依赖 |
| Verification | Acceptance criteria |
| Unresolved choices | 待确认事项 |

For rules that fit multiple places, put each rule closest to the page, operation, or system behavior the implementer will build.

## Permission and Non-Functional Boundaries

When permissions are managed by a unified permission system, render the permission section as configuration points, not role responsibility prose:

- Menu permissions: which menus, pages, or terminal entries need permission control.
- Button/function permissions: which page buttons or function points need permission control, including export, attachment, or other sensitive actions, and their no-permission behavior.
- List-page data permissions: how list data is filtered, such as by the logged-in account's organization or data permission scope.
- Do not render Personas as a role-permission responsibility table. Business actions and responsibility rules belong in user analysis, state-action mappings, or page operation details.
- Do not describe detail-page data visibility as data permission rules. Detail entry is controlled by button/function permissions; detail field display and business explanations belong in page details.

For multi-terminal scenarios, if the input explicitly mentions PC, mobile, employee portal, mini program, or another terminal with a distinct user, entry, page goal, display, or operation difference, plan a separate page or page subsection in functional details. Do not place terminal-specific features in non-functional requirements.

Use non-functional requirements only for development or launch work beyond the core business flow, such as historical data handling, data snapshots, audit, compliance, and launch initialization. Do not put mobile pages, notifications, business-caliber open questions, button rules, or page display rules in non-functional requirements.

## Anti-Duplication Rules

Avoid repeating the same business rule across:

- State machine
- Operation details
- Permissions
- Acceptance criteria
- Summary tables

For rules already present under their primary owner section:

- Reference the rule instead of redefining it.
- Extend the rule only where the new section adds implementation detail.
- Keep acceptance criteria focused on verification, not restating full business logic.
- Prefer local ownership over repeated global summaries.

For readability-required repeated statements, keep them short and point back to the owning section.

## Default Behavioral Assumptions

Unless the product input says otherwise:

- Lists support pagination.
- Export follows current filter conditions.
- Destructive actions require confirmation.
- Successful operations show feedback messages.
- Failed operations preserve user input when possible.
- Permission-denied actions are hidden rather than disabled.
- Empty lists display empty-state messaging.

Use these defaults to avoid unnecessary clarification. Record a default under "待确认事项" only for material effects on scope, risk, compliance, permissions, or acceptance.

## Acceptance Strategy

Plan acceptance criteria after scenario selection, section activation, and edge-case expansion.

Acceptance criteria should verify:

- Core happy path for each activated scenario.
- Required lifecycle transitions and status-action visibility.
- Permission behavior for applicable menu, button/action, data scope, export, and sensitive attachments.
- Applicable validation, import/export, integration, retry, reconciliation, or historical data rules.
- Planned edge cases that materially affect implementation.
- Open assumptions that need product or business confirmation before launch.

Do not copy full business rules into acceptance criteria. Acceptance criteria should be concise, observable checks that point back to the owning section as needed.

## Diagram and Table Plan

Use diagrams and tables for added structure only:

| Artifact | Include When |
| --- | --- |
| Business/system flowchart | Multi-step, multi-role, cross-system, branching, async, or exception-heavy flow |
| State machine | Business statuses affect operations, display, permissions, approval, automation, scheduled checks, notifications, risk calculation, or downstream results |
| Status-action table | Row actions or operation visibility varies by status |
| Filter/list field tables | A page has query or list behavior |
| Control/rule table | An operation has fields, buttons, validation, or feedback |
| Permission matrix | Menu, button, data, attachment, export, or sensitive action permissions matter |
| Data contract/table | Integration, import/export, sync, calculation, or data source rules matter |
| Acceptance criteria table | Implementation or launch verification is needed |

Read `references/rules/mermaid-diagrams.md` before drafting diagrams.

## Generation Plan Output

The generation plan is the typed contract between the planner and the PRD renderer. It should decide structure and ownership before drafting begins.

The plan should contain:

- Selected PRD scenario and secondary scenarios.
- Included and omitted sections.
- Primary owner for each major rule or decision.
- Required diagrams and tables.
- Planned edge cases.
- Defaults applied from `Default Behavioral Assumptions`.
- Acceptance strategy.
- Source conflicts and unresolved assumptions.

Renderer discovery of a missing structural decision requires returning to this planning layer and updating the plan before continuing. Do not patch structure ad hoc during rendering.

On explicit plan display requests, show the typed schema instance first. Add short explanatory notes as needed.

```yaml
scenario: ""
secondary_scenarios: []
sections:
  included: []
  omitted: []
ownership: []
artifacts:
  diagrams: []
  tables: []
edge_cases: []
defaults: []
acceptance_strategy: []
conflicts: []
open_questions: []
```

Without an explicit plan display request, apply it silently and produce the PRD.
