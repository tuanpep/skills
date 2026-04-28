---
name: kiro-specs
description: >-
  Kiro-style spec-driven development workflow for AI agents. Use for complex
  features or risky bug fixes that need explicit requirements, design, tasks,
  execution traceability, and verification.
---

# Kiro Specs — Spec-Driven Development

## On Invocation

1. Clarify target: feature or bugfix.
2. Select mode:
   - Feature -> Requirements-First or Design-First.
   - Design-First -> High Level or Low Level.
   - Bugfix -> collect 4 facts: repro, current behavior, expected behavior, unchanged constraints.
3. Explore relevant code (skip greenfield).
4. Pick spec path: `.kiro/specs/[kebab-case-name]/`.
5. Run 6-phase flow. Write files to disk, not chat-only.

---

## When to Use Specs vs Quick Coding

| Use specs                           | Use quick coding          |
| ----------------------------------- | ------------------------- |
| Complex feature, high coordination  | Small obvious fix         |
| Risky bug / unclear root cause      | Typos / trivial logic fix |
| Prior regression from earlier fixes | Low-risk isolated change  |
| Compliance/doc traceability needed  | Exploratory prototype     |

---

## Token Optimization Defaults

Apply across all phases:

1. Carry only active `REQ-N.M`, active task, changed files.
2. Keep exact IDs/thresholds; cut prose first.
3. Keep static instructions first, run state last (cache friendly).
4. Read `references/*` only when required.
5. Prefer short checklists/tables.
6. Batch `tasks.md` status updates once.

Escalation policy for context pressure:

- Mild: shorten rationale.
- Moderate: keep failing traces + linked `REQ-N.M` only.
- Severe: pause, propose spec compaction.

---

## Spec Types

### Feature Spec

Files: `requirements.md` -> `design.md` -> `tasks.md`, then execute -> review -> complete.

**Requirements-First** (behavior known, architecture flexible):

- Phase 1 `requirements.md` (EARS) -> Phase 2 `design.md` -> Phase 3 `tasks.md`

**Design-First** (architecture constrained/known):

- Choose High Level or Low Level
- Phase 1 `design.md` -> Phase 2 `requirements.md` -> Phase 3 `tasks.md`

Import existing work when present (design docs, JIRA/Confluence reqs, diagram descriptions).

### Bugfix Spec

Files: `bugfix.md` -> `design.md` -> `tasks.md`, then execute -> review -> complete.

- `bugfix.md`: repro/current/expected/unchanged
- `design.md`: root cause, fix strategy, properties, risk
- `tasks.md`: steps + regression tests

---

## 6-Phase Workflow

```text
Phase 1-3: Plan (auto-chain) -> STOP for review
Phase 4: Execute + inline verification
Phase 5: Test + gap check
Phase 6: Complete + summary
```

Phases 1-3 auto-chain. One approval gate after Phase 3. Phases 4-6 auto-chain after approval.

### Phases 1–3: Planning (auto-chain)

Before writing:

- Requirements phase -> `references/ears-notation.md`
- Design phase -> `references/pbt-guide.md`
- Always use matching `templates/*`

After Phase 3, present plan summary:

1. List all 3 file paths written
2. Key decisions (requirements, architecture, task count)
3. Ask: **"Here's the full plan. Ready to proceed with implementation, or want changes?"**
4. Wait for explicit go-ahead

### Phase 4: Execute + Verify-as-you-go

Start immediately after plan approval.

For each task, in order:

1. Use acceptance criteria + linked `REQ-N.M` from memory (no per-task reread of `tasks.md`).
2. Read only files needed now.
3. Implement.
4. Verify linked `REQ-N.M` inline.
5. Write/run tests for that task.
6. Track `[task#, status, REQ coverage, file:line]`.

Rules: use TodoWrite for progress, skip unchanged files, pause on spec gap, batch one `tasks.md` status write at end.

### Phase 5: Test + Gap Check (auto-continues from Phase 4)

Phase 5 is lightweight catch-up after inline checks.

1. Run full tests once; report pass/fail counts (unit/integration/PBT/E2E).
2. Scan REQ coverage notes; flag untraced `REQ-N.M`.
3. Fix failures/gaps; rerun affected tests.

Read `references/quality-gates.md` only if a gap appears.

### Phase 6: Complete (auto-continues from Phase 5)

1. Update `tasks.md` once with status block:

```text
## Status: COMPLETE
- Completed: [date]
- Spec compliance: All REQ-N.M verified
- Tests: All passing
- Remaining optional tasks: [list or "None"]
```

2. Send completion summary (from working memory):
   - What was built/fixed (one sentence)
   - Files created/modified
   - Requirements coverage: N/N verified
   - Test results
   - Optional tasks left undone, known limitations, follow-up items

3. Keep completed spec in `.kiro/specs/` as living docs.

---

## Spec Organization

```text
.kiro/specs/
├── user-authentication/ (requirements.md, design.md, tasks.md)
├── checkout-flow/       (requirements.md, design.md, tasks.md)
└── payment-bug-2026-04/ (bugfix.md, design.md, tasks.md)
```

One spec per feature/bug. Kebab-case names. Include date in bugfix names.

---

## Updating Existing Specs / Multi-Spec Projects

Read `references/spec-management.md` only for existing-spec updates or multi-spec coordination.
