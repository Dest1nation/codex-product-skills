# Flow Builder

Build separate but connected flows.

## Flow Layers

| Layer | Purpose |
| --- | --- |
| Business flow | How the real business progresses across roles and scenarios |
| System flow | How modules, services, and external systems process data/events |
| User operation flow | What users submit, approve, cancel, query, import, or export |
| Exception flow | Rejection, timeout, rollback, duplicate, missing data, sync failure |

## Output Template

```markdown
## 业务 / 系统流程

### 参与角色与系统

| 类型 | 名称 | 职责 |
| --- | --- | --- |

### 主流程

### 分支与异常

| 场景 | 触发条件 | 处理方式 | 结果 |
| --- | --- | --- | --- |

### 系统处理规则

| 节点 | 系统动作 | 输入 | 输出 | 失败处理 |
| --- | --- | --- | --- | --- |
```
