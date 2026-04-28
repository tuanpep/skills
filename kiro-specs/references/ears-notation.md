# EARS Notation (Easy Approach to Requirements Syntax)

Use EARS patterns for every requirement. Choose the pattern that fits:

| Pattern      | Syntax                                                   | Use for                |
| ------------ | -------------------------------------------------------- | ---------------------- |
| Event-driven | `WHEN [event] THE SYSTEM SHALL [behavior]`               | Triggered actions      |
| State-driven | `WHILE [state] THE SYSTEM SHALL [behavior]`              | Continuous behaviors   |
| Conditional  | `IF [condition] THEN THE SYSTEM SHALL [behavior]`        | Unwanted/error cases   |
| Ubiquitous   | `THE SYSTEM SHALL [behavior]`                            | Always-true invariants |
| Optional     | `WHERE [feature is enabled] THE SYSTEM SHALL [behavior]` | Feature flags          |
| Compound     | `WHILE [state] WHEN [event] THE SYSTEM SHALL [behavior]` | State + trigger        |

## Examples

```
WHEN a user submits a form with invalid data THE SYSTEM SHALL display inline validation errors
WHILE a background sync is in progress THE SYSTEM SHALL show a loading indicator
IF authentication fails three consecutive times THEN THE SYSTEM SHALL lock the account for 15 minutes
THE SYSTEM SHALL encrypt all passwords using bcrypt with cost factor >= 12
WHERE the beta feature flag is enabled WHEN a user visits the dashboard THE SYSTEM SHALL show the new UI
```

## Bugfix Variant

For bugfix specs, use these three patterns:

- **Current Behavior (Defect):** `WHEN [condition] THEN the system [incorrect behavior]`
- **Expected Behavior:** `WHEN [condition] THEN the system SHALL [correct behavior]`
- **Unchanged Behavior:** `WHEN [condition] THEN the system SHALL CONTINUE TO [existing behavior]`

## Writing Tips

- Each requirement gets a unique ID: REQ-N.M (story N, requirement M)
- Every EARS requirement should map directly to a testable property
- Avoid ambiguous SHALL — be specific about the behavior
- Cover both happy path and error/edge cases
