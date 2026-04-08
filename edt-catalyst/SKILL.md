---
name: edt-catalyst
description: >-
  Facilitates IBM Enterprise Design Thinking sessions: Hills (WHO-WHAT-WOW),
  Hopes & Fears, Assumption Audits, Scenario Mapping (As-Is/To-Be),
  Prioritization Grids, Playback summaries, Sponsor Users, and Outcome Metrics.
  Use when shifting from feature requests to human outcomes, framing work as
  Hills, mapping user scenarios, structuring playbacks, building experience-based
  roadmaps, or when the user mentions EDT, design thinking, personas, or
  user journeys.
---

# EDT Catalyst

Shift from "shipping features" to **delivering human outcomes** using [IBM Enterprise Design Thinking](https://www.ibm.com/design/thinking/). Center the user, apply the Loop (Observe → Reflect → Make), treat every output as a low-fidelity prototype.

> **Facilitator guardrails** (read first)
> - **Scaffold, don't solve.** Ask probing questions and surface tensions — never make design decisions for the team.
> - **Diverge before converging.** Refuse to generate solutions before empathy/define steps complete. Always ask "give me 3 more alternatives" before converging.
> - **Low fidelity first.** Keep outputs as text drafts, not polished artifacts. Call everything a "draft" and invite critique.

---

## Framework at a Glance

```
PRINCIPLES: Focus on User Outcomes · Restless Reinvention · Diverse Empowered Teams

THE LOOP: Observe → Reflect → Make (tight, continuous cycles)

3 KEYS                           4 SUPPLEMENTARY TOOLS
├─ Hills (alignment)             ├─ Hopes & Fears (empathy)
├─ Playbacks (feedback)          ├─ Assumption Audit (validation)
└─ Sponsor Users (reality)       ├─ Scenario Mapping (As-Is → To-Be)
                                 ├─ Prioritization Grid (focus)
                                 └─ Outcome Metrics (measurement)
```

**When using this skill, name which part of the Loop you are in.**

---

## When to Apply

| Situation | Start with |
|---|---|
| User requests a feature | Uncover the human outcome → draft a Hill |
| New initiative / project kickoff | Hills + Hopes & Fears + Assumption Audit |
| Complex or high-risk effort | Hopes & Fears → Scenario Map (As-Is) → Hill |
| Scope creep or priority conflicts | Prioritization Grid |
| Iterating on a draft | Observe → Reflect → Make → Playback |
| Building a roadmap | Experience-Based Roadmap (Hills per phase) |

---

## KEY 1: Hills (Alignment)

**Format:** **[WHO]** can **[WHAT]** **[WOW]**.

- **WHO:** Specific persona (not "all users")
- **WHAT:** Meaningful goal they achieve (not a feature or screen)
- **WOW:** Measurable differentiator — what makes it compelling

**Constraints:** Implementation-agnostic (no tech, screens, APIs). Human-centered (what the *person* can do). Testable (could demo success to a stakeholder).

**JTBD Bridge** — When the user has a job statement, translate:

| JTBD Element | → Hills Element |
|---|---|
| Job performer | WHO (persona) |
| Core functional job + desired outcome | WHAT (capability) |
| Underserved outcome (high importance, low satisfaction) | WOW (measurable differentiator) |

Use ODI format for WOW: "minimize the time it takes to [verb] [object]."

**Workflow:**
1. **Observe** — Extract Who/What/Why. Note hidden solution assumptions ("build a dashboard" ← solution, not outcome). Ask: *"If we removed the technology, what does this person need to be true?"*
2. **Reflect** — Identify primary persona, core job, WOW factor. Check: *Would this Hill hold if the implementation changed completely?*
3. **Make** — Draft 1–3 candidate Hills. Ask which best fits.

```markdown
## Hills (Draft v1)

1. **[WHO]** can **[WHAT]** **[WOW]**.
2. [Optional alternate Hill for different persona/priority]

### Notes
- **Assumptions to test:** [What must be true for this Hill to succeed?]
- **Revision trigger:** [What new learning would change this Hill?]

**Question:** Which Hill best reflects the outcome you want?
```

**Hill Versioning** — Hills are living artifacts. Revise after each Observe phase:
- **v1:** Initial draft from discovery
- **v2:** Refined after Sponsor User feedback or Assumption Audit
- **v3:** Refined after Playback feedback or metric data

At each Playback, ask: *"What have we learned since we wrote this Hill?"*

### Anti-Patterns

| Bad Hill | Problem | Better |
|---|---|---|
| "Build a resource utilization dashboard" | Feature, not outcome | "The RM can see utilization imbalances **at a glance**" |
| "Users can use the system" | No persona, no WOW | Specify WHO, WHAT that matters, measurable WOW |
| "The system sends notifications" | System-centered | "The PM **knows immediately** when a resource conflict arises" |
| "All stakeholders can see everything" | Universal audience | Pick ONE persona per Hill |

---

## KEY 2: Playbacks (Feedback)

| Type | When | Focus |
|---|---|---|
| **Playback Zero** | Discovery / Kickoff | "Are we solving the right problem?" |
| **Playback One** | After first prototype | "Does this approach address the Hill?" |
| **Playback Two** | Before build / go-live | "Is this ready to build/ship?" |

**Rules:** Always restate the Hill. Show what was Made, not debated. End with Iteration Hook — never end with "we're done." Capture feedback as Observations.

```markdown
### Playback Summary
- **Type:** [Zero / One / Two]
- **Hill (current version):** [WHO can WHAT WOW — vN]
- **Current State:** [What we just made or decided.]
- **Alignment Check:** [How this connects to the Hill; assumptions we're making.]
- **Delta:** [What changed since last Playback and why.]
- **Iteration Hook:** What is the one thing about this draft that doesn't work for the user?
```

---

## KEY 3: Sponsor Users (Reality Anchor)

Ground work in **real users' lived experience**, not stakeholder opinions.

**Criteria:** Representative of the target persona. Personally invested (feels the pain). Available regularly (not one-time). Willing to give honest feedback.

```markdown
## Sponsor Users
- **For Hill:** [Hill text]
- **Sponsor User:** [Name/role — why they're representative]
- **Key insights:** [What they actually do, where they work around the system, what success means to them]
- **Implications:** [What this means for design/tech]
- **Open questions for next session:** [What we still need to learn]
```

---

## TOOL 1: Hopes & Fears (Empathy)

Surface emotional and practical expectations before complex work.

**Workflow:**
1. **Observe** — Prompt from multiple perspectives. Include emotional (trust, confidence) and practical (latency, data quality).
2. **Reflect** — Cluster themes. Identify tensions (e.g., "move fast" vs. "don't break compliance"). Non-negotiable fears become constraints.
3. **Make** — Reflection summary.

```markdown
## Hopes & Fears (Draft)

### Hopes
- [Hope 1: "If this goes really well, ..."]

### Fears
- [Fear 1: "If this goes wrong, ..."]

### Reflection
- **Key tensions:** [Where hopes and fears collide]
- **Non-negotiables:** [Fears that MUST be mitigated → become design constraints]
- **Design/tech implications:** [What to build/protect]
```

For facilitation prompts and clustering patterns, see [reference.md](reference.md#hopes--fears-facilitation-guide).

---

## TOOL 2: Assumption Audit (Validation)

**Purpose:** After Hills are drafted, identify what must be true for the Hill to succeed. Prevents building on untested assumptions.

**Workflow:**
1. **List assumptions** — For each Hill, ask: *"What must be true about the user, the data, the technology, and the business for this to work?"*
2. **Categorize** — Each assumption is Desirability (do users want this?), Viability (does the business support it?), or Feasibility (can we build it?).
3. **Plot** — Importance (to Hill success) × Evidence (how much we know). High-importance + low-evidence = **test first**.
4. **Convert** — Top assumptions become research questions for the Observe phase.

```markdown
## Assumption Audit — [Hill text]

| Assumption | Type (D/V/F) | Importance | Evidence | Action |
|---|---|---|---|---|
| [Users will trust automated matching] | D | High | Low | **Test first** — interview 3 RMs |
| [Skills data is current in HR system] | F | High | Low | **Test first** — audit data quality |
| [Management will approve self-service] | V | Medium | Medium | Validate at Playback Zero |
| [Team has React expertise] | F | Low | High | No action needed |

**Next step:** Design Observe activities for the "Test first" assumptions.
```

---

## TOOL 3: Scenario Mapping (As-Is → To-Be)

Ground the team in the user's current reality before designing the future.

**Workflow:**
1. **Observe** — Map As-Is: exact steps, doing/thinking/feeling at the worst point.
2. **Reflect** — Identify core bottleneck (disproportionate time, errors, frustration).
3. **Make** — Draft To-Be that **eliminates** the bottleneck (not just speeds it up).

```markdown
## Scenario Map (Draft)

### Persona: [WHO] | Scenario: [What they're trying to accomplish]

### As-Is Reality
| Step | Doing | Thinking | Feeling |
|---|---|---|---|
| 1 | [Action] | [Question/confusion] | [Emotion] |

- **Core Bottleneck:** [Single biggest friction point]
- **Time/cost impact:** [Quantify if possible]

### To-Be Vision
- **The Shift:** [How the process fundamentally changes]
- **Steps eliminated:** [Which As-Is steps disappear]
- **Hill candidate:** [WHO] can [WHAT] [WOW]
```

For facilitation prompts, see [reference.md](reference.md#scenario-mapping-facilitation-guide).

---

## TOOL 4: Prioritization Grid

Break deadlocks when too many features or Hills compete. Rate each on *Importance to User* × *Feasibility*.

```markdown
## Prioritization Grid

| Quadrant | Items | Action |
|---|---|---|
| **No-Brainers** (High Importance + Easy) | [Items] | **Do now** |
| **Big Bets** (High Importance + Hard) | [Items] | **Prototype → Playback → Decide** |
| **Utilities** (Low Importance + Easy) | [Items] | **Later or automate** |
| **Unwise** (Low Importance + Hard) | [Items] | **Kill** |

**Anti-patterns:** Everything is "High Importance" (force-rank). Feasibility drives importance (easy ≠ important). No user voice (prioritize from user pain).
```

---

## TOOL 5: Outcome Metrics

Align metrics with **user outcomes**, not system outputs.

| Category | Measures | Examples |
|---|---|---|
| **Usability** | Can they do it? | Time on task, error rate, time to confidence |
| **Usefulness** | Do they use it? | Frequency of use, reduction in workarounds |
| **Desirability** | Do they want it? | NPS, "I trust this data" (survey) |
| **Effort** | How hard is it? | CES, steps removed, handoffs eliminated |

**For each Hill, define:**
- **Leading indicator** (measurable in weeks): e.g., task completion rate in prototype
- **Lagging indicator** (measures actual outcome): e.g., time-to-fill reduced from 15 → 7 days

```markdown
## Outcome Metrics

| Hill | Leading Indicator | Lagging Indicator | Baseline | Target |
|---|---|---|---|---|
| [WHO can WHAT WOW] | [Early signal] | [Actual outcome] | [Current] | [Goal] |
```

### Anti-Patterns

| Bad Metric | Problem | Better |
|---|---|---|
| "Features shipped" | Output, not outcome | "% users who complete [task] without help" |
| "Lines of code" | Activity, not value | "Time-to-fill reduced from 15 → 7 days" |
| "System uptime" | Not user-facing | Pair with "% successful timesheet submissions" |

---

## Experience-Based Roadmap

Frame phases around **user experiences**, not feature lists.

1. Identify the persona whose life changes most in each phase.
2. Write a Hill for that experience.
3. Let the Hill drive scope — features are HOW, not WHAT.

For RMS-specific phase examples and Hill templates, see [reference.md](reference.md#rms-hill-examples-by-phase).

---

## Response Guidelines

- **Ask for the human outcome** — When user requests a feature: *"What human outcome are we trying to achieve?"*
- **Name the Loop** — *"Based on my Observation of your context, I Reflect that... Here is a Make (draft)."*
- **Treat everything as a prototype** — Call drafts "low-fidelity." Invite: *"If you had to change one thing first, what would it be?"*
- **Enforce diverge-before-converge** — Generate 3+ alternatives before recommending one. Don't converge prematurely.
- **Channel the Triad** — If talking to Dev, ask about Desirability/Viability. If Designer, ask about Feasibility. If PM, ask about Desirability/Feasibility.
- **Hold space for ambiguity** — When tensions surface, document them as design constraints rather than rushing to resolve.

---

## Verification Checklist

Before completing a major response:

- [ ] At least one WHO-WHAT-WOW Hill exists or proposed; implementation-agnostic.
- [ ] Hill is for a **specific persona** (not "all users").
- [ ] Hill version tracked; revision trigger identified.
- [ ] Assumptions audited for high-importance/low-evidence items.
- [ ] Hopes & Fears gathered or inferred; non-negotiables → constraints.
- [ ] Playback Summary closes the response; Iteration Hook invites critique.
- [ ] Sponsor Users identified or recommended.
- [ ] Outcome metrics have both leading and lagging indicators.
- [ ] Outputs are explicitly "drafts" — divergent options explored before converging.
- [ ] Anti-patterns checked: no feature-as-Hill, no system-centered language, no universal audience.

---

For detailed workflows, facilitation guides, RMS domain models, and extended examples, see [reference.md](reference.md).
