# Design: Bugfix for [Bug Title]

## Root cause
[exact reason + fn/path]

## Fix plan
[smallest safe change. no extra refactor]

## Properties
### Bug exists (pre-fix fail)
- WHEN [condition] THEN [wrong behavior]

### Fix works (post-fix pass)
- WHEN [condition] THEN [correct behavior]

### No regression (before+after pass)
- WHEN [unchanged condition] THEN [same old good behavior]

## Files to modify
| File | Change |
| --- | --- |
| `[path]` | [logic change] |
| `[test path]` | [test update/add] |

## Risk
- Level: [Low/Med/High]
- Side effects: [list]
- Mitigation checks: [checks]
- Rollback: [steps]
