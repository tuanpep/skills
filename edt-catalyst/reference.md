# EDT Catalyst — Ultra Reference

Use when `SKILL.md` not enough detail.

## 1) Hill-Making Fast Flow

### Observe
1. Extract who/goal/why from request.
2. Mark solution words (`dashboard`, `API`, `button`) as assumptions.
3. Ask: if tech vanished, what must be true for user?

### Reflect
1. Define concrete persona.
2. Define core job (human outcome).
3. Define WOW metric (ODI: "minimize/maximize ...").
4. Verify implementation-agnostic.
5. Verify demo-able in 1 minute.

### Make
1. Draft 1-3 Hills (WHO/WHAT/WOW).
2. Offer variants if priorities conflict.
3. Ask user to choose best-fit Hill.
4. Log assumptions + version.

## 2) JTBD -> Hill
- Job performer -> WHO
- Functional job -> WHAT
- Underserved outcome -> WOW
- Validate WOW measurable + observable

## 3) Assumption Audit

Lenses:
- Desirability: users want/adopt?
- Viability: business/compliance supports?
- Feasibility: tech/data/integration possible?

Grid:
- High importance + low evidence -> test first
- High importance + high evidence -> monitor
- Low importance + low evidence -> defer
- Low importance + high evidence -> proceed

Convert "test first" into research tasks (interviews, data audit, prototype, compliance check).

## 4) Hopes & Fears
- Capture success hopes and failure fears.
- Cluster by theme: transparency, control, speed, trust, fairness.
- Hope vs fear conflict = design constraint, not contradiction to erase.

## 5) Scenario Mapping
- Map As-Is step-by-step (doing/thinking/feeling/time/tools/handoffs).
- Find bottleneck (time, errors, frustration, handoff pain).
- Design To-Be that removes bottleneck, not polish pain.

## 6) Playback Types
- Playback Zero: kickoff; "right problem?"
- Playback One: post-prototype; "addresses Hill?"
- Playback Two: pre-build/go-live; "ready?"

Rules:
- Start with latest Hill.
- Show what made.
- End with iteration hook.
- Capture new learning; version Hill if needed.

## 7) AI Facilitation Anti-Patterns
- Premature convergence -> force 3+ alternatives.
- Skipping empathy -> demand evidence from real observation.
- Over-polished artifacts -> keep low-fidelity text artifacts.
- Resolving tensions -> keep as constraints.
- Rushing groan zone -> hold ambiguity before deciding.
- AI deciding priorities -> present options; team decides.
- Generic output without context -> ground in project artifacts.

## 8) RMS Domain Snapshot

Key personas: Resource Manager, Delivery Lead, PM, Finance Ops, CxO, Individual Resource.

Common pains:
- availability visibility
- manual reconciliation/billing
- weak real-time KPI visibility

Core tensions:
- speed vs configurable depth
- automation vs manual override
- data completeness vs simple UX
- central control vs team autonomy

## 9) Outcome Metrics
- Usability: task time, success, error
- Usefulness: adoption, key-flow frequency, workaround drop
- Trust/desirability: confidence/NPS/satisfaction
- Effort: steps/handoffs/time saved
- Business: utilization, billing accuracy, margin, time-to-fill

Pair leading (weeks) + lagging (months) metrics per Hill.

## 10) Common Mistakes
- Feature as Hill
- Skip As-Is
- Measure output count, not user/business outcome
- "All users" persona
- No iteration hook
- Ignore fears
- Late sponsor user involvement
- No assumption audit

## 11) Facilitation Prompts
- Feature request -> "What outcome for which persona?"
- Scope creep -> "Which Hill does this serve?"
- Priority conflict -> "Rate user importance x feasibility."
- Review -> "What one thing still fails user?"
- Metrics -> "How user knows life improved?"

Reference companion to `SKILL.md`.
