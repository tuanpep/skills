# Design: Bugfix for [Bug Title]

## Root Cause Analysis
[Detailed explanation of why the bug occurs — trace through the code path, identify the exact line/function where behavior diverges]

## Proposed Fix
[Approach to fix the issue — specific files and logic changes. Be surgical: change only what's necessary]

## Property-Based Test Properties

Three categories of properties validate the fix:

### Bug Exists (pre-fix verification)
These tests MUST fail before the fix is applied:
- `WHEN [condition] THEN [incorrect behavior]` — confirms the bug is reproducible
- For any [input in bug-triggering space], the system produces [incorrect result]

### Fix Works (post-fix verification)
These tests MUST pass after the fix is applied:
- `WHEN [condition] THEN [correct behavior]` — confirms the fix resolves the issue
- For any [input in bug-triggering space], the system produces [correct result]

### No Regressions (preservation verification)
These tests MUST pass both before AND after the fix:
- `WHEN [unchanged condition] THEN [existing behavior]` — confirms no side effects
- For any [input in unaffected space], the system continues to produce [expected result]

## Files to Modify
| File | Change |
|------|--------|
| `[path/to/file]` | [What changes and why] |
| `[path/to/test]` | [New/updated test cases — including PBT] |

## Risk Assessment
- **Risk level**: [Low/Medium/High]
- **Potential side effects**: [List anything that could be inadvertently affected]
- **Mitigation**: [How to detect or prevent unintended side effects]
- **Rollback plan**: [How to revert if the fix causes issues]
