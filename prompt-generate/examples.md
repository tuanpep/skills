# Examples and quality checklist

This file provides **concrete prompt examples** and a quality checklist. When generating new prompts, match **section order and depth** to the user's example, not necessarily these.

---

## Before / After: vague prompt → structured agent prompt

### Before (weak)

```
You are a senior developer. Write tests for the allocation service.
Make sure they cover edge cases and follow best practices.
Run the tests when done.
```

**Problems**: No repo context, no measurable "done", vague deliverables ("edge cases"), no failure handling, no verification loop, no priority order, explains nothing the agent doesn't already know.

### After (structured)

```markdown
> **Critical constraints** (read first)
>
> - Do NOT modify production code unless a failing test proves a bug
> - All new tests extend `AbstractServiceTest` and use `TestDataBuilder`
> - All tests must pass: `./gradlew :rms-service:test --tests "*AllocationServiceTest"`

You are a senior Java test engineer. Your mission is to bring AllocationService test coverage to >=90% branch coverage with deterministic, fast unit tests.

<context>
## Project context
- Repo: `resource-management/`, module: `rms-service`
- Stack: Java 17, Spring Boot 3.2, JUnit 5, Mockito, AssertJ
- Conventions: see `CLAUDE.md` — naming: `methodName_scenario`, no records, AssertJ only
- Key domain: Allocation state machine: PROPOSED -> APPROVED -> ACTIVE -> ENDING -> ENDED (or CANCELLED)
</context>

## Done looks like

1. Every public method in `AllocationService` has >=1 happy-path + >=1 error-path test
2. State machine transitions fully covered: valid transitions succeed, invalid throw `BusinessRuleException`
3. `./gradlew :rms-service:test --tests "*AllocationServiceTest"` passes with 0 failures
4. No flaky tests — no `Thread.sleep`, no shared mutable state

## Gotchas

- `CurrentUserIdAspect` sets ThreadLocal from SecurityContext — `AbstractServiceTest` handles this, but raw `@ExtendWith(MockitoExtension.class)` won't
- DB triggers maintain `member_total_allocated` — do NOT assert on this field in unit tests (only in integration tests)
- `@Transactional(readOnly = true)` is on the service class — mutating methods need their own `@Transactional`

<constraints>
## Constraints
- Use `@ExtendWith(MockitoExtension.class)` with `@Mock` + `@InjectMocks`
- Priority if time-boxed: state machine transitions > CRUD happy paths > edge cases
- Do NOT add integration tests in this task (unit only)
</constraints>

## Execution plan

1. **Audit** — Read `AllocationService.java` and existing `AllocationServiceTest.java`. List every public method and note which are untested or under-tested.
2. **Design** — For each gap, write a one-line test name (`method_scenario`). Group by: state transitions, validation, CRUD.
3. **Implement** — Write tests in priority order. Before each batch, state which methods you're targeting and why.
4. **Verify** — Run `./gradlew :rms-service:test --tests "*AllocationServiceTest"`. If failures, diagnose and fix. After 2 failed fixes on the same test, reassess your approach.
5. **Report** — List: tests added, methods now covered, any gaps you chose to skip and why.

## Output format

- Per phase: brief progress line + files changed
- Final: markdown table of `method | test name | status (pass/skip+reason)`

## On failure

- **Wrong approach** (2 failed fixes): switch strategy, don't patch incrementally.
- **Blocked** (can't determine expected behavior): document the ambiguity, skip the test, flag it.

## Start now by:

1. Read `AllocationService.java` — list all public methods
2. Read existing test file — identify coverage gaps
3. Write tests for the 3 highest-priority state transitions first
```

**Why this works**: Measurable end state, project-specific gotchas the agent can't infer, positive constraints with clear defaults, verification loop with escalation, priority order for time-boxing.

---

## Before / After: SKILL.md description

### Before (weak)

```yaml
description: Helps with prompts.
```

