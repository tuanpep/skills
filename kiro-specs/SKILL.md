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
Phase 1: Requirements/Bugfix   → approval gate
Phase 2: Design                 → approval gate
Phase 3: Tasks                  → approval gate
Phase 4: Execute                → implement all tasks
Phase 5: Review & Verify        → validate against spec
Phase 6: Complete               → final summary & status
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

### Phase 4: Execute

Proceed immediately after plan approval — no additional confirmation.

**Sequential mode:**
```
For each task:
  1. Mark [~] in tasks.md
  2. Read relevant source files
  3. Implement + write/run tests
  4. Mark [x] in tasks.md
  5. Brief status report
```

**Batch mode:** Run all required tasks in dependency order. Skip optional unless requested.

**Rules:**
- Read existing files before modifying
- Follow conventions from codebase exploration
- If a task reveals a spec gap, **pause** and propose a spec update
- Use TodoWrite to track progress across multiple tasks

### Phase 5: Review & Verify (auto-continues from Phase 4)

After all tasks are `[x]`, immediately run a **single consolidated pass**. Read `references/quality-gates.md` for the checklist. Do NOT skip this phase.

**Single-pass review** — For each source file touched during Phase 4:
1. **Spec compliance**: Map implementation to REQ-N.M. Flag missing/partial coverage.
2. **Design conformance**: Check component boundaries, data model, API design, error handling match `design.md`.
3. **Acceptance criteria**: Trace each Given/When/Then criterion. Verify a test covers it.

**Report as a checklist:**
```
- [x] REQ-1.1 — src/auth/login.ts:42
- [x] REQ-1.2 — src/auth/login.ts:67
- [ ] REQ-2.1 — MISSING ← needs fix
- [~] REQ-2.2 — PARTIAL: success only ← needs fix
```

**Then:**
- Run full test suite. Report pass/fail counts (unit, integration, PBT, E2E).
- Fix any failures before Phase 6.
- Evaluate all quality gates — all must pass.

### Phase 6: Complete (auto-continues from Phase 5)

1. **Update tasks.md** — Add status block at top:
   ```
   ## Status: COMPLETE
   - Completed: [date]
   - Spec compliance: All REQ-N.M verified
   - Tests: All passing
   - Remaining optional tasks: [list or "None"]
   ```

2. **Completion summary** to user:
   - What was built/fixed (one sentence)
   - Files created/modified
   - Requirements coverage: N/N verified
   - Test results
   - Optional tasks left undone, known limitations, follow-up items

3. **Archival** — Completed spec stays in `.kiro/specs/` as living documentation for future reference, regression context, and compliance audit trail.

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

## Updating Existing Specs (Refinement Cascade)

**Requirements changed** → Regenerate affected `design.md` sections → Regenerate affected `tasks.md` entries → Show diff summary before writing.

**Design changed** → Validate requirements feasibility → Re-derive affected requirements → Regenerate affected `tasks.md` → Show diff summary.

**Check task progress** → Read codebase against acceptance criteria → Mark implemented tasks `[x]`.

Always read current file before writing updates — avoid overwriting user edits.

---

## Multi-Spec Projects

Unlimited specs per repo, organized by feature. Each independent — teams work on different specs without conflicts. Reference specs in conversation with `#spec [spec-name]` to load full context.
