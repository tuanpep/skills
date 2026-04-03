---
name: kiro-specs
description: Kiro-style spec-driven development workflow for AI agents. Full 6-phase lifecycle — plan (requirements, design, tasks), execute, review & verify, complete — using EARS notation and property-based testing. Use when building complex features, fixing critical bugs, or when structured planning and verified implementation are needed.
---

# Kiro Specs — Spec-Driven Development

## On Invocation

1. **Clarify intent** — If not already clear, ask:
   - What are we building or fixing? Feature or bug fix?
   - For features: Requirements-First (behavior known) or Design-First (architecture known)?
   - For Design-First: **High Level** (architecture, diagrams) or **Low Level** (pseudocode, algorithms)?
   - For bugs: Collect 4 elements — reproduction steps, current behavior, expected behavior, unchanged code constraints
   - Any existing designs, diagrams, or requirements to import?

2. **Explore the codebase** — Read relevant files to understand architecture, patterns, conventions, test frameworks. Skip for greenfield projects.

3. **Determine spec directory** — `.kiro/specs/[kebab-case-name]/`

4. **Execute the 6-phase workflow** — Phases 1–3 auto-chain without stopping. Present the full plan (all 3 spec files) for review after Phase 3. After approval, Phases 4–6 auto-chain to completion.

5. **Write files to disk** — Use the Write tool. Don't just show content in chat.

---

## When to Use Specs vs Quick Coding

| Use specs | Use quick coding |
|-----------|-----------------|
| Complex features needing structured planning | Exploratory prototyping |
| Bugs where regressions are costly or root cause is unclear | Simple fixes, typos, obvious logic errors |
| Previous fix attempts caused regressions | Scope is obvious and small |
| Multiple discrete tasks involved | No regression risk |
| Team collaboration or compliance documentation needed | |

---

## Spec Types

### Feature Spec

Files: `requirements.md` → `design.md` → `tasks.md`, then execute → review → complete.

**Requirements-First** — Behavior known, architecture flexible, product-driven, greenfield.
- Phase 1: `requirements.md` (EARS notation) → Phase 2: `design.md` → Phase 3: `tasks.md`

**Design-First** — Architecture decided, porting existing docs, strict constraints, feasibility exploration.
- Choose: **High Level** (system architecture, components, diagrams) or **Low Level** (pseudocode, interfaces, data structures)
- Phase 1: `design.md` → Phase 2: `requirements.md` (guaranteed feasible) → Phase 3: `tasks.md`

**Importing existing work:** Paste designs/architecture for Design-First Phase 1. Import JIRA/Confluence requirements for Requirements-First Phase 1. Describe PNG diagrams for `design.md`.

### Bugfix Spec

Files: `bugfix.md` → `design.md` → `tasks.md`, then execute → review → complete.

- Phase 1: `bugfix.md` — reproduction steps, current/expected/unchanged behaviors
- Phase 2: `design.md` — root cause, fix approach, PBT properties, risk assessment
- Phase 3: `tasks.md` — implementation steps with regression-prevention tests

---

## 6-Phase Workflow

```
Phase 1–3: Plan (auto-chain)    → STOP: review full plan
Phase 4: Execute + verify inline → implement tasks, verify REQ-N.M as you go
Phase 5: Test + gap check        → run tests, scan for missed requirements
Phase 6: Complete                 → update status, summary
```

Phases 1–3 auto-chain (no stops). Single approval gate after Phase 3. Phases 4–6 auto-chain after approval.

### Phases 1–3: Planning (auto-chain)

**Before writing each phase**, read the relevant reference:
- Phase 1 (requirements): Read `references/ears-notation.md` for EARS patterns
- Phase 2 (design): Read `references/pbt-guide.md` for property extraction
- Use the appropriate template from `templates/` for the file being written

Write all three spec files in sequence without stopping. After Phase 3, present a **plan summary**:
1. List all 3 file paths written
2. Summarize key decisions from each phase (requirements highlights, architecture choices, task count)
3. Ask: **"Here's the full plan. Ready to proceed with implementation, or want changes?"**
4. Wait for explicit go-ahead

### Phase 4: Execute + Verify-as-you-go

Proceed immediately after plan approval — no additional confirmation.

**For each task** (in dependency order):
```
1. Read task's acceptance criteria and linked REQ-N.M from memory (do NOT re-read tasks.md)
2. Read only the source files needed for this task
3. Implement the task
4. Verify inline: confirm implementation satisfies linked REQ-N.M and acceptance criteria
5. Write/run tests for this task only
6. Track: note [task #, status, REQ coverage, file:line] in working memory
```

**Token-saving rules:**
- Use TodoWrite for progress tracking — do NOT read/write tasks.md per task
- Only read source files you are about to modify — skip unchanged files
- Follow conventions from codebase exploration (already in context)
- If a task reveals a spec gap, **pause** and propose a spec update
- Batch all tasks.md status updates into a single write at the end of Phase 4

**After all tasks complete**, update tasks.md once with all statuses set to `[x]`.

### Phase 5: Test + Gap Check (auto-continues from Phase 4)

Phase 5 is lightweight — Phase 4 already verified each REQ-N.M inline. Phase 5 only catches what inline verification might miss.

1. **Run tests once** — Execute the full test suite. Report pass/fail counts (unit, integration, PBT, E2E).
2. **Gap scan** — Check the REQ coverage notes from Phase 4. Flag any REQ-N.M not yet traced to code. Do NOT re-read spec files unless a gap is found.
3. **Fix** — If tests fail or gaps exist, fix them. Re-run only affected tests.

Read `references/quality-gates.md` only if a gap is found and you need the full checklist.

### Phase 6: Complete (auto-continues from Phase 5)

1. **Update tasks.md** — Single write. Add status block at top:
   ```
   ## Status: COMPLETE
   - Completed: [date]
   - Spec compliance: All REQ-N.M verified
   - Tests: All passing
   - Remaining optional tasks: [list or "None"]
   ```

2. **Completion summary** to user (from working memory — no re-reads):
   - What was built/fixed (one sentence)
   - Files created/modified
   - Requirements coverage: N/N verified
   - Test results
   - Optional tasks left undone, known limitations, follow-up items

3. **Archival** — Completed spec stays in `.kiro/specs/` as living documentation.

---

## Spec Organization

```
.kiro/specs/
├── user-authentication/
│   ├── requirements.md, design.md, tasks.md
├── checkout-flow/
│   ├── requirements.md, design.md, tasks.md
└── payment-bug-2026-04/
    ├── bugfix.md, design.md, tasks.md
```

One spec per feature/bug. Kebab-case names. Include date in bugfix names. Version control alongside code.

---

## Updating Existing Specs / Multi-Spec Projects

Read `references/spec-management.md` when updating an existing spec or managing multiple specs. Not needed for new spec creation.
