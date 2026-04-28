---
name: caveman-code
description: >
  Practical coding defaults. Correctness + code health first. KISS/YAGNI.
  No speculative abstraction. Build now, refactor when pressure real.
---

# Caveman Code

Ship smallest clear code that works now. Keep future change easy.

## Use When

- "simple code", "less abstraction", "avoid overengineering"
- quick maintainable impl
- "ship simple first"
- caveman coding style (not chat style)

## Decision Order

1. correctness first
2. code health over clever local win
3. KISS
4. YAGNI
5. readable > clever
6. refactor when needed, not before

Aligns: Google code health, XP YAGNI, refactor-first evolution.

## Hard Rules

1. solve current req only
2. follow existing project patterns
3. no new layer (service/repo/adapter/factory/hook/helper) without immediate proof
4. no generic util for one caller
5. shallow call depth; no pass-through wrappers
6. split fn only when readability/testability improves
7. explicit domain names (`calculateInvoiceTotal` > `processData`)
8. straightforward control flow + plain data
9. add deps only when built-in/current deps insufficient
10. add config/env only for real behavior differences now
11. optimize only with evidence (measure/profile/incident)
12. tests cover changed behavior + touched failure paths

## Rule Of Three (Abstraction)

1. first: direct impl
2. second: allow small duplication if context differs
3. third stable repeat: extract minimal shared abstraction

Likely divergence soon -> do not extract early.

## Simplicity Checklist

- delete code, still meets req?
- remove abstraction layer?
- touch fewer files?
- replace generic framework with direct logic?
- every branch tied to current req?
- mid-level engineer reads fast?
- code health improved/preserved?

Any "yes" -> simplify more.

## Avoid

- speculative extensibility
- generic util one caller
- wrappers with zero behavior
- optimization without measured bottleneck
- unnecessary patterns
- config explosion
- hidden side effects/magic
- plugin/extensible arch without present use case

## Workflow

1. restate req one sentence
2. shortest clear path in existing structure
3. add/adjust tests (happy + relevant edge/failure)
4. remove dead code/needless wrappers
5. readability pass (names/flow/errors)
6. complexity pass (files/branches/deps/config delta)
7. explain: why simplest now, what deferred

## Review Gate (Block + Simplify If True)

- abstraction with one consumer
- extensibility point no concrete near-term req
- new dep to save few simple lines
- new config with one practical value
- optimization no bottleneck evidence

## Response Behavior

- give one preferred approach
- alternatives max 2, short
- call out overengineering risk when rejecting abstraction
- state deferred complexity explicitly: "not now, trigger = X"
- keep explanation concrete + short

## Decision Examples

**New endpoint + maybe future versions**
- do: current contract
- skip: versioning framework unless needed now

**Dup logic in 2 places**
- do: small shared fn
- skip: full service layer unless behaviors justify

**Perf concern no data**
- do: readable impl + light measurement
- skip: complex cache/pool before proven bottleneck

**"Make reusable for future"**
- do: ask concrete 2nd use case + timeline
- skip: hypothetical generic abstraction

**Reviewer asks extra polish not required now**
- do: merge when safe + code health up
- skip: delay for theoretical perfection
