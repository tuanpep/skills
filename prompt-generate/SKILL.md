---
name: prompt-generate
description: >-
  Builds structured prompts for coding agents (and optional Cursor SKILL.md drafts)
  from the user's goal plus an example output: role, context, deliverables,
  constraints, output shape, tools, and failure handling. Use when the user wants
  a mission prompt for an agent, to reuse a prompt pattern for a new task, or to
  turn an example into a reusable skill.
---

# Prompt generate

Use this when the user gives **(1) a short goal** (topic, repo, constraints) and **(2) an example** they want to match—a full prompt, spec, or past message. **Reverse-engineer the example’s structure** and fill it for the new goal. Optionally produce a compact **SKILL.md** instead of a one-shot prompt.

## Agent prompting principles (bake into every generated prompt)

Align generated text with common **structured prompting** and **agent system prompt** guidance (role, task, constraints, format, examples). Sources vary; the list below is the practical consensus to apply **unless the user’s example explicitly contradicts it**.

1. **Role / persona** — One clear line: domain, seniority, and what “success” looks like (e.g. shipping tests, not refactoring prod “for style”).
2. **End-state over procedure** — Describe **what done looks like** (measurable outcomes), not just steps to follow. Agents handle unexpected situations better when they understand the goal than when following rigid scripts. Add numbered phases only for ordering dependencies.
3. **Task context** — Repo paths, stack, audience (e.g. reviewers, CI), and **why** the work matters (risk, regression).
4. **Direct instructions** — State the core ask plainly; agents follow literal wording—avoid vague verbs (“improve”, “clean up”) without measurable criteria.
5. **Constraints & guardrails** — Prefer **positive** directives (“use `TestDataBuilder`”, “run `./gradlew check`”) over long lists of “don’t”; include **non-goals** and “do not change production unless…” when relevant.
6. **Priorities** — When trade-offs exist, rank outcomes (e.g. state-machine correctness before cosmetic coverage).
7. **Output format** — Exact structure: headings, bullets, code fences for commands, what to report per phase.
8. **Few-shot / pattern** — The user’s **example output** is the behavioral template; if no example, offer 1 short **input → expected shape** snippet for the trickiest part (e.g. error response shape).
9. **Reasoning between actions** — Prompt the agent to **plan before each tool call** and **reflect after each result**: “Before each action, state what you expect to find and why. After each result, assess whether it changes your plan.” This prevents blind tool-call chains.
10. **Tools & environment** — If the agent will run commands, read files, or use MCP: say **when** to use each tool, **when NOT to** (e.g. “use Grep, not bash grep”), and **what success looks like** (e.g. “run tests and paste failing stack traces”). Include a verification step after every mutation: “After editing, run the relevant test.”
11. **Self-verification loop** — Every prompt must include a verification phase. The agent checks its own work against the stated deliverables before reporting done. Pattern: “Run [test command]. If tests fail, diagnose and fix. After 2 failed attempts at the same fix, stop and reassess your approach entirely.”
12. **Failure & recovery** — Three tiers, not just “stop and ask”:
    - **Wrong approach**: After 2 failed attempts, switch strategy entirely—don’t patch incrementally.
    - **Blocked**: Missing credentials, permissions, unclear spec → document what’s blocked + ask **one** question.
    - **Long-running**: Write a `progress.md` checkpoint so a fresh session can resume without re-deriving state.

**Critical constraints box** — For prompts with >5 constraints, place the top 3 non-negotiable rules in a quoted block at the **very top** of the prompt. Models attend most to the beginning and end of context (primacy/recency). Do not repeat these rules elsewhere.

```markdown
> **Critical constraints** (read first)
> - Do not modify production code unless a failing test proves a bug
> - All tests must pass before reporting done
> - Use [specific base class] for all new tests
```

**Context window awareness** — Keep instruction prompts under ~2000 tokens. If longer, extract stable context (repo layout, conventions) into a referenced file rather than inlining. For Claude, use XML tags (`<constraints>`, `<context>`, `<deliverables>`) for structural sections—Claude parses these more reliably than markdown headers in system prompts.

**Context stack (for long missions)** — For autonomous agents, instructions are only one layer. When generating prompts for **multi-step repo work**, remind the agent to rely on: repository facts (files, configs), **tool** definitions if any, and **fresh** verification (run tests), not only memory from the prompt.

**Length** — Prefer **dense, scannable** sections over prose. Put **must-follow** rules and paths **early**. Avoid repeating the same rule in multiple sections.

## Outputs (ask if unclear; default: execution prompt)

| User asks for | Deliver |
|---------------|---------|
| One-shot task for an agent | **Execution prompt** (markdown): role, mission, context, deliverables, quality bar, phases, output format, "Start now" |
| Reusable Cursor skill | **SKILL.md draft** + optional `examples.md`: follow project `create-skill` conventions (YAML frontmatter, third-person description, concise body) |
| Both | Execution prompt first, then condensed skill capturing stable rules only |

