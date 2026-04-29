# EARS (caveman quick)

One req -> one pattern:

| Pattern | Syntax | Use |
| --- | --- | --- |
| Event | `WHEN [event] THE SYSTEM SHALL [behavior]` | triggered action |
| State | `WHILE [state] THE SYSTEM SHALL [behavior]` | continuous behavior |
| Conditional | `IF [condition] THEN THE SYSTEM SHALL [behavior]` | error/guard path |
| Ubiquitous | `THE SYSTEM SHALL [behavior]` | invariant |
| Optional | `WHERE [flag on] THE SYSTEM SHALL [behavior]` | feature flag |

## Bugfix trio
- Current defect: `WHEN [condition] THEN system [wrong behavior]`
- Expected: `WHEN [condition] THEN system SHALL [correct behavior]`
- Unchanged: `WHEN [condition] THEN system SHALL CONTINUE TO [existing behavior]`

## Rules (hard)
- ID format: `REQ-N.M`
- 1 req -> 1 testable property
- use specific behavior words, no vague SHALL
- Cover happy + edge/error paths
