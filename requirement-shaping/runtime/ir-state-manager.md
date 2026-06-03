# IR State Manager

Maintain an implicit working IR in the conversation. Do not require users to edit YAML unless they ask.

## Discovery Update Rules

- Treat Discovery IR as conversation memory plus decision readiness, not a field collector.
- Record the user's changed understanding after meaningful turns.
- Record model questions only when they shaped thinking.
- Do not generate a Requirement Brief until readiness is High, unless the user explicitly asks for a partial summary.
- Do not expose YAML-like IR to the user during normal Discovery Conversation. Use natural facilitation language.

## General Update Rules

- Outside Discovery Conversation, add raw facts to the current IR before summarizing them.
- Mark inferred content as assumption.
- Mark unanswered blockers as open questions.
- Move discarded directions to rejected options with reasons.
- When summarizing, include what changed since the previous stage.

## Output Pattern

When useful, expose the IR as:

```markdown
## 当前 IR 状态

- 阶段：
- Discovery Readiness：
- 已确认：
- 假设：
- 待确认：
- 可能影响后续设计的风险：
```

Keep the IR lightweight unless the user asks for a complete artifact.