### After (follows agentskills.io spec)

```yaml
description: >-
  Generates structured mission prompts for coding agents and optional SKILL.md
  drafts from a user's goal plus an example. Produces role, context, deliverables,
  constraints, verification loops, and failure handling. Use when the user wants
  to create an agent prompt, reverse-engineer an example prompt for a new task,
  turn a workflow into a reusable skill, or asks about prompt engineering for agents.
```

**Why**: Third person, includes both WHAT (generates prompts) and WHEN (creating agent prompts, reverse-engineering examples, building skills). Includes trigger keywords the agent can match against.

---

## Calibrating control: three levels

### High freedom (code review — multiple valid approaches)

```markdown
## Code review process

1. Check all database queries for SQL injection (use parameterized queries)
2. Verify authentication checks on every endpoint
3. Look for race conditions in concurrent code paths
4. Confirm error messages don't leak internal details
```

### Medium freedom (report — preferred pattern with flexibility)

````markdown
## Report structure

Use this template, adapting sections as needed:

```markdown
# [Analysis Title]

## Executive summary

[One-paragraph overview]

## Key findings

- Finding 1 with supporting data

## Recommendations

1. Specific actionable recommendation
```
````

### Low freedom (database migration — fragile, exact sequence)

````markdown
## Database migration

Run exactly this sequence:

```bash
python scripts/migrate.py --verify --backup
```

Do not modify the command or add additional flags.
````

---

## Sections typically present in a strong prompt

1. **Critical constraints box** — Top 3 non-negotiable rules in a quoted block. Models attend most to the start and end of context.
2. **Role + mission** — Single sentence each; role sets expertise and tone.
3. **Context** — Repo layout, modules, stack, tooling, **non-negotiable** project rules. Use `<context>` XML tags for Claude agents. Only what the agent doesn't already know.
4. **Done looks like** — Numbered measurable outcomes (not activities). "Tests pass" not "write tests".
5. **Gotchas** — Environment-specific facts that defy reasonable assumptions. Highest-value content in many prompts.
6. **Constraints** — Positive directives, non-goals, priority order, default tools. Use `<constraints>` XML tags for Claude agents.
7. **Execution plan** — Phased with reasoning prompts: "Before acting, state what you expect. After each result, reassess."
8. **Progress checklist** — For multi-step workflows. Agent copies and checks off items.
9. **Verification** — Explicit test/build commands + escalation rule (2 failures -> rethink).
10. **Output format** — What to emit per phase + final report structure.
11. **Failure & recovery** — Three tiers: wrong approach, blocked, long-running.
12. **Start now** — Concrete first steps targeting highest-risk work.

## Commands block (project-specific)

Repeat actual `./gradlew` or `yarn` lines from the repo docs; do not invent tasks.

## What to vary per new task

| Slot                 | Source                                                   |
| -------------------- | -------------------------------------------------------- |
| Role                 | User brief                                               |
| Repo paths           | User or workspace                                        |
| Stack versions       | User or `build.gradle` / `package.json`                  |
| Done looks like      | User goals, converted to measurable outcomes             |
| Gotchas              | User corrections, project CLAUDE.md, code review history |
| Critical constraints | Project CLAUDE.md + user brief                           |
| Control level        | Fragility of each section's task (see examples above)    |
| "Start now"          | Highest-risk or user-priority work                       |

## Anti-patterns

