---
name: discovery-opportunities
description: Weekly opportunity discovery coach for Legalhero PMs. Use this skill whenever you want to run a weekly opportunity discovery session, process user interview notes into structured opportunities, extract problems from customer feedback or complaints, update the Opportunity Solution Tree (OST), or review and prioritize the problem backlog. Trigger phrases: "run discovery", "weekly discovery", "I just did an interview", "help me extract opportunities", "update the OST", "what problems should we focus on", "process this feedback", "discovery session", "analyse this interview", "what did we learn this week". Also trigger immediately when the user pastes raw interview notes, complaint data, support ticket summaries, analytics observations, or internal feedback — and wants to turn those inputs into structured product opportunities. This skill only covers the opportunity/problem space. Solution exploration is out of scope here. Always activate this skill for any discovery-related work — catching new opportunities early and keeping the OST current is the foundation of everything else the PM team does.
---

# Discovery: Opportunity Space

This skill runs your weekly opportunity discovery session — the first and most critical half of the discovery cycle. The goal is a systematic, habit-based process for surfacing, scoring, and organising customer problems into your Opportunity Solution Tree.

**Important scope boundary**: This skill covers the *problem space* only — identifying and structuring opportunities. Solution brainstorming and assumption testing are a separate step (see `discovery-solutions`, when available).

---

## What you need to bring

Inputs can include any combination of:
- **Interview notes or transcripts** — from partner lawyer sessions, client calls, RSV stakeholder meetings
- **Internal feedback** — operations team observations, support tickets, verbal reports
- **Analytics signals** — PostHog usage patterns, drop-off points, feature adoption data
- **Complaint data** — "Keine Rückmeldung" reports, case delays, NPS responses
- **Your own observations** — friction points you noticed in the product this week

You don't need all of these every week. One solid interview and a handful of observations is enough to run a meaningful session.

---

## Workflow

### Step 1: Orient to the current context

Before extracting anything, read the current state:

1. Check the quarterly outcomes at `/Product Management OS/.claude/product/outcomes/` to understand what business objectives are in focus this quarter. Discovery should serve those outcomes — not float freely.
2. Scan existing opportunity files in `/Product Management OS/.claude/product/discovery/opportunities/` to understand what's already captured. This prevents duplication and helps you spot where new inputs reinforce or challenge existing opportunities.

If those files don't exist yet, start fresh and note it.

### Step 2: Intake the inputs

Ask the user what they're bringing to this session. Typical entry points:

**A. Post-interview processing** — the user has notes/transcript from a session they just ran. Go deep: extract every distinct problem or need mentioned, no matter how small. Don't filter yet — you're in listening mode.

**B. Weekly review with mixed inputs** — the user has several signals from the week (interview + complaints + analytics). Process each source separately, then consolidate.

**C. Quick add** — a single piece of feedback or observation that should be captured before it's forgotten. Create a minimal opportunity entry and cross-reference it with the existing OST.

If the user hasn't provided inputs yet, ask: *"What did you learn this week? Walk me through it — I'll handle the structuring."*

### Step 3: Extract raw opportunities

As you process each input, capture raw opportunity statements in this form:

> **[User type] [pain verb] [specific situation]**

Examples:
- *Partner lawyers lose case context when switching to the document editor*
- *Operations team has no visibility into email delivery failures*
- *Clients with non-German backgrounds don't respond to email communication*

Don't score yet. Don't filter yet. Don't jump to solutions. Just surface every distinct problem or need.

**What counts as an opportunity:**
- Friction in a workflow (takes more steps than it should)
- Missing capability the user needs (something they work around)
- Trust/quality failure (wrong data, unreliable feature)
- Emotional frustration (even vague complaints are signals)
- Workarounds users have invented (always indicates an unmet need)

**What does NOT count:**
- Solution requests from users ("they asked for X") — note the request, but reframe as the underlying problem
- Internal process issues unrelated to product
- Pure feature requests without an articulated problem

### Step 4: Structure into the Opportunity Solution Tree

Organise the raw opportunities into a parent-child hierarchy:

- **Parent opportunity** — a broad, high-level problem cluster
- **Child opportunity** — a specific, observable instance of the parent

The OST is not a flat list. It's a tree where the top nodes represent strategic problem areas, and the children represent specific, testable sub-problems. Good trees have 2-5 children per parent.

**Hierarchy test**: Can you say "X happens *because of* Y"? If yes, Y is the parent and X is the child.

**Example:**
```
Case takeover workflow doesn't ensure timely first client contact [Parent]
  ├── No automated first-contact message triggered at case takeover [Child]
  └── Cases without deadlines sink to the bottom and are forgotten [Child]
```

### Step 5: Score each opportunity

Use the Pain × Reach × Frequency formula. Each dimension is rated on a 1–3 scale:

| Dimension | 1 | 2 | 3 |
|-----------|---|---|---|
| **Pain** | Low — minor inconvenience, easy workaround | Medium — real friction, disrupts flow, risks errors | High — blocks key workflow, causes failures, significant time cost |
| **Reach** | Limited — a few specific users or edge cases | Significant — a meaningful segment of users | Broad — virtually all relevant users are affected |
| **Frequency** | Rare — occasionally, hard to predict | Regular — multiple times per week | Constant — every time the user performs this workflow |

