---
name: prompt-generate
description: >-
  Generate structured agent mission prompts and optional SKILL.md drafts from
  user goal + example. Use for reverse-engineering prompt structure and
  producing concise, verifiable agent instructions.
---

# Prompt Generate — Compressed

Use when user gives:
1. target goal (task/repo/constraints)
2. example prompt/spec/message to emulate

Output: execution prompt, SKILL draft, or both.

## Core stance
- Concise by default; tokens are budget.
- Prefer real project knowledge over generic tips.
- Teach repeatable procedure, not one-off output.

## Must include (unless example conflicts)
1. Role line (domain + success target)
2. Done state (measurable outcomes)
3. Minimal required context
4. Direct ask (no vague "improve")
5. Control level by fragility (guidance/template/exact steps)
6. Constraints + non-goals
7. Priority order
8. Explicit output format
9. Environment gotchas
10. Pattern anchor from example
11. Plan-before-action, reflect-after-result loop
12. Tool policy (when to use/avoid)
13. Verification loop (tests/checks required)
14. Failure handling (switch strategy / blocked / long-running)

## Critical constraints block
If >5 constraints, put top 3 non-negotiables at top:
```markdown
> **Critical constraints** (read first)
> - [Rule 1]
> - [Rule 2]
> - [Rule 3]
```

## Token optimization defaults
1. Pick budget first: `tight` / `standard` / `high-fidelity`.
2. Static instructions first; request-specific details last.
3. Include only needed tools/params.
4. Keep commands/paths/thresholds exact; compress explanation.
5. State each rule once.
6. Use at most 1 short example unless fragile task.
7. Run final compression pass.

Budget guide:
- `tight`: <=700 tokens
- `standard`: <=1500 tokens
- `high-fidelity`: <=2500 tokens

## Output selection
- one-shot task -> execution prompt
- reusable capability -> `SKILL.md` (+ optional `examples.md`)
- both -> execution prompt first, condensed skill second

## Workflow
1. Parse example structure (role/mission/goals/context/constraints/phases/output/start).
2. Split fixed scaffold vs variable slots.
3. Fill missing inputs from workspace; if blocked ask one short question or mark `TBD`.
4. Generate prompt with same section order + specificity level.
5. Sanity-check commands/scope/placeholders/verification.
6. For high-stakes missions, run checklist in `examples.md`.

## Default execution prompt template
Use only if example gives no structure:
```markdown
> **Critical constraints** (read first)
> - [Top rule #1]
> - [Top rule #2]
> - [Top rule #3]

You are a [ROLE]. Mission: [ONE LINE].

## Project context
- Repo: [path], stack: [versions]
- Conventions: [file/link]
- Audience: [reviewers/consumers]

## Done looks like
1. [Measurable outcome]
2. [Measurable outcome]

## Gotchas
- [Non-obvious fact]
- [Project trap]

## Constraints
- [Positive directive]
- [Non-goal]
- Default tool: [X], fallback: [condition]
- Priority: [#1] > [#2] > [#3]

## Execution plan
1. [Phase] expect finding before action.
2. [Phase] reassess after each result.
3. Verify with `[test command]` before done.

## Progress checklist
- [ ] Step 1
- [ ] Step 2
- [ ] Step 3 (verify)

## Output format
- [per-phase updates]
- [final report shape]

## Failure handling
- 2 failed fixes same issue -> switch strategy
- blocked -> document blocker + ask one question
- long-running -> write `progress.md`

## Start now by
1. ...
2. ...
3. ...
```

## SKILL draft rules
- Follow [Agent Skills spec](https://agentskills.io/specification)
- Frontmatter: `name`, `description` (third-person; what+when+triggers)
- Keep SKILL body <= ~500 lines
- Move long examples/docs to `examples.md` or `references/`
- Avoid dumping one-off mega prompt into SKILL

## Resources
- Internal: `examples.md`
- External:
  - [Agent Skills Specification](https://agentskills.io/specification)
  - [Agent Skills Best Practices](https://agentskills.io/skill-creation/best-practices)
  - [Anthropic: Effective Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
  - [Anthropic: Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)
  - [OpenAI: GPT-4.1 Prompting Guide](https://cookbook.openai.com/examples/gpt4-1_prompting_guide)
