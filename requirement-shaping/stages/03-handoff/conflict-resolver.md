# Conflict Resolver

Check for conflicts before handoff.

## Common Conflicts

- Scope says excluded, but flow or prototype includes it.
- A status enables an action that permission rules deny.
- A page operation has no business flow or system rule.
- A business object has lifecycle behavior but no state decision.
- An assumption is written as a confirmed rule.
- An open question affects acceptance criteria but is hidden.

Output conflicts as:

```markdown
| 冲突 | 位置 | 影响 | 建议处理 |
| --- | --- | --- | --- |
```
