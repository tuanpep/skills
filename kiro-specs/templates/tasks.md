# Tasks: [Feature Name]

| # | Task | Status | Required |
|---|------|--------|----------|
| 1 | [Task title with clear outcome] | [ ] | Yes |
| 2 | [Task title with clear outcome] | [ ] | Yes |
| 3 | [Task title with clear outcome] | [ ] | Yes |
| 4 | [Property-based tests for REQ-N.M] | [ ] | No |
| 5 | [Task title with clear outcome] | [ ] | No |

Status legend: `[ ]` pending · `[~]` in-progress · `[x]` done

## Task Details

### Task 1: [Title]
- **Description**: [What needs to be done and why]
- **Files to create/modify**:
  - `src/[path]/[file]` — [what changes and why]
- **Acceptance criteria**:
  - [ ] [Specific, verifiable check]
  - [ ] [Specific, verifiable check]
- **Dependencies**: None

### Task 2: [Title]
- **Description**: [What needs to be done and why]
- **Files to create/modify**:
  - `src/[path]/[file]` — [what changes and why]
- **Acceptance criteria**:
  - [ ] [Specific, verifiable check]
- **Dependencies**: Task 1

### Task 3: [Title]
- **Description**: [What needs to be done and why]
- **Files to create/modify**:
  - `src/[path]/[file]` — [what changes and why]
- **Acceptance criteria**:
  - [ ] [Specific, verifiable check]
- **Dependencies**: Task 2

### Task 4: Property-Based Tests
- **Description**: Implement PBT for key requirements to validate properties across input spaces
- **Properties to test**:
  - P1 (REQ-1.1): For any [input], when [condition], [invariant holds]
  - P2 (REQ-2.1): For any [input], when [condition], [invariant holds]
- **Files to create/modify**:
  - `tests/[path]/[file].property.test` — [property-based test implementations]
- **Acceptance criteria**:
  - [ ] Properties pass for all generated inputs (100+ iterations)
  - [ ] Shrinking produces minimal counter-examples on failure
- **Dependencies**: Task 1, Task 2

## Execution Order
1. Task 1 (no dependencies)
2. Task 2 (depends on Task 1)
3. Task 3 (depends on Task 2)
4. Task 4 — PBT (optional, parallelizable with Task 3)
5. Task 5 (optional)
