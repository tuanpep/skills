# EDT Catalyst — Reference Guide

Extended workflows, facilitation guides, domain examples, and decision aids. Load when the agent needs more depth than SKILL.md provides.

---

## Part 1: Detailed Workflows

### Hill-Making: Step-by-Step

**Observe**

1. Extract from the request: Who is impacted? What are they trying to accomplish? Why does it matter?
2. Note hidden solution assumptions — watch for words like "dashboard", "API", "page", "button", "notification". These are solutions, not outcomes.
3. Ask: _"If we removed the technology entirely, what does this person need to be true?"_

**Reflect**

1. Identify: Primary persona (WHO) — be specific. "Manager" is too broad; "Resource Manager handling 30+ allocations" is actionable.
2. Identify: Core job/outcome (WHAT) — the human goal, not the system feature.
3. Identify: WOW — meaningful improvement. Use ODI format: "minimize the time it takes to [verb] [object]."
4. Check: Would the statement still be true if the implementation changed? If not, it's a feature, not a Hill.
5. Check: Could this Hill be demoed to a stakeholder in 1 minute? If not, break it down.

**Make**

1. Draft 1-3 candidate Hills in WHO-WHAT-WOW format.
2. If competing priorities exist, offer variants: one for end-user, one for manager.
3. Ask explicitly: _"Which Hill best matches the outcome you want?"_
4. Document assumptions to test. Assign version (v1).

### JTBD-to-Hill Translation

When the user starts with a Jobs-to-be-Done statement:

