# Tasks: [Feature Name]

| # | Task | Status | REQ | Required | Depends |
| --- | --- | --- | --- | --- | --- |
| 1 | [clear outcome] | [ ] | REQ-1.1 | Yes | - |
| 2 | [clear outcome] | [ ] | REQ-1.2 | Yes | 1 |
| 3 | [PBT task] | [ ] | REQ-1.1, REQ-1.2 | No | 1,2 |

Status: `[ ]` pending · `[~]` doing · `[x]` done

## Task template (copy per task)
### Task [N]: [Title]
- Why: [need now]
- Files: `[path]`, `[path]`
- Accept:
  - [ ] [verifiable check]
- Verify: `[test/lint/cmd]`

## Done block (update once)
```text
## Status: COMPLETE
- Completed: [date]
- Spec compliance: All required REQ-N.M verified
- Tests: [targeted/full] passing
- Remaining optional tasks: [list or "None"]
```
