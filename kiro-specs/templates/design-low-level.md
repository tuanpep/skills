# Design: [Feature Name]

## Technical approach
[what + why]

## Algorithm / pseudocode
```text
fn process(input):
  validate(input)
  out = transform(input)
  save(out)
  return out
```

## Interfaces
```text
interface [Name] {
  method(param): Return
}
```

## Data structures
```text
struct [Name] {
  field: Type
}
```

## NFR targets (needed only)
- Latency: [target]
- Throughput: [target]
- Memory/CPU: [target]

## Properties
| Property | Source Req | Description |
| --- | --- | --- |
| P1 | REQ-1.1 | [invariant] |

## Errors + deps
- Errors: [key cases]
- Deps: [must-have only]