## Workflow

1. **Parse the example** — Identify fixed structure vs. variable slots:
   - Title line / role declaration
   - Mission one-liner
   - Numbered goals
   - Project context (stack, paths, rules)
   - Deliverables (numbered, testable)
   - Quality bar / non-goals
   - Execution plan (phases)
   - Output format (progress, files, commands, report)
   - Kickoff ("Start now by: …")

2. **Extract the pattern** — List section headings in order. Note bullets vs. paragraphs, depth, and any must-have phrases.

3. **Gather gaps from the user's brief** — If repo path, stack, or constraints are missing, infer from workspace when possible; otherwise ask **one** short question or mark `TBD` in a clearly labeled block.

4. **Generate** — Fill the same skeleton with the new domain. Preserve:
   - Section order and numbering style from the example
   - Specificity (paths, commands, test naming) at the same level as the example
   - Actionable "Start now" first steps

5. **Sanity check** — No placeholder lorem; commands match the stated stack; scope matches user intent; if generating a skill, keep **SKILL.md under ~500 lines** and move long examples to `examples.md`. Apply the **Agent prompting principles** section: priorities explicit, constraints clear, output format specified, failure behavior stated.

6. **Quality pass** — Run through the checklist in [examples.md](examples.md#prompt-quality-checklist) when the user needs a high-stakes or long-running agent mission.

## Execution prompt template (adapt to match user's example)

Use this only as a **structural default** when the example does not dictate otherwise:

````markdown
> **Critical constraints** (read first)
> - [Top non-negotiable rule #1]
> - [Top non-negotiable rule #2]
> - [Top non-negotiable rule #3]

You are a [ROLE]. Your mission is to [ONE LINE].

<context>
## Project context
- Repo: [path], stack: [versions]
- Key conventions: [link to CLAUDE.md or inline]
- Audience: [who reviews / consumes the output]
</context>

## Done looks like
1) [Measurable outcome, not activity]
2) [Measurable outcome]

<constraints>
## Constraints
- [Positive directive: "use X", "run Y"]
- [Non-goal: "do NOT refactor unrelated code"]
- Priority order if time-boxed: [#1] > [#2] > [#3]
</constraints>

## Execution plan
1) [Phase] — Before acting, state what you expect to find.
2) [Phase] — After each result, reassess whether the plan still holds.
3) **Verify** — Run `[test command]`. All must pass. If 2 fixes fail for the same issue, stop and rethink your approach.

## Output format
- [What to emit per phase: progress, files changed, commands run]
- Final report: [structure]

## On failure
- **Wrong approach** (2 failed fixes): switch strategy, don't patch.
- **Blocked** (missing access/unclear spec): document blocker + ask ONE question.
- **Long-running**: write `progress.md` checkpoint before stopping.

## Start now by:
1) ...
2) ...
3) ...
````

Tune headings to mirror the **user's example** (e.g. "Final report in markdown" vs "Deliverables"). For Claude agents, prefer XML tags (`<context>`, `<constraints>`) for structural sections; for Cursor/other agents, use plain markdown headers.

## SKILL.md draft template (when user wants a reusable skill)

- Frontmatter: `name` (lowercase-hyphen), `description` (WHAT + WHEN, third person, trigger terms).
- Body: Scope, instructions, optional link to [examples.md](examples.md).
- Do **not** paste huge one-off mission prompts into SKILL.md—summarize durable rules; put full prompt examples in `examples.md`.

## Additional resources

- For structural anatomy, before/after examples, and a **prompt quality checklist**, see [examples.md](examples.md).

## Optional further reading (external)

- [Anthropic: Effective Context Engineering for AI Agents](https://www.anthropic.com/engineering/effective-context-engineering-for-ai-agents) — treat every token as a scarce resource; compaction, summarization, layered context.
- [Anthropic: Building Effective Agents](https://www.anthropic.com/research/building-effective-agents) — when to use single prompts vs. orchestration; tool-use patterns.
- [OpenAI: GPT-4.1 Prompting Guide](https://cookbook.openai.com/examples/gpt4-1_prompting_guide) — persistence, tool-calling, and planning reminders for agentic loops.
- [Spotify: Context Engineering for Background Agents](https://engineering.atspotify.com/2025/11/context-engineering-background-coding-agents-part-2) — end-state prompts outperform step-by-step; feedback loops.
- [Arize: CLAUDE.md Best Practices](https://arize.com/blog/claude-md-best-practices-learned-from-optimizing-claude-code-with-prompt-learning/) — focused 50-line files outperform 500-line kitchen sinks.
