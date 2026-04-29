# Quality gates (caveman)

| Gate | Pass check |
| --- | --- |
| Req quality | EARS valid, no vague wording |
| Design quality | main + error flow covered |
| Property mapping | each `REQ-N.M` has property/test |
| Task quality | each required task has accept + files |
| Impl done | required tasks done |
| Traceability | all required `REQ-N.M` traced |
| Tests | required suites green |
| Completion | `tasks.md` completion block added |

## Gap report template
```text
## Gap Report
- REQ gaps:
  - [ ] REQ-N.M [missing/partial] -> [fix]
- Failing tests:
  - [test]: [reason] -> [fix]
- Plan:
  1. [step]
  2. rerun affected tests
  3. confirm closed
```
