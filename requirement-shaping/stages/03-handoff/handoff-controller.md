# Handoff Controller

Use Handoff to prepare PRD input materials for `write-prd`.

## Steps

1. Run `conflict-resolver.md`.
2. Run `open-question-extractor.md`.
3. Map Structured IR to Handoff IR using `mappings/structured-to-handoff.map.yaml`.
4. Map Handoff IR to PRD planning using `prd-schema-mapper.md`.
5. Produce a PRD input package, not a full PRD.

## Output

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
