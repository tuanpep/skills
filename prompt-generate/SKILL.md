---
name: prompt-generate
description: >-
  Generates structured agent mission prompts and optional SKILL.md drafts from
  user goal plus example. Use for prompt reverse-engineering, reusable skill
  extraction, and agent prompt quality hardening.
---

# Prompt generate

Use when user gives:

1. target goal (repo/task/constraints), and
2. example prompt/spec/message to mimic.

Output either execution prompt, SKILL draft, or both.

## Core stance

- Keep prompt concise. Every token competes with tool output/history.
- Prefer real project knowledge over generic advice.
- Teach repeatable procedure, not one-off output.

## Must-include principles

Apply unless example explicitly conflicts.

1. **Role**: one clear line (domain + success criteria).
2. **End-state**: define done as measurable outcomes.
3. **Context**: include only missing repo/task facts.
4. **Direct ask**: avoid vague verbs without criteria.
5. **Control level by fragility**:
   - High freedom: guidance
   - Medium freedom: template
   - Low freedom: exact steps/commands
6. **Constraints**: prefer positive directives + explicit non-goals.
7. **Priorities**: rank trade-offs.
8. **Output format**: exact expected structure.
9. **Gotchas**: include environment-specific traps.
10. **Pattern anchor**: use user example as behavioral template.
11. **Reasoning loop**: plan before action, reflect after result.
12. **Tool policy**: when to use / when not to use each tool.
13. **Verification loop**: always run tests/checks before done.
14. **Failure handling**:
    - wrong approach (2 failed attempts) -> switch strategy
    - blocked -> document + ask one question
    - long-running -> write `progress.md`

## Critical constraints block

If prompt has >5 constraints, place top 3 non-negotiables at very top, once.

```markdown
> **Critical constraints** (read first)
>
> - [Rule 1]
> - [Rule 2]
> - [Rule 3]
```

## Token optimization defaults

1. Pick budget first (`tight`, `standard`, `high-fidelity`).
2. Put static instructions first; dynamic request details last.
3. Include only needed tools/schema fields.
4. Keep exact commands/paths/thresholds; compress explanations.
5. Do not repeat same rule in multiple sections.
6. Limit examples (0-1 unless task is fragile).
7. Run final compression pass.

Budget guide:

- `tight`: <= 700 tokens
- `standard`: <= 1500 tokens
- `high-fidelity`: <= 2500 tokens

## Output selection

| User asks for       | Deliver                                      |
| ------------------- | -------------------------------------------- |
| one-shot agent task | execution prompt (markdown)                  |
| reusable capability | `SKILL.md` draft (+ optional `examples.md`)  |
| both                | execution prompt first, then condensed skill |

## Workflow

1. Parse example structure:
   - title/role
   - mission line
   - goals
   - context
   - deliverables
   - constraints
   - phases
   - output format
   - kickoff wording
2. Separate fixed scaffold vs variable slots.
3. Fill missing inputs from workspace; if still missing, ask one short question or mark `TBD`.
4. Generate new prompt preserving section order + specificity level.
5. Sanity-check:
   - commands match stack
   - scope matches ask
   - no placeholder text
   - constraints/priorities/verification present
6. For high-stakes missions, run checklist in [examples.md](examples.md#prompt-quality-checklist).

## Execution prompt default template

Use only when user example does not prescribe structure:

```markdown
> **Critical constraints** (read first)
>
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

- [Non-obvious environment fact]
- [Non-obvious project rule]

## Constraints

- [Positive directive]
- [Non-goal]
- Default tool: [X], fallback: [condition]
- Priority: [#1] > [#2] > [#3]

## Execution plan

1. [Phase] — state expected finding before action.
2. [Phase] — reassess after each result.
3. Verify — run `[test command]`; all pass before done.

## Progress checklist

- [ ] Step 1
- [ ] Step 2
- [ ] Step 3 (verify)

## Output format

- [per-phase updates]
- [final report shape]

## Failure handling

- Wrong approach: 2 failed fixes -> switch strategy
- Blocked: document blocker + ask one question
- Long-running: write `progress.md`

## Start now by

1. ...
2. ...
3. ...
```

## SKILL.md draft rules

Follow [Agent Skills spec](https://agentskills.io/specification):

- Required frontmatter:
  - `name` (lowercase-hyphen, dir-matching)
  - `description` (third person; what + when + triggers)
- Keep SKILL body under ~500 lines; move long examples to `examples.md`/`references/`.
- Use progressive disclosure; one-level file references.
- Do not dump large one-off prompts into SKILL body.

## Resources

- Internal checklist/examples: [examples.md](examples.md)
- External references:
  - [Agent Skills Specification](https://agentskills.io/specification)
  - [Agent Skills Best Practices](https://agentskills.io/skill-creation/best-practices)
  - [Anthropic: Effective Context Engineering](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents)
  - [Anthropic: Building Effective Agents](https://www.anthropic.com/research/building-effective-agents)
  - [OpenAI: GPT-4.1 Prompting Guide](https://cookbook.openai.com/examples/gpt4-1_prompting_guide)
