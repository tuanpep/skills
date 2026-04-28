---
name: caveman-architecture
description: >
  Practical architecture defaults. KISS/YAGNI first, C4-lite outputs,
  ADR-lite decisions, measurable guardrails, trigger-based complexity growth.
---

# Caveman Architecture

Goal: smallest system hits outcome now, easy evolve later.

## Use when
- system design, scaling, boundaries
- monolith vs services choice
- simplify overengineered design

## Order
1. Stakeholders + failure risk.
2. Requirements + constraints.
3. KISS now.
4. YAGNI (no speculative infra).
5. Lower coupling, higher cohesion.
6. Define growth triggers.

## Default
1. Modular monolith first.
2. One primary DB.
3. Sync for must-have flow.
4. Async/events for side effects or proven scale pain.
5. Cache/index/CDN only after bottleneck evidence.
6. Managed service > custom infra.

## Required inputs
- business goal + success metric
- scale envelope (users/RPS/data/growth)
- quality targets (latency/avail/RTO/RPO/error budget)
- security/privacy/compliance constraints
- team/ops maturity
- cost boundary

Missing input -> ask focused question.

## Option scoring
Rate Low/Med/High: reliability, security, performance, operability, cost, evolvability, sustainability (if needed).
Call top 2 drivers.

## Output shape (C4-lite)
1. Context: users/purpose/externals.
2. Containers: app/api/worker/db interactions.
3. Components: critical path only.
Include ownership + trust boundaries each level.

## Boundary rules
- 1 capability per boundary
- no shared DB across boundaries
- no circular deps
- API/event contracts, no reach-through
- explicit data/invariant ownership
- local tx first; saga/outbox only if unavoidable

## ADR-lite (major decisions)
- Context
- Decision
- Alternatives (<=3)
- Tradeoffs
- Consequences
- Status
One ADR = one decision.

## Reject complexity when
- microservices without scale/org need
- event-driven for simple CRUD
- multi-DB without data-shape proof
- rewrite before bottleneck fix
- abstraction with one impl
- multi-region/cloud without explicit need

## Baseline checks
1. Top 3 failure modes + fallback.
2. Backup/restore + recovery target.
3. Authn/authz + least privilege.
4. Logs/metrics/traces + key alerts.
5. Deploy/rollback + runbook owner.

## Workflow
1. Gather inputs.
2. Propose simplest viable design.
3. List top 3 risks + mitigations.
4. Define 3-5 fitness checks.
5. Show next step if load/team doubles.
6. Give smallest-first implementation order.

## Fitness checks
- API p95 + error SLO
- deploy freq + change failure rate
- MTTR + recurrence
- boundary/coupling violations
- cost per req/job

## Response format
1. Recommended design (single default)
2. Requirements/constraints snapshot
3. Why simplest now
4. Tradeoffs + explicit "not now"
5. Risks + baseline checks
6. Fitness checks + complexity triggers
7. First implementation steps
---
name: caveman-architecture
description: >
  Practical architecture defaults. KISS/YAGNI first, C4-lite output, ADR-lite
  decisions, measurable guardrails, trigger-based complexity growth.
---

# Caveman Architecture

Smallest system that hits target. Clear boundaries. Measure always.

## Use When

- system design / architecture / scaling / boundaries
- monolith -> services decisions
- reliability + scalability tradeoffs
- simplify overengineered design

## Decision Order

1. Stakeholders + failure risk.
2. Requirements + constraints.
3. KISS now.
4. YAGNI (no speculative infra).
5. Lower coupling.
6. Higher cohesion (1 capability/boundary).
7. Evolution path.

## Default Architecture

1. Modular monolith first.
2. One primary DB first.
3. Sync for mandatory flow.
4. Async/events only for side effects or proven need.
5. Cache/CDN/index only after bottleneck evidence.
6. Managed service > custom infra.
7. One deployable unless independent cadence required.

## Required Inputs Before Design

1. business goal + success metric
2. scale envelope (users/RPS/jobs/data/growth)
3. quality targets (latency/availability/RTO/RPO/error budget)
4. risk constraints (security/privacy/compliance)
5. team constraints (size/ownership/ops maturity)
6. cost boundary

Missing input -> ask focused questions.

## Score Options (Low/Med/High Fit)

- reliability
- security
- performance
- operability/observability
- cost
- evolvability
- sustainability (if relevant)

Call top 2 drivers.

## Output Shape (C4-Lite)

1. Context: users, purpose, externals.
2. Containers: app/service/api/worker/db + interactions.
3. Components: critical path only.

Per level include: responsibilities, data ownership, trust boundaries.

## Boundary Rules

- 1 business capability per boundary
- avoid shared DB
- no circular deps
- contracts via API/events, not internal reach-through
- explicit data/invariant ownership
- local tx first; saga/outbox only if distribution unavoidable

## ADR-Lite (Major Decisions)

- Context (2-4 lines)
- Decision (1-2 lines)
- Alternatives (<=3)
- Tradeoffs
- Consequences
- Status (proposed/accepted/superseded)

One ADR = one decision.

## Reject Complexity If

- microservices no clear scale/org need
- event-driven for simple CRUD
- multi-DB no proven shape need
- rewrite before fixing bottleneck
- heavy abstraction, one impl
- reliability patterns beyond SLO/risk need
- multi-region/cloud no explicit availability/regulatory need

## Baseline Checks (Always)

1. top 3 failure modes + fallback
2. backup/restore + recovery target
3. authn/authz + least privilege
4. logs/metrics/traces + key alerts
5. deploy/rollback + runbook owner

Cloud: map to Well-Architected pillars (ops, security, reliability, performance, cost, sustainability).

## Minimal Workflow

1. gather requirements/constraints/metrics
2. propose simplest viable design
3. list top 3 risks + mitigations
4. define 3-5 measurable fitness checks
5. show next step if load/team doubles
6. give smallest-first implementation order

## Fitness Checks (Required)

- API p95 + error SLO
- deploy frequency + change failure rate
- MTTR + incident recurrence
- boundary violation/coupling guard
- cost per req/job threshold

Automate in CI/monitoring when possible.

## Response Format

1. recommended design (single default)
2. requirements + constraints snapshot
3. why simplest now
4. explicit tradeoffs / not now
5. risk + baseline checks
6. fitness checks + trigger points
7. first implementation steps

## Trigger Examples (Add Complexity Only After Hit)

- API p95 above target sustained
- DB CPU/IO saturation at normal peak
- ownership coordination bottleneck
- coupled releases block cadence
- compliance requires stronger isolation/audit
- repeated error-budget burn (2+ periods)
