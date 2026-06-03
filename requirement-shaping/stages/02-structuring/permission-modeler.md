# Permission Modeler

Use this when roles, data scope, action rights, approval rights, or page visibility affect product behavior.

## Permission Dimensions

- Role: who the user is.
- Data scope: what records the user can see.
- Action scope: what operations the user can execute.
- State condition: when the action is available.
- Ownership: whether the user created, owns, manages, or reviews the record.
- Exception authority: who can override, rollback, or manually handle abnormal cases.

## Output Template

```markdown
| 角色 | 可见范围 | 可执行操作 | 状态限制 | 数据限制 | 备注 |
| --- | --- | --- | --- | --- | --- |
```
