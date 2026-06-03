# State Machine Designer

Design a state machine when business statuses affect visibility, operations, permissions, downstream processing, audit, rollback, fulfillment, settlement, or approval.

## Steps

1. Identify the business object.
2. Define statuses and business meanings.
3. Identify initial, terminal, normal, abnormal, and rollback statuses.
4. Define transitions with trigger, actor/system, precondition, target state, and side effects.
5. Map statuses to visible actions, editable fields, and permission checks.
6. Add timeout, cancellation, rejection, retry, and manual handling rules.

## Output Template

```markdown
## 状态机设计

| 状态 | 含义 | 类型 | 用户可见文案 |
| --- | --- | --- | --- |

| 当前状态 | 触发动作 / 事件 | 触发方 | 前置条件 | 目标状态 | 后置结果 | 异常处理 |
| --- | --- | --- | --- | --- | --- | --- |

| 状态 | 可见操作 | 可操作角色 | 字段编辑性 | 页面影响 |
| --- | --- | --- | --- | --- |
```
