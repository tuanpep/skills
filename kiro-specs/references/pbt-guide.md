# Property-Based Testing (PBT) Guide

## What is a Property?

A universal statement about system behavior — an invariant that holds regardless of specific data. Each EARS requirement maps to a property.

**Traditional test:** "User adds car X to favorites -> car X appears in list"
**Property:** "For ANY user and ANY car, WHEN added to favorites, it appears in the user's list"

PBT tests hundreds of input combinations automatically, using "shrinking" to find minimal counter-examples.

## Extracting Properties from EARS Requirements

During the Design phase, extract one property per EARS requirement:

| EARS Requirement                                  | Property                                                           |
| ------------------------------------------------- | ------------------------------------------------------------------ |
| `WHEN [event] THE SYSTEM SHALL [behavior]`        | For any valid [event input], the system produces [behavior output] |
| `WHILE [state] THE SYSTEM SHALL [behavior]`       | For any moment during [state], [behavior] holds                    |
| `IF [condition] THEN THE SYSTEM SHALL [behavior]` | For any input matching [condition], the system produces [behavior] |

Record in design.md as:

```
| Property | Source Req | Description |
|----------|-----------|-------------|
| P1 | REQ-1.1 | For any [input space], when [condition], [invariant] |
| P2 | REQ-1.2 | For any [input space], while [state], [invariant] |
```

## PBT in Tasks

Include as optional task in tasks.md:

- Link each property to its source REQ-N.M
- Target 100+ generated input iterations
- Verify shrinking produces minimal counter-examples on failure

## PBT for Bugfix Specs

Three property categories:

| Category           | When it must hold       | Purpose                         |
| ------------------ | ----------------------- | ------------------------------- |
| **Bug exists**     | FAILS before fix        | Confirms bug is reproducible    |
| **Fix works**      | PASSES after fix        | Confirms fix resolves the issue |
| **No regressions** | PASSES before AND after | Confirms no side effects        |
