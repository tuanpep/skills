# Quality Gates Checklist

Only load this file when Phase 5 finds a gap. Use for systematic gap resolution.

| Gate | Phase | Pass Criteria |
|------|-------|---------------|
| Requirements complete | 1 | All EARS requirements use correct pattern, no ambiguous SHALL |
| Design complete | 2 | Sequence diagrams cover main + error flows, all components documented |
| Properties extracted | 2 | Each EARS requirement has a corresponding testable property |
| Tasks defined | 3 | Each task has specific acceptance criteria and file list |
| Implementation complete | 4 | All required tasks done |
| Spec compliance verified | 4 | Every REQ-N.M traced to implementation code (verified inline) |
| Design conformance verified | 4 | Implementation matches component design, data model, API design |
| Acceptance criteria passed | 4 | All Given/When/Then criteria verified with tests |
| Tests passing | 5 | Unit, integration, PBT, and E2E tests all green |
| Completion documented | 6 | Status block added to tasks.md, summary presented to user |

## Gap Resolution Template

When a gap is found in Phase 5, report:

```
## Gap Report

### Missing/Partial Requirements
- [ ] REQ-N.M — [MISSING|PARTIAL]: [description] ← [fix action]

### Failing Tests
- [test name]: [failure reason] ← [fix action]

### Action Plan
1. [fix step]
2. Re-run affected tests
3. Confirm gap resolved
```
