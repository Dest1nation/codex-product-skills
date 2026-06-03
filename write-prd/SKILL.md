---
name: write-prd
description: "Create, refine, review, or template structured Chinese PRDs from clear product inputs, especially a PRD input package, finalized requirement brief, product prototype, business/system flow, state machine, or implementation-ready requirement notes. Use for 中文产品需求文档、PRD、需求说明书、页面字段说明、筛选/列表/表单/导出设计、权限方案、状态流转、系统流程、业务规则、数据口径、接口同步、非功能性需求, or when turning prepared product design materials into implementation-ready PRDs."
---

# Write PRD

## Core Workflow

1. First identify the input maturity: PRD input package, finalized requirement brief, product prototype, business/system flow, state machine, existing PRD draft, or clear implementation notes.
2. If the user provides only a vague idea or asks to discuss/collect/organize the requirement first, do not run a full discovery process inside this skill. Recommend using `product-design-process` to produce a PRD input package before drafting.
3. When a PRD input package or prepared product design materials are provided, treat them as the source of truth. Check completeness and normalize the input into a concise internal requirement model before drafting.
4. Run the planning layer in `references/rules/prd-planning-layer.md` before writing the PRD. Use it to produce a PRD generation plan: scenario, section plan, module ownership, required diagrams/tables, defaults, conflicts, and unresolved assumptions.
5. Clarify only blocking unknowns that change PRD scope, page structure, state flow, permissions, data rules, or acceptance criteria. For proceed-without-confirmation requests, make reasonable assumptions and list them under "待确认事项".
6. Use `references/templates/prd-template.md` as the rendering template. Include only sections selected by the plan or needed for user-requested partial output.
7. Render the PRD from the generation plan. Do not re-decide structure, add broad new modules, or move rule ownership while drafting; if a structural issue appears, revise the plan first.
8. Run the internal PRD self-check in `references/rules/prd-self-check.md` after rendering. Fix detected gaps before final output. Do not show the self-check report by default.
9. Repair gaps found by self-check. Small omissions can be fixed directly; structural gaps must return to the planning layer and revise the generation plan before re-rendering.
10. Structure the PRD around a single functional source of truth: page/scenario details carry implementable behavior, operation rules, field rules, list behavior, validation, feedback, and planned edge cases.
11. Produce Chinese PRDs by default. Preserve useful user-provided terminology when refining an existing PRD.

## Planning Layer

Before drafting or materially revising a PRD, derive a brief PRD generation plan from the available product input. Do this internally unless the user asks to see the plan.

The plan should contain the planner-owned decisions defined in `references/rules/prd-planning-layer.md`, including structure, ownership, required artifacts, defaults, conflicts, and open questions.

Use the plan to guide the final PRD structure. Do not expose process mechanics, rule-engine language, or intermediate IR unless the user explicitly requests it.

## Renderer Role

After planning, act as a renderer:
- Treat the PRD generation plan as the structural source of truth.
- Expand planned sections into clear Chinese PRD language, tables, and diagrams.
- Preserve module ownership from the plan instead of redistributing rules during prose writing.
- Render defaults, assumptions, edge cases, acceptance criteria, and unresolved items from the plan.
- Keep acceptance criteria concise verification points rather than a second copy of business rules.

## Self-Check Role

After rendering, run `references/rules/prd-self-check.md` as an internal quality gate before final output.

- Fix small omissions directly in the PRD, such as missing acceptance checks, failure feedback, or open-question entries.
- If the self-check finds structural gaps, such as a missing state machine, missing system flow, missing permission matrix, or activated section not rendered, return to the planning layer and revise the generation plan before re-rendering.
- Do not output the self-check report unless the user explicitly asks for it.

## Page Detail Architecture

For each planned page, follow the generation plan, product prototype, and prepared design materials. Use this order when applicable:

1. Page goal and entry
2. Status Tabs
3. Filters
4. List fields
5. List row actions
6. Page-level operations

Rules:
- Describe status Tabs before filters when the plan or source materials include Tabs, because Tabs define the page's primary information structure.
- Do not create status Tabs during rendering. Unplanned Tabs require plan revision or a "待确认事项" entry.
- Add "适用状态/Tab" to filters, list fields, and row actions when the plan or source materials indicate Tabs or status-varying behavior.
- Use concise list field tables, normally "字段 / 字段逻辑", plus "适用状态/Tab" as planned.
- Use concise list row action tables, normally "操作名称 / 处理逻辑", plus "适用状态/Tab" as planned.
- Treat toolbar actions such as 新增、导入、导出 as page-level operations. Describe each concrete operation under "页面内操作" rather than in a summary table.
- Under "页面内操作", use concrete operation headings such as "新增", "编辑", "导入", "导出", "审核", or "撤回".
- Add a lightweight "页面形式" line when useful, such as 抽屉、弹窗、新页面、当前页内展开, to help front-end implementation.
- For operation fields and in-operation buttons, use one table with "控件名称 / 控件类型 / 是否必填 / Tips说明 / 业务规则". Include only controls shown in the prototype or product input. Buttons such as 提交、取消、确认、关闭、预览审批 should be rows with 控件类型=按钮, with click effects and success/failure feedback in "业务规则".
- Put complex row-action form details in the corresponding operation subsection, not in the row action summary.

## Output Specifications

- Start with document metadata when useful: version, owner, date, status, related links.
- Follow the generation plan for selected headings, diagrams, tables, permissions, and open questions.
- Prefer numbered headings matching the template's six major sections when the plan selects them.
- Render planned diagrams with Mermaid. Read `references/rules/mermaid-diagrams.md` before drafting or revising diagrams.
- Do not activate new scenario modules, sections, status-action mappings, permission matrices, or diagram types during rendering; revise the plan first.
- Keep technical operation plans in technical PRDs unless the user asks to include them here.
- Render planned rules with concrete nouns, measurable conditions, trigger conditions, validation rules, permission rules, and data rules.
- Render planned "待确认事项" when assumptions, conflicts, or unresolved business decisions remain.

## Resources Context

- Base template: `references/templates/prd-template.md`
- PRD planning layer: `references/rules/prd-planning-layer.md`
- Typed PRD plan schema: `references/rules/prd-plan-schema.md`
- PRD self-check: `references/rules/prd-self-check.md`
- Diagram rules: `references/rules/mermaid-diagrams.md`
- Complex lifecycle example: `references/examples/lifecycle-management-prd.md`
