---
name: kiro-specs
description: >-
  Spec workflow for complex/risky work. Minimal words. Full traceability.
---

# Kiro Specs (caveman)

## Base mode
- Design rules: `caveman-architecture`
- Code rules: `caveman-code`
- Talk style: normal unless user asks caveman

## Use gate (30s)
Use specs if any:
- multi-module/interface
- contract/behavior unclear or changing
- risky bug/regression/security/compliance
- need `REQ-N.M` trace

Else quick coding.

## Start
1. classify: feature | bugfix
2. folder: `.kiro/specs/[kebab-name]/`
3. read only relevant code
4. run flow

## File set
- Feature: `requirements.md` -> `design.md` -> `tasks.md`
- Bugfix: `bugfix.md` -> `design.md` -> `tasks.md`

## Flow
1. Plan
2. Review gate
3. Execute
4. Verify
5. Complete

### 1) Plan
- use `templates/*`
- use refs only when needed:
  - `references/ears-notation.md`
  - `references/pbt-guide.md`
- output:
  - req/bugfix with numbered testable reqs
  - design: simplest now + "not now"
  - tasks: order + `REQ-N.M` mapping + verify step

### 2) Review gate
Show:
1. file paths
2. key decisions
3. top risks + mitigations
4. ask approval

No execute before explicit approval.

### 3) Execute
Per task:
1. smallest clear impl, follow project pattern
2. verify mapped `REQ-N.M`
3. run targeted tests
4. update task + coverage note

Fail loop:
- impl bug -> minimal fix -> rerun affected tests
- spec gap -> update spec first -> continue

### 4) Verify
- run required tests (targeted first; full suite for high risk/release critical)
- no untraced required `REQ-N.M`
- no unresolved critical risk
- open `references/quality-gates.md` only when gap found

### 5) Complete
Update `tasks.md` once:
```text
## Status: COMPLETE
- Completed: [date]
- Spec compliance: All required REQ-N.M verified
- Tests: [targeted/full] passing
- Remaining optional tasks: [list or "None"]
```

Final summary:
- one-line outcome
- files changed
- coverage N/N
- test result
- optional follow-ups

Keep completed spec in `.kiro/specs/`.

## Guardrails
- no complexity without trigger metric
- no abstraction with one consumer
- no optimization without measurement
- no new dep/config unless needed now
- one action -> verify
