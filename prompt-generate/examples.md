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

**Problems**: No repo context, no measurable "done", vague deliverables ("edge cases"), no failure handling, no verification loop, no priority order.

### After (structured)

````markdown
> **Critical constraints** (read first)
> - Do NOT modify production code unless a failing test proves a bug
> - All new tests extend `AbstractServiceTest` and use `TestDataBuilder`
> - All tests must pass: `./gradlew :rms-service:test --tests "*AllocationServiceTest"`

You are a senior Java test engineer. Your mission is to bring AllocationService test coverage to ≥90% branch coverage with deterministic, fast unit tests.

<context>
## Project context
- Repo: `resource-management/`, module: `rms-service`
- Stack: Java 17, Spring Boot 3.2, JUnit 5, Mockito, AssertJ
- Conventions: see `CLAUDE.md` — naming: `methodName_scenario`, no records, AssertJ only
- Key domain: Allocation state machine: PROPOSED → APPROVED → ACTIVE → ENDING → ENDED (or CANCELLED)
</context>

## Done looks like
1) Every public method in `AllocationService` has ≥1 happy-path + ≥1 error-path test
2) State machine transitions fully covered: valid transitions succeed, invalid throw `BusinessRuleException`
3) `./gradlew :rms-service:test --tests "*AllocationServiceTest"` passes with 0 failures
4) No flaky tests — no `Thread.sleep`, no shared mutable state

<constraints>
## Constraints
- Use `@ExtendWith(MockitoExtension.class)` with `@Mock` + `@InjectMocks`
- Priority if time-boxed: state machine transitions > CRUD happy paths > edge cases
- Do NOT add integration tests in this task (unit only)
</constraints>

## Execution plan
1) **Audit** — Read `AllocationService.java` and existing `AllocationServiceTest.java`. List every public method and note which are untested or under-tested.
2) **Design** — For each gap, write a one-line test name (`method_scenario`). Group by: state transitions, validation, CRUD.
3) **Implement** — Write tests in priority order. Before each batch, state which methods you're targeting and why.
4) **Verify** — Run `./gradlew :rms-service:test --tests "*AllocationServiceTest"`. If failures, diagnose and fix. After 2 failed fixes on the same test, reassess your approach.
5) **Report** — List: tests added, methods now covered, any gaps you chose to skip and why.

## Output format
- Per phase: brief progress line + files changed
- Final: markdown table of `method | test name | status (pass/skip+reason)`

## On failure
- **Wrong approach** (2 failed fixes): switch strategy, don't patch incrementally.
- **Blocked** (can't determine expected behavior): document the ambiguity, skip the test, flag it.

## Start now by:
1) Read `AllocationService.java` — list all public methods
2) Read existing test file — identify coverage gaps
3) Write tests for the 3 highest-priority state transitions first
````

---

## Sections typically present in a strong prompt

1. **Critical constraints box** — Top 3 non-negotiable rules in a quoted block. Models attend most to the start and end of context.
2. **Role + mission** — Single sentence each; role sets expertise and tone.
3. **Context** — Repo layout, modules, stack, tooling, **non-negotiable** project rules. Use `<context>` XML tags for Claude agents.
4. **Done looks like** — Numbered measurable outcomes (not activities). "Tests pass" not "write tests".
5. **Constraints** — Positive directives, non-goals, priority order. Use `<constraints>` XML tags for Claude agents.
6. **Execution plan** — Phased with reasoning prompts: "Before acting, state what you expect. After each result, reassess."
7. **Verification** — Explicit test/build commands + escalation rule (2 failures → rethink).
8. **Output format** — What to emit per phase + final report structure.
9. **Failure & recovery** — Three tiers: wrong approach, blocked, long-running.
10. **Start now** — Concrete first steps targeting highest-risk work.

## Commands block (project-specific)

Repeat actual `./gradlew` or `yarn` lines from the repo docs; do not invent tasks.

## What to vary per new task

| Slot | Source |
|------|--------|
| Role | User brief |
| Repo paths | User or workspace |
| Stack versions | User or `build.gradle` / `package.json` |
| Done looks like | User goals, converted to measurable outcomes |
| Critical constraints | Project CLAUDE.md + user brief |
| "Start now" | Highest-risk or user-priority work |

## Anti-patterns

| Anti-Pattern | Why It Fails | Fix |
|---|---|---|
| Vague deliverables ("improve tests") | No measurable "done"; agent guesses scope | State outcomes: "≥90% branch coverage, 0 failures" |
| Step-by-step without end state | Breaks on unexpected situations | Lead with "done looks like", add steps only for ordering |
| Missing "do not change production" | Agent may refactor prod code to make tests easier | Add as critical constraint |
| Commands that don't exist in the repo | Agent wastes time on errors | Copy exact commands from CLAUDE.md or package.json |
| 500+ token constraint lists | Important rules get buried | Top 3 in critical constraints box; rest in `<constraints>` |
| No verification step | Agent reports "done" with failing tests | Always include: run tests → diagnose → 2-failure escalation |
| No reasoning prompts between actions | Blind tool-call chains, compounding errors | "Before each action, state what you expect and why" |
| Repeating same rule in 3 places | Wastes tokens, creates contradictions on edit | State once in the right section; critical rules in top box only |
| Generic "think step by step" | Too vague to change behavior | Specific: "Before each tool call, state what you expect to learn" |

---

## Prompt quality checklist

Use before finalizing a **high-stakes or long-running** agent prompt.

- [ ] **Critical constraints** — Top 3 rules in a quoted block at the very top of the prompt.
- [ ] **Role** — One line: who the agent is and what "done" means.
- [ ] **Context** — Repo/module paths, stack, links to docs. Use XML tags for Claude agents.
- [ ] **End state** — "Done looks like" with measurable outcomes (not "make it better").
- [ ] **Priorities** — If time runs out, what ships first is explicit.
- [ ] **Constraints** — Positive rules preferred; non-goals stated; no more than ~10 (or extract to a file).
- [ ] **Reasoning prompts** — Agent instructed to plan before each action and reflect after each result.
- [ ] **Verification loop** — Specific test/build command + "after 2 failed fixes, reassess approach."
- [ ] **Output format** — Headings/bullets/schema the agent must use; commands in fenced blocks.
- [ ] **Pattern / few-shot** — User's example honored, or one minimal good/bad snippet for the hardest part.
- [ ] **Tools & environment** — When to use each tool, when NOT to, verification after mutation.
- [ ] **Failure tiers** — Wrong approach (switch strategy), blocked (ask one question), long-running (checkpoint).
- [ ] **Token budget** — Instructions under ~2000 tokens. Stable context extracted to referenced files, not inlined.
- [ ] **Scannability** — No filler paragraphs; critical rules not buried mid-prompt; no rule repeated in multiple sections.
