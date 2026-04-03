# Quality Gates Checklist

Evaluate each gate during Phase 5: Review & Verify. All must pass before Phase 6.

| Gate | Phase | Pass Criteria |
|------|-------|---------------|
| Requirements complete | 1 | All EARS requirements use correct pattern, no ambiguous SHALL |
| Design complete | 2 | Sequence diagrams cover main + error flows, all components documented |
| Properties extracted | 2 | Each EARS requirement has a corresponding testable property |
| Tasks defined | 3 | Each task has specific acceptance criteria and file list |
| Implementation complete | 4 | All required tasks marked `[x]` |
| Spec compliance verified | 5 | Every REQ-N.M traced to implementation code |
| Design conformance verified | 5 | Implementation matches component design, data model, API design |
| Acceptance criteria passed | 5 | All Given/When/Then criteria verified with tests |
| Tests passing | 5 | Unit, integration, PBT, and E2E tests all green |
| Completion documented | 6 | Status block added to tasks.md, summary presented to user |

## Review Report Template

```
## Phase 5 Review Report

### Spec Compliance
- [x] REQ-1.1 — Implemented in [file:line]
- [x] REQ-1.2 — Implemented in [file:line]
- [ ] REQ-2.1 — MISSING ← needs fix
- [~] REQ-2.2 — PARTIAL ← needs fix

### Design Conformance
- [x] Component boundaries match design
- [x] Data model matches schema
- [x] API endpoints match design table
- [x] Error handling covers all scenarios

### Test Results
- Unit: X/Y passed
- Integration: X/Y passed
- PBT: X/Y passed (or N/A)
- E2E: X/Y passed (or N/A)

### Quality Gates
- [x] All gates passed / [ ] Gates failing: [list]
```
