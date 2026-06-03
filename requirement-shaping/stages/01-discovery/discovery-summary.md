# Discovery Summary

Use this layer only after Decision Readiness is High, or when the user explicitly asks to summarize current progress with gaps preserved.

Discovery Summary creates `brief_material` for the next stage. It should not replay the whole conversation; it should preserve only the understanding needed to structure the product responsibly.

## Requirement Brief Template

```markdown
# 需求输入简报

## 1. 需求目标

## 2. 核心用户

| 用户 / 角色 | 场景 | 关注点 |
| --- | --- | --- |

## 3. 核心场景

| 场景 | 触发条件 | 用户要完成什么 | 期望结果 |
| --- | --- | --- | --- |

## 4. 主要边界

### 4.1 本期包含

### 4.2 暂不包含

## 5. 已形成的关键判断

| 判断 | 理由 | 影响 |
| --- | --- | --- |

## 6. 仍需查漏补缺的问题

| 问题 | 影响 | 建议下一步 |
| --- | --- | --- |
```

## Summary Rules

- Preserve the user's own terms.
- Distinguish confirmed understanding from model assumptions.
- Include unresolved tensions instead of smoothing them over.
- End by recommending whether to move to Structuring or continue Discovery Conversation.
