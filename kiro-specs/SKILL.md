---
name: kiro-specs
description: >-
  Kiro-style spec-driven development for complex features and risky bugfixes.
  Use explicit requirements, design, tasks, traceable execution, verification.
---

# Kiro Specs — Compressed

## On invocation
1. Clarify target: feature or bugfix.
2. Pick mode:
   - Feature: Requirements-First or Design-First.
   - Design-First: High Level or Low Level.
   - Bugfix: collect repro/current/expected/unchanged constraints.
3. Explore relevant code (skip greenfield).
4. Set spec path: `.kiro/specs/[kebab-case-name]/`.
5. Run 6 phases; write files to disk.

## Use specs vs quick coding
Use specs for complex/risky/multi-task/compliance work.
Use quick coding for small obvious low-risk isolated fixes.

## Token defaults
1. Keep only active `REQ-N.M`, active task, changed files.
2. Keep IDs/thresholds exact; compress prose first.
3. Static rules first, dynamic state last.
4. Read references only when needed.
5. Batch `tasks.md` status update once.

## Spec types

### Feature
Files: `requirements.md` -> `design.md` -> `tasks.md`.

- Requirements-First: behavior known, architecture flexible.
- Design-First: architecture constrained/known; high-level or low-level first.

### Bugfix
Files: `bugfix.md` -> `design.md` -> `tasks.md`.
- `bugfix.md`: repro/current/expected/unchanged
- `design.md`: root cause/fix/properties/risk
- `tasks.md`: steps + regression prevention tests

## 6-phase flow
```text
1-3 Plan (auto-chain) -> STOP for approval
4 Execute + inline verify
5 Test + gap check
6 Complete + summary
```

### Phases 1-3 (auto-chain)
Before writing:
- requirements phase -> `references/ears-notation.md`
- design phase -> `references/pbt-guide.md`
- use matching template in `templates/`

After phase 3, present:
1. paths of 3 created files
2. key requirement/design/task decisions
3. ask approval to implement

### Phase 4 execute
For each task:
1. Use acceptance criteria + linked `REQ-N.M` from memory.
2. Read only needed source files.
3. Implement.
4. Verify linked `REQ-N.M` inline.
5. Add/run task tests.
6. Track `[task#, status, REQ coverage, file:line]`.

Rules: no per-task reread of `tasks.md`; pause if spec gap; batch final task status write.

### Phase 5 test + gap
1. Run full test suite once; report unit/integration/PBT/E2E pass/fail.
2. Scan REQ coverage notes; flag untraced `REQ-N.M`.
3. Fix failures/gaps; rerun affected tests.
4. Read `references/quality-gates.md` only if gap found.

### Phase 6 complete
Update `tasks.md` once:
```text
## Status: COMPLETE
- Completed: [date]
- Spec compliance: All REQ-N.M verified
- Tests: All passing
- Remaining optional tasks: [list or "None"]
```

Send summary:
- built/fixed in one sentence
- files changed
- requirements coverage N/N
- test results
- remaining optional work / limits / follow-ups

Keep completed spec in `.kiro/specs/`.

## Spec organization
One spec per feature/bug. Kebab-case names. Date in bugfix names.

## Existing/multi-spec work
Read `references/spec-management.md` only for existing-spec updates or multi-spec coordination.
