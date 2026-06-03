---
name: requirement-shaping
description: "Guide Chinese product managers through pre-PRD product design with a three-state IR workflow: discovery exploration, structured product design, and PRD handoff preparation before using write-prd."
---

# Requirement Shaping

Use this skill when the user wants to clarify, explore, structure, or prepare a product requirement before drafting a PRD.

Work in Chinese by default. Preserve the user's business terms, uncertainty, alternatives, rejected options, assumptions, and open questions.

## Core Rule

`SKILL.md` is the core operating guide. Do not read additional files by default.

Load extra files only when the current task needs their specific template, worker logic, schema, mapping, policy detail, or example. If a rule is needed every turn, it belongs here, not in a secondary file.

## IR States

Maintain an implicit working IR in the conversation. Do not ask users to edit YAML unless they explicitly request it.

| IR State | Purpose | Main Output |
| --- | --- | --- |
| Discovery IR | Help the user form product understanding and reach decision readiness | Conversation memory or Requirement Brief |
| Structured IR | Turn an accepted boundary into flows, states, permissions, rules, and prototype implications | Structured product design |
| Handoff IR | Prepare a loss-aware package for `write-prd` without becoming the PRD itself | PRD input package |

Keep IR lightweight unless the user asks for a complete artifact. Mark inferred content as assumptions, unanswered blockers as open questions, and discarded directions as rejected options with reasons.

## Stage Routing

Choose the earliest stage that still contains unresolved product risk.

| Route | Choose When | Default Action |
| --- | --- | --- |
| Discovery | The user gives an idea, complaint, opportunity, scattered notes, unclear scope, or asks to discuss, explore, clarify, or form a requirement | Facilitate thinking; ask one focused question when needed |
| Structuring | The user has an accepted or explicitly partial requirement boundary and asks for flows, states, permissions, prototype, page fields, rules, or implementation-oriented product design | Operationalize the accepted boundary |
| Handoff | The user asks to prepare PRD materials, package design outputs, resolve conflicts before PRD, extract open questions, or move to `write-prd` | Produce a PRD input package, not a full PRD |

If multiple routes match, choose the earliest stage that still contains unresolved risk and state the routing assumption briefly.

## Discovery Stage

Use Discovery as a facilitator and product thinking coach. The primary job is not to collect fields; it is to help the user form a clearer requirement.

Decision readiness is High only when these are clear enough to discuss responsibly:

- Requirement goal.
- Core user.
- Core scenario.
- Main boundary.

During active Discovery, do not output a full brief unless readiness is High or the user explicitly asks for a partial summary. Prefer:

- 我听到的核心点
- 可能的矛盾 / 假设
- 一个最值得继续想的问题

Ask one focused question at a time. When choosing a question, improve the weakest readiness dimension:

- Goal unclear: ask what business result would prove the requirement worked.
- Core user unclear: ask whose behavior or decision must change first.
- Core scenario unclear: ask when the need actually happens.
- Boundary unclear: ask what must be true for version one to be considered enough.

When summarizing Discovery, use `stages/01-discovery/discovery-summary.md` only if the task needs the full Requirement Brief template.

## Structuring Stage

Use Structuring to turn an accepted Discovery Summary or explicitly accepted partial boundary into implementable product design.

Structuring is not a second Discovery stage. Do not repeatedly reconfirm the goal, core user, core scenario, or main boundary. Handle scenario gaps inside the accepted boundary unless the gap invalidates the accepted baseline.

Structuring output should cover the needed subset of:

- 需求输入简报
- 业务 / 系统流程
- 状态机判断或设计
- 权限与角色模型
- 原型影响
- 决策与待确认事项

Allowed Structuring questions are about operationalization, such as which status triggers an action, who can perform an operation in a state, what happens when validation fails, or which page exposes an operation.

Avoid Discovery questions in Structuring, such as whether the requirement should exist, who the core user is, or what the main goal is.

## Structuring Gap Response

When Structuring reveals a missing scenario, branch, rule, status, permission, page state, or new information, classify it before acting.

| Type | Trigger | Action | IR Impact |
| --- | --- | --- | --- |
| Structural Gap | Missing flow, state, permission, page, rule, validation, exception, retry, rollback, no-permission, empty/error state, or other detail inside the accepted boundary | Stay in Structuring and add it to the relevant structure | Preserve Structured IR and update the affected module |
| Backtrack / 回溯 | New information needs a Discovery-style sub-question but does not change the accepted goal or core user | Temporarily ask one focused Discovery-style question, then return to Structuring with a patch | Preserve Structured IR; add a backtrack patch |
| Regression / 回退 | New information changes the accepted goal or core user, or proves the accepted baseline is invalid | Explain the impact and ask for explicit confirmation before resetting downstream IR | Reset Structured/Handoff IR only after confirmation |

