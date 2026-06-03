---
name: requirement-shaping
description: "Guide Chinese product managers through pre-PRD product design with a three-state IR workflow: discovery exploration, structured product design, and PRD handoff preparation before using write-prd."
---

# Requirement Shaping

Use this skill when the user wants to clarify, explore, structure, or prepare a product requirement before drafting a PRD.

The skill is controlled by three IR states and a stage router. The goal is to help the user form product understanding before summarizing it, instead of silently compressing discovery into a final document.

## Three-State IR

| IR State | Purpose | Primary Stage |
| --- | --- | --- |
| Discovery IR | Facilitate product thinking; main outcome is decision readiness, with summary generated only when ready | `stages/01-discovery/` |
| Structured IR | Turn an accepted requirement boundary into complete flows, states, permissions, rules, and prototype decisions | `stages/02-structuring/` |
| Handoff IR | Prepare a loss-aware package for `write-prd` without becoming the PRD itself | `stages/03-handoff/` |

Before producing any artifact, identify the current IR state. If unclear, use `runtime/stage-router.md`.

## Stage Routing

1. Read `runtime/stage-router.md` to decide the stage.
2. Read `runtime/ir-state-manager.md` to update or evolve the current IR.
3. Apply the relevant controller:
   - Discovery: `stages/01-discovery/discovery-controller.md`
   - Structuring: `stages/02-structuring/structuring-controller.md`
   - Handoff: `stages/03-handoff/handoff-controller.md`
4. Before stage transitions, apply `runtime/transition-engine.md` and `policy/stage-transition-gates.policy.md`.
5. Before handoff or summarization, run `runtime/consistency-checker.md`.

## Operating Rules

- Work in Chinese by default.
- Preserve the user's business terms, uncertainty, alternatives, and rejected options.
- In Discovery, act as a facilitator and product thinking coach: ask, challenge, reflect, and help the user form their own understanding before summarizing.
- In Structuring, do not rediscover the requirement. Handle scenario gaps inside the accepted boundary; return to Discovery only when a gap changes goal, core user, core scenario, or main boundary.
- Ask one focused question at a time when discovery is fuzzy. Do not turn early discovery into a collector checklist.
- Do not silently drop exploration details. Follow `policy/no-silent-loss.policy.md`.
- Do not force a PRD. Hand off to `write-prd` only when the user asks for PRD writing or the Handoff IR is complete enough.
- At each stage boundary, offer two paths: continue to the next stage, or refine the current stage.
- If the user wants to move forward despite gaps, make assumptions explicit and record them in `memory/assumption-log.md`.

## Resource Map

- IR schemas: `ir/`
- Stage controllers and workers: `stages/`
- Persistent working memory templates: `memory/`
- Process policies: `policy/`
- IR transformation maps: `mappings/`
- Runtime control logic: `runtime/`
- Examples: `examples/`
