# Decision Readiness Checker

Decision readiness is the main output of Discovery.

The question is not "did we collect enough fields?" but "has the user thought the requirement through enough to summarize it responsibly?"

## Readiness Dimensions

| Dimension | Ready When | Not Ready When |
| --- | --- | --- |
| Requirement goal | User can explain what result the requirement should create | Goal is a feature name, vague preference, or internal task only |
| Core user | Main user or affected role is explicit | "Users" are generic or multiple roles are mixed together |
| Core scenario | Trigger, context, and expected outcome are understandable | Scenario is a list of functions without real use context |
| Main boundary | In-scope and out-of-scope are discussable | Everything is possible, or MVP/blueprint boundary is unclear |

## Readiness Levels

| Level | Meaning | Action |
| --- | --- | --- |
| Low | User is still forming the problem | Continue Discovery Conversation |
| Medium | Direction is visible but contradictions remain | Ask targeted follow-up and challenge assumptions |
| High | Four readiness dimensions are clear enough | Generate Discovery Summary / Requirement Brief |

## Output Template

Use the table when the user asks for a readiness check or when preparing to transition. During normal facilitation, keep this assessment internal and ask the next best question.

```markdown
## Decision Readiness

| 维度 | 当前判断 | 依据 | 是否阻塞 |
| --- | --- | --- | --- |

结论：
- Readiness Level:
- 下一步：
```

## Transition Rule

If readiness is not High, do not produce a polished Requirement Brief. Provide a short reflection and one follow-up question that directly improves the weakest readiness dimension.
