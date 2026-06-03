# PRD Schema Mapper

Map Handoff IR to a PRD writing plan.

## Mapping

| Handoff IR Section | PRD Destination |
| --- | --- |
| requirement_brief | 背景、目标、范围 |
| flow_summary | 业务流程、系统流程、异常流程 |
| state_summary | 状态流转、操作规则、页面状态 |
| prototype_summary | 页面说明、字段规则、交互反馈 |
| permissions | 权限设计 |
| rules | 业务规则、校验规则、非功能规则 |
| assumptions | 假设说明 |
| open_questions | 待确认事项 |

When invoking `write-prd`, pass the package and ask it to preserve assumptions and open questions.