1. **Identify the job performer** → WHO
2. **Extract the core functional job** (what they're trying to accomplish) → WHAT
3. **Find the underserved outcome** (high importance, low satisfaction) → WOW
4. **Validate:** Is the WOW measurable? Can you observe it? Does it satisfy: "minimize/maximize [metric] when [context]"?

**Example:**

- JTBD: "When managing 30+ resources across projects, minimize the time it takes to find a skill-matched available person"
- Hill: "The **Resource Manager** can **find the best-fit resource for a project request** **by searching skills, level, and availability in a single query — in minutes, not days**."

---

### Assumption Audit: Facilitation Guide

**Step 1: Generate assumptions.** For each Hill, ask across three lenses:

| Lens             | Prompt                                                          |
| ---------------- | --------------------------------------------------------------- |
| **Desirability** | "Do users actually want this? Will they change their behavior?" |
| **Viability**    | "Does the business support this? Budget, timeline, compliance?" |
| **Feasibility**  | "Can we build this? Data quality, integrations, skills?"        |

**Step 2: Plot on the grid.**

```
                    High Importance
                         │
          TEST FIRST     │     MONITOR
        (research now)   │   (track during build)
                         │
   Low Evidence ─────────┼───────── High Evidence
                         │
          DEFER          │     SAFE TO PROCEED
        (revisit later)  │   (no action needed)
                         │
                    Low Importance
```

**Step 3: Convert to research questions.** Each "Test First" assumption becomes an Observe activity:

- Interview 3 sponsor users
- Audit data quality
- Prototype the riskiest interaction
- Check compliance requirements

**Common assumption traps:**

- "Users will adopt it because it's better" — adoption requires behavior change, not just better features
- "The data is clean enough" — always audit before assuming
- "Stakeholders are aligned" — run a Playback Zero to verify

---

### Hopes & Fears: Facilitation Guide

**Prompting Questions (Observe):**

For Hopes:

- "If this project goes really well, what will be true in 6 months?"
- "What's the best possible outcome for the [persona]?"
- "What would make this project worth celebrating?"

For Fears:

- "If this goes wrong, what are you most worried about?"
- "What could make users abandon this system?"
- "What's the worst thing that could happen to data integrity / trust / adoption?"

**Clustering (Reflect):**

Common theme clusters:

- **Transparency** — "I want to see how decisions are made" / "I fear black-box logic"
- **Control** — "I want to manage my own data" / "I fear the system decides for me"
- **Speed** — "I want instant feedback" / "I fear it's slower than Excel"
- **Trust** — "I want to believe the data" / "I fear nobody will update it"
- **Fairness** — "I want objective allocation" / "I fear favoritism in assignments"

**Tension Resolution:**
When a Hope directly contradicts a Fear, this is a **design constraint**, not a contradiction to resolve. Both must be true. Document it and let it shape the solution.

---

### Scenario Mapping: Facilitation Guide

**As-Is Mapping Prompts:**

- "Walk me through the last time you [did this task]. Step by step."
- "Where did you get stuck? What did you have to work around?"
- "How long did it actually take vs. how long it should take?"
- "What tools did you switch between? Where did data get re-entered?"

**Identifying the Bottleneck:**

- Look for: disproportionate time, error points, emotional frustration, handoffs between people/systems.
- Ask: _"If you could magically fix ONE step, which one?"_

**To-Be Design:**

- The To-Be should **eliminate the bottleneck**, not just speed it up.
- Good: "The system auto-compares timesheets and highlights discrepancies."
- Bad: "The system makes it easier to manually compare spreadsheets." (polishes the pain)

---

### Playback Types: When to Use What

| Type              | Stage                  | Duration  | Audience                     | Focus                                  |
| ----------------- | ---------------------- | --------- | ---------------------------- | -------------------------------------- |
| **Playback Zero** | Discovery / Kickoff    | 15-30 min | Sponsor, stakeholders, team  | "Are we solving the right problem?"    |
| **Playback One**  | After first prototype  | 30-45 min | Sponsor, sponsor users, team | "Does this approach address the Hill?" |
| **Playback Two**  | Before build / go-live | 30-60 min | Full stakeholder group       | "Is this ready?"                       |

**Rules:**

- Always start by restating the Hill (current version).
- Show what was Made, not what was debated.
- End with Iteration Hook — never end with "we're done."
- Ask: _"What have we learned since we wrote this Hill?"_ — update version if needed.
- Capture feedback as Observations for the next Loop.

---

## Part 2: AI Facilitation Anti-Patterns

These are specific failure modes when an AI agent runs design thinking sessions. Build these into your facilitation approach:

| Anti-Pattern                   | Why It Fails                                                        | Guardrail                                                                     |
| ------------------------------ | ------------------------------------------------------------------- | ----------------------------------------------------------------------------- |
| **Premature convergence**      | AI generates solutions too fast; team fixates on first answer       | Always generate 3+ alternatives before recommending one                       |
| **Skipping empathy**           | Team says "we already know the user" — AI accepts it                | Insist on evidence: "When did you last observe this user doing this task?"    |
| **Over-polished artifacts**    | High-fidelity AI output causes design fixation                      | Keep all outputs as text, markdown tables, bullet lists — not mockups         |
| **Resolving tensions**         | AI tries to "solve" the contradiction between a Hope and Fear       | Document tensions as design constraints, don't resolve them                   |
| **Missing the groan zone**     | AI rushes through the uncomfortable divergent→convergent transition | Hold space for ambiguity: "Let's sit with these 4 options before choosing"    |
| **Making design decisions**    | AI picks the "best" Hill or priority                                | Always present options and ask the team to decide                             |
| **Generating without context** | AI produces generic EDT artifacts from training data                | Always ground in project-specific artifacts, sponsor user insights, real data |

---

## Part 3: RMS Domain Models

### RMS Personas for EDT

| Persona                     | Role                                       | Primary Pain                                             | Hill Focus                                         |
| --------------------------- | ------------------------------------------ | -------------------------------------------------------- | -------------------------------------------------- |
| **Resource Manager (RM)**   | Manages resource pool, allocation requests | Can't see availability; matches skills manually in Excel | Visibility, speed, utilization                     |
| **Delivery Lead (DL)**      | Project delivery, client relationships     | No margin visibility until month-end                     | Real-time health, margin, early risk detection     |
| **Project Manager (PM)**    | Execution, timesheets, deliverables        | Days on manual timesheet reconciliation                  | Accuracy, automation, less admin                   |
| **Finance Ops Analyst**     | Billing, invoicing, payments               | Manual invoice creation; billing errors                  | Billing accuracy, faster cycle, revenue visibility |
| **CxO / Senior Management** | Strategic decisions, portfolio oversight   | No KPIs, no dashboards — gut-feeling decisions           | Utilization, profitability, forecasting            |
| **Individual Resource**     | Engineers, consultants on projects         | Doesn't know allocation schedule; manual timesheets      | Self-service: see assignments, submit time         |

### RMS Hill Examples by Phase

**Phase 1 — Foundation:**

1. "The **Resource Manager** can **see every team member's current status, skills, and availability** **without opening a single spreadsheet, updating in real time**."
2. "The **Delivery Lead** can **register a new project and define resource requirements** **so the matching process starts within hours, not days**."
3. "The **Resource Manager** can **find the best-fit resource for a project request** **by searching skills, level, and availability in a single query**."

**Phase 2 — Operations:** 4. "The **PM** can **reconcile internal timesheets against client records** **with automated comparison that catches 100% of discrepancies**." 5. "The **Finance Analyst** can **generate accurate invoices from approved timesheets** **in minutes instead of days, with zero manual data transfer**." 6. "The **Individual Resource** can **submit timesheets and view project assignments** **through a self-service portal, without emailing anyone**."

**Phase 3 — Intelligence:** 7. "The **CxO** can **see portfolio utilization, profitability, and staffing forecasts** **on a single dashboard, updated in real time**." 8. "The **Resource Manager** can **predict resource needs 3 months ahead** **based on pipeline data, so hiring starts before gaps become crises**."

> **Note:** Phase 1 core is currently implemented (Dashboard, Resources, Projects, Allocations, Certifications, Checkpoints, Analytics, Master Data, Knowledge Base). Phase 2-3 Hills are aspirational.

### RMS Hopes & Fears (Pre-collected)

**Hopes:**

- "We finally know who's available without asking 5 people."
- "One system replaces all the spreadsheets."
- "Billing errors drop to near zero."
- "We can see project profitability in real time."
- "New hires can onboard to projects faster."

**Fears:**

- "The system becomes another spreadsheet nobody trusts."
- "Data quality is so bad nobody uses it."
- "It's so complex that adoption fails — people go back to Excel."
- "Managers game the utilization numbers."
- "Client-specific rules can't be configured — hard-coded logic."
- "Integration with existing systems (CRM, ATS, HR) is brittle."

**Key Tensions:**

- Speed of deployment ↔ Depth of configuration per client
- Automation ↔ Manual override for edge cases
- Comprehensive data ↔ Simple UX people actually use
- Centralized control ↔ Team-level autonomy

---

## Part 4: Outcome Metric Patterns (Expanded)

### By Category

| Category                 | What It Measures         | Example Metrics                                                        |
| ------------------------ | ------------------------ | ---------------------------------------------------------------------- |
| **Usability**            | Can they do it?          | Time on task, task success rate, error rate, SUS score                 |
| **Usefulness**           | Do they use it?          | Active users / target, frequency of key flows, workaround reduction    |
| **Desirability / Trust** | Do they want it?         | NPS, satisfaction, "I trust this data" (survey), adoption rate         |
| **Effort**               | How hard is it?          | CES, steps removed, handoffs eliminated, time saved                    |
| **Business Outcome**     | Does it move the needle? | Revenue per resource, utilization rate, billing accuracy, time-to-fill |

### Leading vs Lagging Indicators

| Hill                     | Leading (weeks)                      | Lagging (months)                       |
| ------------------------ | ------------------------------------ | -------------------------------------- |
| RM sees availability     | Prototype task completion rate       | Time-to-fill (days → hours)            |
| PM reconciles timesheets | Error detection rate in testing      | Hours/month on reconciliation (40 → 8) |
| CxO sees dashboard       | Time to generate report in prototype | Decision response time improvement     |

**Always pair user metrics with business metrics** — keeps Design and Business voices in the conversation.

---

## Part 5: Common Mistakes & How to Avoid Them

| Mistake                     | Problem                                         | Fix                                            |
| --------------------------- | ----------------------------------------------- | ---------------------------------------------- |
| Features as Hills           | "Build allocation dashboard with drag-and-drop" | Reframe: "What does the RM need to be true?"   |
| Skipping As-Is              | Solutions that miss the real bottleneck         | Always map As-Is first                         |
| Measuring output            | "12 features shipped this sprint"               | "Utilization improved from 67% to 74%"         |
| Universal audience          | "All users can manage resources"                | ONE persona per Hill                           |
| No Iteration Hook           | Kills the Loop                                  | Always ask: "What doesn't work for the user?"  |
| Ignoring Fears              | Fears = what to protect against                 | Every non-negotiable Fear → design constraint  |
| Sponsor Users as validators | "Show them the finished design"                 | Bring them in during sketching                 |
| No Assumption Audit         | Building on untested beliefs                    | Plot assumptions on importance × evidence grid |

---

## Part 6: Facilitation Cheat Sheet

| Situation            | Prompt                                                                            |
| -------------------- | --------------------------------------------------------------------------------- |
| Feature request      | _"What human outcome are we trying to achieve for [persona]?"_                    |
| Scope creep          | _"Which Hill does this serve? If none, add a Hill or drop the feature."_          |
| Priority conflict    | _"Let's use the Prioritization Grid. Rate: importance to user × feasibility."_    |
| Design review        | _"Playback: Does this address the Hill? What's the one thing that doesn't work?"_ |
| New phase            | _"Who is the persona whose life changes most? Let's write their Hill."_           |
| Metrics discussion   | _"How would the [persona] know their life got better? That's our metric."_        |
| Misalignment         | _"Let's run Hopes & Fears. What does success look like for each of you?"_         |
| Untested assumptions | _"What must be true for this Hill to succeed? How confident are we?"_             |
| Premature solution   | _"Before we converge — give me 3 more ways to address this Hill."_                |

---

_Reference companion to [SKILL.md](SKILL.md)._
