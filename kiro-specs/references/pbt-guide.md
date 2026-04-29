# PBT (caveman quick)

## Property = invariant
Behavior true across many inputs, not one example.

Example test: `input X -> output Y`  
Example property: `for any valid input, invariant holds`.

## Map from EARS
| Req type | Property shape |
| --- | --- |
| `WHEN ... SHALL ...` | for any valid event input -> expected output |
| `WHILE ... SHALL ...` | for any time in state -> invariant holds |
| `IF ... THEN SHALL ...` | for any input matching condition -> expected behavior |

Record in `design.md`:
```text
| Property | Source Req | Description |
| P1 | REQ-1.1 | [invariant] |
```

## Task rules (hard)
- Link each property to `REQ-N.M`
- Run 100+ generated cases (or team standard)
- Ensure shrinking gives minimal counterexample on fail

## Bugfix property set
- Bug exists: fail pre-fix
- Fix works: pass post-fix
- No regression: pass before + after