**Score = Pain × Reach × Frequency** (max 27)

Score parents and children separately. A parent score should reflect the aggregate problem cluster, not just one child.

**Scoring calibration:**
- Score ≥ 18: High priority — directly worth investigating for solutions
- Score 9–17: Medium priority — keep in OST, monitor for reinforcing signals
- Score ≤ 8: Low priority — captured but not actioned unless patterns emerge

Be honest. Don't inflate scores to justify working on something you like.

### Step 6: Cross-reference with existing opportunities

Before finalising, compare new opportunities against existing ones:
- **Reinforcement** — new evidence strengthens an existing opportunity → update the existing file with new evidence, don't create a duplicate
- **New child** — the new opportunity is a specific instance of an existing parent → add it as a child
- **New parent** — a recurring theme across multiple sources → create a new parent opportunity
- **Contradiction** — new evidence challenges an existing opportunity → flag the tension and note what needs further validation

Note every cross-reference explicitly in the output file.

### Step 7: Connect to quarterly outcomes

For each high-priority opportunity (score ≥ 18), note which quarterly outcome it connects to. If an opportunity doesn't connect to any current outcome, flag it — it may be important, but it isn't discovery that serves the current focus.

Reference Legalhero's five strategic pillars when stating strategic relevance:
1. **Intelligent Matching** — right lawyer, right case
2. **Mandate Distribution** — balanced workload, predictable case flow
3. **Digital Case Orchestration** — standardised workflows across the lifecycle
4. **Process Standardisation** — measurable, SLA-driven quality
5. **Data-Driven Infrastructure** — transparency, measurability, scalability

### Step 8: Write the output file

For each new source of opportunities (one interview, one feedback batch, one analytics observation), create a new file:

**File path:** `/Product Management OS/.claude/product/discovery/opportunities/`
**Filename format:** `{source-type}-{topic}-{YYYY-MM-DD}.md`

Examples:
- `interview-livshic-2026-04-10.md`
- `internal-feedback-intake-quality-2026-04-10.md`
- `analytics-document-editor-dropoff-2026-04-10.md`

Read the template at `references/opportunity-template.md` and follow it exactly.

For existing opportunity files that receive new evidence, edit the file directly — add evidence quotes to the relevant child opportunity and update the "Gaps & Uncertainties" section.

### Step 9: Deliver a discovery summary

After saving the file(s), give the user a crisp summary:

```
## Weekly Discovery Summary — [Date]

**New opportunities identified**: N (X high priority, Y medium, Z low)
**Existing opportunities reinforced**: N
**Top opportunities this week**:
  1. [Title] — Score: [N] — [One-line description]
  2. ...

**Key themes emerging**:
  - [Theme 1]
  - [Theme 2]

**Recommended next focus**:
  [The 1-2 opportunities most worth investigating further, and why]

**Gaps to fill next week**:
  - [Specific validation question or interview focus area]
```

---

## Quality checks

Before saving any opportunity file, verify:
- Every opportunity is a *problem*, not a solution — "lawyers can't see deadlines while editing" not "add a sidebar panel"
- Every score has evidence backing it — not vibes
- Parent opportunities are genuinely distinct problem clusters, not just groupings of convenience
- Children are specific enough to be testable
- Cross-references are explicit — don't leave overlaps ambiguous
- Strategic relevance is stated for high-priority opportunities

---

## Handling common situations

**"The user just wants to paste notes and have you do everything"**
Do it. Read the notes, extract opportunities, score them, build the tree, write the file. Ask only if something is genuinely unclear. Don't turn a 15-minute processing task into a 15-question interview.

**"The user only talked to one person"**
That's fine — one interview is enough for a weekly session. Note the single-source limitation in the "Source Notes" section and flag what needs validation from additional perspectives.

**"The input is in German"**
Process it as-is. Opportunity titles and descriptions should be in English for consistency (this is how existing files are structured), but German quotes can be included verbatim as supporting evidence.

**"Nothing interesting happened this week"**
Help the user look harder. Check: Did they review any analytics? Were there any support tickets? Did they use the product themselves? A week without discovery inputs usually means discovery wasn't prioritised — surface that gently and help schedule next week.

**"A user suggested a specific solution"**
Note it in the opportunity file under the relevant child (as "Proposed solution from user") but don't let it become the opportunity itself. The opportunity is the problem. The solution suggestion is evidence of the problem's salience.

---

## File organisation reference

```
.claude/product/discovery/
├── opportunities/          ← Opportunity files live here
│   ├── interview-{topic}-{date}.md
│   ├── internal-feedback-{topic}-{date}.md
│   └── analytics-{topic}-{date}.md
├── assumptions/            ← Out of scope for this skill
└── solutions/              ← Out of scope for this skill
```

---

See `references/opportunity-template.md` for the exact output file structure.
