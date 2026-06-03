# PRD Plan Schema

Use this schema as the typed contract between the planner and the PRD renderer.

The planner should populate this structure internally before drafting. Show it to the user only on explicit plan requests.

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

## Field Rules

| Field | Type | Required | Description |
| --- | --- | --- | --- |
| `scenario` | string | Yes | Primary PRD scenario selected by the planner |
| `secondary_scenarios` | string[] | No | Additional scenario modules that materially affect the PRD |
| `sections.included` | object[] | Yes | Sections selected for rendering |
| `sections.omitted` | object[] | No | Sections intentionally omitted and why |
| `ownership` | object[] | Yes | Primary owner for each major rule or decision |
| `artifacts.diagrams` | object[] | No | Planned diagrams and their owning sections |
| `artifacts.tables` | object[] | No | Planned tables and their owning sections |
| `edge_cases` | object[] | No | Planned edge cases that affect implementation or acceptance |
| `defaults` | object[] | No | Default assumptions applied by the planner |
| `acceptance_strategy` | object[] | Yes | Planned acceptance checks by scenario or module |
| `conflicts` | object[] | No | Source conflicts and selected resolution |
| `open_questions` | object[] | No | Unresolved decisions to render under "待确认事项" |

## Object Shapes

Use these object shapes for stable planning.

```yaml
sections:
  included:
    - id: ""
      title: ""
      reason: ""
      source_fields: []
  omitted:
    - id: ""
      title: ""
      reason: ""

ownership:
  - decision: ""
    owner_section: ""
    source_fields: []

artifacts:
  diagrams:
    - type: "flowchart | stateDiagram-v2 | other"
      owner_section: ""
      purpose: ""
      source_fields: []
  tables:
    - type: "filters | list_fields | row_actions | controls | permissions | status_actions | data_contract | acceptance | open_questions | other"
      owner_section: ""
      purpose: ""
      source_fields: []

edge_cases:
  - case: ""
    owner_section: ""
    handling: ""
    acceptance_needed: true

defaults:
  - assumption: ""
    applies_to: ""
    render_as_open_question: false

acceptance_strategy:
  - item: ""
    verifies: ""
    owner_section: ""
    method: "product review | test case | data check | permission check | integration check | other"

conflicts:
  - conflict: ""
    sources: []
    resolution: ""
    render_as_open_question: true

open_questions:
  - question: ""
    impact: ""
    owner: ""
```

## Stability Rules

- Use stable section ids such as `doc_info`, `overview`, `analysis`, `system_functions`, `functional_details`, `permissions`, `non_functional`, `acceptance`, and `open_questions`.
- Keep values concise and deterministic.
- Do not include raw conversational transcript.
- Prefer source field names from the internal requirement model over long prose.
- Use empty arrays instead of omitting top-level fields.
- Do not add ad hoc top-level fields unless the planner explicitly needs an extension.