| Anti-Pattern                               | Why It Fails                                          | Fix                                                               |
| ------------------------------------------ | ----------------------------------------------------- | ----------------------------------------------------------------- |
| Vague deliverables ("improve tests")       | No measurable "done"; agent guesses scope             | State outcomes: ">=90% branch coverage, 0 failures"               |
| Over-explaining what the agent knows       | Wastes context tokens on common knowledge             | Only add what the agent would get wrong without being told        |
| Step-by-step without end state             | Breaks on unexpected situations                       | Lead with "done looks like", add steps only for ordering          |
| Presenting multiple tools as equal options | Agent wastes time deciding or tries several           | Pick a default, mention alternatives only for specific conditions |
| Missing gotchas section                    | Agent makes avoidable mistakes from false assumptions | Add concrete facts that defy reasonable assumptions               |
| Missing "do not change production"         | Agent may refactor prod code to make tests easier     | Add as critical constraint                                        |
| Commands that don't exist in the repo      | Agent wastes time on errors                           | Copy exact commands from CLAUDE.md or package.json                |
| 500+ token constraint lists                | Important rules get buried                            | Top 3 in critical constraints box; rest in `<constraints>`        |
| No verification step                       | Agent reports "done" with failing tests               | Always include: run tests -> diagnose -> 2-failure escalation     |
| No reasoning prompts between actions       | Blind tool-call chains, compounding errors            | "Before each action, state what you expect and why"               |
| Repeating same rule in 3 places            | Wastes tokens, creates contradictions on edit         | State once in the right section; critical rules in top box only   |
| Generic "think step by step"               | Too vague to change behavior                          | Specific: "Before each tool call, state what you expect to learn" |
| Deeply nested file references              | Agent partially reads files, misses info              | Keep references one level deep from SKILL.md                      |
| Time-sensitive information                 | Becomes wrong as time passes                          | Use "current method" / "old patterns" sections instead of dates   |

---

## Prompt quality checklist

Use before finalizing a **high-stakes or long-running** agent prompt.

### Content quality

- [ ] **Conciseness** — Every section justifies its token cost. No explanations of things the agent already knows.
- [ ] **Real expertise** — Instructions drawn from actual project artifacts/experience, not generic advice.
- [ ] **Critical constraints** — Top 3 rules in a quoted block at the very top of the prompt.
- [ ] **Role** — One line: who the agent is and what "done" means.
- [ ] **Context** — Repo/module paths, stack, links to docs. Use XML tags for Claude agents.
- [ ] **End state** — "Done looks like" with measurable outcomes (not "make it better").
- [ ] **Gotchas** — Environment-specific facts that defy reasonable assumptions.
- [ ] **Priorities** — If time runs out, what ships first is explicit.

### Control & structure

- [ ] **Calibrated control** — High freedom for flexible tasks, low freedom for fragile operations. Each section calibrated independently.
- [ ] **Constraints** — Positive rules preferred; non-goals stated; defaults over menus; no more than ~10 (or extract to a file).
- [ ] **Reasoning prompts** — Agent instructed to plan before each action and reflect after each result.
- [ ] **Verification loop** — Specific test/build command + "after 2 failed fixes, reassess approach."
- [ ] **Output format** — Headings/bullets/schema the agent must use; commands in fenced blocks.
- [ ] **Pattern / few-shot** — User's example honored, or one minimal good/bad snippet for the hardest part.
- [ ] **Tools & environment** — When to use each tool, when NOT to, verification after mutation.
- [ ] **Failure tiers** — Wrong approach (switch strategy), blocked (ask one question), long-running (checkpoint).

### Token budget & scannability

- [ ] **Token budget** — Instructions under ~2000 tokens / 500 lines. Stable context extracted to referenced files.
- [ ] **Progressive disclosure** — Large prompts reference detail files conditionally, not inline everything.
- [ ] **Scannability** — No filler paragraphs; critical rules not buried mid-prompt; no rule repeated in multiple sections.
- [ ] **Consistent terminology** — One term per concept throughout (not mixing "endpoint" / "URL" / "route").

### If generating a SKILL.md

- [ ] **Name** — Lowercase-hyphen, 1-64 chars, matches directory name.
- [ ] **Description** — Third person, WHAT + WHEN, trigger keywords, under 1024 chars.
- [ ] **Body** — Under 500 lines. Only what the agent wouldn't know.
- [ ] **References** — One level deep. Conditional triggers for when to read each file.
