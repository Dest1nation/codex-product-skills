# Structuring Controller

Use Structuring to turn an accepted Discovery Summary into implementable product design.

Structuring is not a second Discovery stage. It should not reopen the product goal, core user, core scenario, or main boundary unless a discovered gap proves the Discovery output was not ready.

## Difference from Discovery

| Question Type | Discovery | Structuring |
| --- | --- | --- |
| Goal | What result should this requirement create? | Given the goal, what product/system behavior is needed? |
| User | Who is the core user or affected role? | Given the roles, what permissions and entries are needed? |
| Scenario | When does the need happen? | Given the scenario, what flow and exception paths exist? |
| Boundary | What is in/out for this requirement? | Given the boundary, what rules, states, and screens are needed? |
| Decision | Is this the right requirement shape? | How should the accepted shape be operationalized? |

## Steps

1. Consume the accepted Requirement Brief / `brief_material` as the baseline.
2. Use `scenario-gap-handler.md` when missing scenarios appear.
3. Use `flow-builder.md` for business/system/user/exception flows.
4. Decide whether state machine design is required.
5. Use `state-machine-designer.md` when lifecycle status affects actions, permissions, display, or downstream processing.
6. Use `permission-modeler.md` when roles, data scope, or action rights matter.
7. Use `decision-reducer.md` to choose among competing implementation options and record tradeoffs.
8. Summarize page/prototype implications.

## Output

Structure output as:

- 需求输入简报
- 业务 / 系统流程
- 状态机判断或设计
- 权限与角色模型
- 原型影响
- 决策与待确认事项

## Allowed Questions

Structuring may ask operationalization questions:

- Which status should trigger this action?
- Who can perform this operation in this state?
- What happens when sync, approval, or validation fails?
- Which page should expose this operation?

Structuring should avoid Discovery questions:

- Who is the core user?
- What is the main goal?
- Should this requirement exist?
- Is this in scope at all?

If a missing scenario changes the goal, core user, core scenario, or main boundary, route back to Discovery Conversation.
