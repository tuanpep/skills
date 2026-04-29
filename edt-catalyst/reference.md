# EDT Catalyst reference (caveman)

Use when `SKILL.md` not enough.

## 1) Hill fast flow
### Observe
1. extract who/goal/why from ask
2. mark solution words (`dashboard`, `API`, `button`) as assumptions
3. ask: if tech gone, what must stay true for user?

### Reflect
1. define concrete persona
2. define core job (human outcome)
3. define WOW metric (ODI: minimize/maximize)
4. verify implementation-agnostic
5. verify demo-able in 1 min

### Make
1. draft 1-3 Hills (WHO/WHAT/WOW)
2. offer variants if priorities conflict
3. ask user choose best-fit Hill
4. log assumptions + version

## 2) JTBD -> Hill
- Job performer -> WHO
- Functional job -> WHAT
- Underserved outcome -> WOW
- WOW must be measurable + observable

## 3) Assumption audit
Lenses:
- desirability: users want/adopt?
- viability: business/compliance supports?
- feasibility: tech/data/integration possible?

Grid:
- high importance + low evidence -> test first
- high importance + high evidence -> monitor
- low importance + low evidence -> defer
- low importance + high evidence -> proceed

Turn "test first" into research tasks (interview, data audit, prototype, compliance check).

## 4) Hopes & fears
- capture success hopes + failure fears
- cluster by theme: transparency/control/speed/trust/fairness
- hope-fear conflict = design constraint

## 5) Scenario mapping
- map As-Is step-by-step (doing/thinking/feeling/time/tools/handoffs)
- find bottleneck (time/errors/friction/handoff pain)
- design To-Be removing bottleneck, not polish-only

## 6) Playback types
- Playback Zero: kickoff -> right problem?
- Playback One: post prototype -> addresses Hill?
- Playback Two: pre-build/go-live -> ready?

Rules:
- start latest Hill
- show what made
- end iteration hook
- capture learning, version Hill if needed

## 7) AI anti-patterns
- premature converge -> force 3+ alternatives
- skip empathy -> require real observation evidence
- over-polish artifacts -> keep low fidelity
- erase tensions -> keep as constraints
- rush groan zone -> hold ambiguity longer
- AI decides priority -> present options, team decides
- generic output -> ground in project artifacts

## 8) RMS domain snapshot
Personas: Resource Manager, Delivery Lead, PM, Finance Ops, CxO, Individual Resource.

Common pains:
- availability visibility
- manual reconciliation/billing
- weak real-time KPI visibility

Core tensions:
- speed vs configurable depth
- automation vs manual override
- data completeness vs simple UX
- central control vs team autonomy

## 9) Outcome metrics
- usability: task time/success/error
- usefulness: adoption/key-flow frequency/workaround drop
- trust: confidence/NPS/satisfaction
- effort: steps/handoffs/time saved
- business: utilization/billing accuracy/margin/time-to-fill

Pair leading (weeks) + lagging (months) per Hill.

## 10) Common mistakes
- feature as Hill
- skip As-Is
- measure output count, not outcome
- "all users" persona
- no iteration hook
- ignore fears
- late sponsor user involvement
- no assumption audit

## 11) Facilitation prompts
- feature ask -> "what outcome for which persona?"
- scope creep -> "which Hill does this serve?"
- priority conflict -> "rate user importance x feasibility"
- review -> "what one thing still fails user?"
- metrics -> "how user knows life improved?"
