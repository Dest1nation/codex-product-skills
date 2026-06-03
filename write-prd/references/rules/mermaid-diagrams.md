# Mermaid Diagram Rules

Use these rules when creating, reviewing, or revising PRD diagrams.

## Selection

- Use `flowchart TD` for system flows with cross-system processing, branching, validation, asynchronous jobs, and exception paths.
- Do not use `sequenceDiagram` in PRDs by default. Use it only for explicit user requests about backend interaction timing in the PRD; otherwise leave sequence diagrams to technical design documents.
- Use `stateDiagram-v2` when a business object's status affects visible data, available actions, permissions, approval handling, scheduled or business-event processing, risk calculation, reminders/notifications, or downstream business results.
- Use `stateDiagram-v2` for lightweight computed statuses when dates, records, rules, or upstream data derive statuses that affect page labels, risk buttons, counts, scheduled scans, notifications, or downstream recognition. These are business state machines even when no user action directly moves the status.
- Do not use a state machine solely for transient operation results such as loading, save success/failure, or one-time export completion unless they drive business decisions or subsequent operations.

## General Rules

- Use Chinese labels unless the product, codebase, or engineering convention uses English.
- Keep node names short and business-readable.
- Put state transition rules directly on `stateDiagram-v2` transition labels when they are short enough. Use the format `操作 / 角色 / 条件` or `触发事件 / 条件 -> 结果`.
- Put long validation rules, data fields, permission checks, and exception handling in page details, permission tables, or exception tables rather than overloading node labels.
- For computed statuses, put formulas, priority rules, date windows, and edge conditions in a focused status calculation table after the diagram.
- Render planned normal paths, rejection paths, cancellation paths, timeout paths, and system exception paths.
- For missing information already identified by the plan, render a minimal diagram with `待确认` nodes and list the missing decisions under "待确认事项".
- Do not create generic transition-supplement tables after a state machine that already explains the flow. Use lightweight status-action tables for operation visibility, and focused exception tables for rollback, timeout, notification, or audit rules that materially affect implementation.

## Flowchart Pattern

```mermaid
flowchart TD
    A[用户发起操作] --> B{基础校验是否通过}
    B -- 否 --> C[提示校验失败原因]
    B -- 是 --> D[提交业务请求]
    D --> E{业务规则是否通过}
    E -- 否 --> F[返回业务拦截提示]
    E -- 是 --> G[系统处理数据]
    G --> H[写入操作日志]
    H --> I[返回处理结果]
    I --> J[触发后续通知或流转]
```

## Sequence Pattern

Use only on explicit request.

```mermaid
sequenceDiagram
    actor U as 用户
    participant FE as 前端页面
    participant API as 业务服务
    participant DB as 数据库
    participant EXT as 外部系统/消息服务

    U->>FE: 发起操作
    FE->>FE: 前端字段校验
    FE->>API: 提交请求
    API->>API: 权限与业务规则校验
    API->>DB: 查询/写入业务数据
    DB-->>API: 返回处理结果
    API->>EXT: 发送通知/触发异步任务
    API-->>FE: 返回成功或失败结果
    FE-->>U: 展示处理反馈
```

## State Machine Pattern

```mermaid
stateDiagram-v2
    [*] --> 草稿
    草稿 --> 待提交: 暂存 / 创建人 / 必填可缺省
    待提交 --> 待审核: 提交 / 创建人 / 必填完整且附件合规
    待提交 --> 已取消: 取消 / 创建人或管理员 / 未进入审批
    待审核 --> 已驳回: 驳回 / 审批人 / 说明驳回原因
    待审核 --> 已取消: 撤回或取消 / 创建人或管理员 / 审批未完成
    待审核 --> 已通过: 审核通过 / 审批人 / 审批流完成
    已驳回 --> 待审核: 重新提交 / 创建人 / 修改后再次校验
    已通过 --> 已生效: 生效 / 系统 / 到达开始日期
    已生效 --> 已失效: 到期或停用 / 系统或管理员 / 到结束日期或手动终止
    已取消 --> [*]
    已失效 --> [*]
```

After the diagram, add a table only for new implementation decisions. Prefer focused exception or status-action visibility tables over broad transition-supplement tables.