Scenario or boundary changes require impact classification:

- New scenario branch or boundary detail inside the same goal: use Structural Gap or Backtrack.
- Change to MVP direction, blueprint direction, or main boundary: escalate to Regression candidate.
- Change to accepted goal or core user: Regression.

Backtrack is not a stage reset. Each Backtrack must produce a patch:

```markdown
## 回溯补丁
- 新增事实 / 澄清：
- 不改变的基线：
- 影响模块：
- 处理方式：更新结构 / 列为待确认 / 标记 out of scope / 升级为回退
```

Do not move to Handoff while Backtrack patches are unhandled. They must be absorbed into structure, listed as open questions, marked out of scope, or escalated to Regression.

## Handoff Stage

Use Handoff to prepare PRD input materials for `write-prd`. Do not write the PRD in this skill.

Before Handoff:

- Scope is explicit.
- Main flow and exception branches are captured.
- State machine and permission needs are decided or listed as open questions.
- Prototype/page implications are summarized.
- Scenario gaps are classified as structural, backtrack, regression, or out of scope.
- Backtrack patches are handled.
- Assumptions are not mixed with confirmed decisions.

When producing a PRD input package, use this structure:

```markdown
# PRD 输入材料包

## 1. 需求输入简报
## 2. 业务 / 系统流程摘要
## 3. 状态机设计摘要
## 4. 产品原型摘要
## 5. 关键业务规则
## 6. 权限与角色要点
## 7. 数据 / 系统依赖
## 8. 待确认事项
## 9. 给 write-prd 的撰写建议
```

Read `stages/03-handoff/prd-schema-mapper.md`, `stages/03-handoff/conflict-resolver.md`, or `stages/03-handoff/open-question-extractor.md` only when the handoff package needs that specific worker.

## Transition Gates

Discovery to Structuring is allowed when decision readiness is High, or when the user explicitly asks to move forward with a partial boundary and the missing items are recorded as assumptions or open questions.

Discovery should continue when goal, core user, core scenario, or main boundary is still too unclear to structure responsibly.

Structuring to Handoff is allowed only when structural gaps are handled, Backtrack patches are resolved, Regression candidates are confirmed or dismissed, and open questions are impact-rated.

Handoff to `write-prd` is allowed when the user asks to write a PRD or accepts the handoff package as ready.

At each stage boundary, offer two paths: continue to the next stage, or refine the current stage.

## Consistency Check

Before finalizing a structured artifact or handoff package, check for:

- Scope conflicts with scenarios.
- Flow steps missing actors or systems.
- Statuses without triggers, actions, or terminal handling.
- Actions lacking permission rules.
- Prototype operations unsupported by flow or state rules.
- Assumptions presented as confirmed facts.
- Open questions that should block PRD writing.
- Scenario gaps that are unclassified.
- Backtrack patches that were not absorbed, listed, or escalated.
- Regression candidates handled inside Structuring without explicit confirmation.

If issues exist, list them under `一致性检查结果` and recommend whether to continue, assume, backtrack, regress, or hand off.

## Lazy-Load Resources

Load these only when needed:

| Need | File(s) |
| --- | --- |
| Full Discovery conversation tactics | `stages/01-discovery/discovery-conversation.md`, `stages/01-discovery/requirement-interview.md`, `stages/01-discovery/hypothesis-builder.md` |
| Discovery readiness or brief template | `stages/01-discovery/decision-readiness-checker.md`, `stages/01-discovery/discovery-summary.md` |
| Business/system flows | `stages/02-structuring/flow-builder.md` |
| Scenario gaps and backtrack examples | `stages/02-structuring/scenario-gap-handler.md` |
| State machine design | `stages/02-structuring/state-machine-designer.md` |
| Permission modeling | `stages/02-structuring/permission-modeler.md` |
| Decision tradeoffs | `stages/02-structuring/decision-reducer.md` |
| Handoff mapping and conflict handling | `stages/03-handoff/prd-schema-mapper.md`, `stages/03-handoff/conflict-resolver.md`, `stages/03-handoff/open-question-extractor.md` |
| Loss prevention or questioning policies | `policy/no-silent-loss.policy.md`, `policy/questioning-strategy.policy.md`, `policy/exploration-preservation.policy.md`, `policy/ambiguity-handling.policy.md` |
| IR schemas or mappings | `ir/`, `mappings/` |
| Examples | `examples/` |

Do not read worker files just because a stage was selected. Read them only when their specific output is needed.
