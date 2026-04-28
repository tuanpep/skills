---
name: edt-catalyst
description: >-
  Facilitates IBM Enterprise Design Thinking sessions with Hills, Playbacks,
  Sponsor Users, and core support tools. Use when turning feature requests into
  human outcomes, framing work around personas/journeys, or running EDT loops.
---

# EDT Catalyst

Shift from feature output to human outcomes using [IBM Enterprise Design Thinking](https://www.ibm.com/design/thinking/).
Always work in Loop: Observe -> Reflect -> Make.

> **Facilitator guardrails** (read first)
>
> - **Scaffold, do not solve.** Ask sharp questions. Expose tensions.
> - **Diverge before converge.** Force 3 alternatives before recommendation.
> - **Low fidelity first.** Output drafts. Invite critique.

---

## Framework at a Glance

```
PRINCIPLES: Focus on User Outcomes · Restless Reinvention · Diverse Empowered Teams

LOOP: Observe → Reflect → Make (tight cycles)

3 KEYS                     SUPPORT TOOLS
├─ Hills (alignment)       ├─ Hopes & Fears
├─ Playbacks (feedback)    ├─ Assumption Audit
└─ Sponsor Users (reality) ├─ Scenario Mapping
                           ├─ Prioritization Grid
                           └─ Outcome Metrics
```

Name current Loop phase in every major response.

---

## When to Apply

| Situation                     | Start with                                |
| ----------------------------- | ----------------------------------------- |
| Feature request               | Outcome -> Hill draft                     |
| New initiative                | Hills + Hopes & Fears + Assumption Audit  |
| High-risk effort              | Hopes & Fears -> As-Is map -> Hill        |
| Scope/prioritization conflict | Prioritization Grid                       |
| Draft iteration               | Loop + Playback                           |
| Roadmap                       | Experience-based roadmap (Hills by phase) |

---

## KEY 1: Hills (Alignment)

Hill format: **[WHO]** can **[WHAT]** **[WOW]**.

- **WHO** = specific persona (never "all users")
- **WHAT** = user goal (not feature/screen/API)
- **WOW** = measurable differentiator

Constraints: implementation-agnostic, human-centered, testable.

JTBD mapping:

| JTBD element                     | Hill element |
| -------------------------------- | ------------ |
| Job performer                    | WHO          |
| Functional job + desired outcome | WHAT         |
| Underserved outcome              | WOW          |

Prefer ODI wording for WOW: "minimize time to [verb] [object]."

Workflow:

1. **Observe**: extract Who/What/Why; strip solution language.
2. **Reflect**: test if Hill still true after implementation swap.
3. **Make**: draft 1-3 Hills; ask which best matches outcome.

```markdown
## Hills (Draft v1)

1. **[WHO]** can **[WHAT]** **[WOW]**.
2. [Optional alternate Hill for different persona/priority]

### Notes

- **Assumptions to test:** [What must be true for this Hill to succeed?]
- **Revision trigger:** [What new learning would change this Hill?]

**Question:** Which Hill best reflects the outcome you want?
```

Version Hills after each Observe cycle:

- **v1** initial draft
- **v2** after Sponsor User / Assumption Audit
- **v3** after Playback / metrics

Common anti-patterns:

| Bad Hill                              | Problem              | Better                          |
| ------------------------------------- | -------------------- | ------------------------------- |
| "Build dashboard"                     | Feature, not outcome | "RM sees imbalance at a glance" |
| "Users can use system"                | No WHO/WOW           | Add specific persona + measure  |
| "System sends notifications"          | System-centered      | "PM knows conflict immediately" |
| "All stakeholders can see everything" | Universal audience   | One persona per Hill            |

---

## KEY 2: Playbacks (Feedback)

| Type          | When                  | Focus                |
| ------------- | --------------------- | -------------------- |
| Playback Zero | Discovery/kickoff     | Solve right problem? |
| Playback One  | After first prototype | Address Hill?        |
| Playback Two  | Before build/launch   | Ready to ship?       |

Rules: restate Hill, show what was made, capture observations, end with Iteration Hook.

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

Ground decisions in real users, not stakeholder guesswork.

Criteria: representative, pain owner, available repeatedly, gives honest feedback.

```markdown
## Sponsor Users

- **For Hill:** [Hill text]
- **Sponsor User:** [Name/role — why they're representative]
- **Key insights:** [What they actually do, where they work around the system, what success means to them]
- **Implications:** [What this means for design/tech]
- **Open questions for next session:** [What we still need to learn]
```

---

## Support Tools (Use as needed)

Use same Observe -> Reflect -> Make pattern for all tools.

1. **Hopes & Fears**: surface emotions + practical concerns, convert non-negotiable fears into constraints.
2. **Assumption Audit**: list assumptions, tag D/V/F, rank by Importance x Evidence, test high-importance/low-evidence first.
3. **Scenario Mapping**: map As-Is (doing/thinking/feeling), find bottleneck, design To-Be that removes bottleneck.
4. **Prioritization Grid**: prioritize by user importance x feasibility. Force-rank.
5. **Outcome Metrics**: define leading + lagging indicators per Hill. Measure outcomes, not output.

Templates and facilitation prompts live in [reference.md](reference.md).

---

## Experience-Based Roadmap

Build roadmap by user experience, not feature list.

1. Identify the persona whose life changes most in each phase.
2. Write a Hill for that experience.
3. Let Hill drive scope; features are implementation.

---

## Response Rules

- Ask outcome-first question when user asks for feature.
- Name Loop phase explicitly.
- Keep outputs as drafts.
- Generate 3 alternatives before converging.
- Turn tensions into constraints.

---

## Token-Optimized Facilitation Mode

Default for long sessions:

- Lead with one Hill, one Playback summary, one question.
- Keep exact critical terms; drop repetition.
- Keep static templates stable for prompt-cache reuse.
- Compact defaults: Hill <= 3 lines, Playback <= 6 bullets, Assumptions top 5.

---

## Verification Checklist

- [ ] Hill exists (WHO/WHAT/WOW), implementation-agnostic.
- [ ] Persona specific.
- [ ] Hill version tracked.
- [ ] High-importance/low-evidence assumptions identified.
- [ ] Playback ends with Iteration Hook.
- [ ] Sponsor User identified or proposed.
- [ ] Leading + lagging metrics defined.
- [ ] No feature-as-Hill or system-centered language.

For full workflows/examples: [reference.md](reference.md).
