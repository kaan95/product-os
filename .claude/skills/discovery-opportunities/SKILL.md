---
name: discovery-opportunities
description: Weekly opportunity discovery coach. Use to run a discovery session, process interview notes into structured opportunities, extract problems from feedback, or update the Opportunity Solution Tree in Jira Polaris. Trigger phrases: "run discovery", "weekly discovery", "I just did an interview", "help me extract opportunities", "update the OST", "process this feedback", "discovery session", "analyse this interview". Also trigger when the user pastes raw interview notes, complaint data, support tickets, analytics observations, or internal feedback and wants to turn those into structured opportunities. Problem space only — solution exploration is out of scope.
---

# Discovery: Opportunity Space

This skill runs your weekly opportunity discovery session. The goal is a systematic, habit-based process for surfacing, scoring, and organising customer problems into your Opportunity Solution Tree — tracked in Jira Polaris (project: PD).

**Scope boundary**: This skill covers the *problem space* only — identifying and structuring opportunities. Solution brainstorming and assumption testing are a separate step.

---

## Jira issue type guide

The PD project uses these issue types. Only create the types listed here during a discovery session:

| Type | When to use |
|---|---|
| **Opportunity** | A customer problem, pain point, or unmet need — the core output of this skill |
| **Idea** | A specific solution concept a user proposed (capture it, but note it's out of scope for deeper work here) |
| **Feature** | Committed, scoped work — *not* created by this skill |
| **Improvement** | Operational or quality enhancement — *not* created by this skill |
| **Initiative** | Strategic theme grouping multiple items — *not* created by this skill |

---

## What you need to bring

Inputs can include any combination of:
- **Interview notes or transcripts** — from user sessions, partner calls, stakeholder meetings
- **Internal feedback** — operations team observations, support tickets, verbal reports
- **Analytics signals** — usage patterns, drop-off points, feature adoption data
- **Complaint data** — reports, case delays, NPS responses
- **Your own observations** — friction points you noticed in the product this week

You don't need all of these every week. One solid interview and a handful of observations is enough to run a meaningful session.

---

## Workflow

### Step 1: Orient to the current context

Before extracting anything, load the current state from Jira:

1. Query existing opportunities: `project = PD AND issuetype = Opportunity ORDER BY created DESC` — scan the results to understand what's already captured. This prevents duplication and helps you spot where new inputs reinforce or challenge existing opportunities.
2. Ask the user what the current quarter's key outcomes or focus areas are, if they haven't stated them. Discovery should serve those outcomes — not float freely. Do not attempt to read outcomes from local files.

If the PD project returns no opportunities yet, note it and start fresh.

### Step 2: Intake the inputs

Ask the user what they're bringing to this session. Typical entry points:

**A. Post-interview processing** — the user has notes/transcript from a session they just ran. Go deep: extract every distinct problem or need mentioned, no matter how small. Don't filter yet — you're in listening mode.

**B. Weekly review with mixed inputs** — the user has several signals from the week (interview + complaints + analytics). Process each source separately, then consolidate.

**C. Quick add** — a single piece of feedback or observation that should be captured before it's forgotten. Create a minimal Opportunity in Jira and cross-reference it with the existing board.

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

The OST is not a flat list. Good trees have 2–5 children per parent.

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

Before creating any new Jira issue, query the PD board for potential overlaps. For each new opportunity statement:

- **Reinforcement** — a matching existing Opportunity already exists → update its Jira description with the new evidence quote; do not create a duplicate
- **New child** — the new opportunity is a specific instance of an existing parent → create it as a new Opportunity and note the relationship in both descriptions
- **New parent** — a recurring theme across multiple sources → create a new parent Opportunity
- **Contradiction** — new evidence challenges an existing opportunity → flag the tension in the existing issue's description and note what needs further validation

State every cross-reference decision explicitly before writing to Jira.

### Step 7: Connect to quarterly outcomes

For each high-priority opportunity (score ≥ 18), state which current quarter outcome or strategic theme it connects to. Use the outcomes the user provided in Step 1. If an opportunity doesn't connect to any current outcome, flag it — it may be important, but it isn't discovery that serves the current focus.

Do not hardcode strategic pillars in this skill. Ask the user if they haven't provided them.

### Step 8: Write to Jira Polaris

For each new or updated opportunity, write to the PD project:

**Creating a new Opportunity:**
- Use `issuetype = Opportunity`
- **Title**: the opportunity statement (`[User type] [pain verb] [specific situation]`)
- **Description**: structured as below

```
## Evidence
- [Source type, date]: "[verbatim quote or observation]"
- [Source type, date]: "[verbatim quote or observation]"

## Score
Pain: [1–3] | Reach: [1–3] | Frequency: [1–3] → Total: [score]/27 ([Low/Medium/High] priority)

## Outcome connection
[Which quarterly outcome this connects to, or "Not connected to current quarter — flagged"]

## Gaps & open questions
- [What would need to be true to raise the score?]
- [What would further validation look like?]
```

**Updating an existing Opportunity:**
Append new evidence to the Evidence section and update the score if the new data changes it. Do not overwrite existing evidence.

**Capturing a user-proposed solution:**
If a user suggested a specific solution during the session, create an `Idea` issue (not an Opportunity). Title it as the proposed solution and link it to the relevant Opportunity in the description.

### Step 9: Deliver a discovery summary

After writing to Jira, give the user a crisp summary:

```
## Weekly Discovery Summary — [Date]

**New opportunities created**: N (X high priority, Y medium, Z low)
**Existing opportunities reinforced**: N
**Top opportunities this week**:
  1. [PD-XXX] [Title] — Score: [N] — [One-line description]
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

Before writing to Jira, verify:
- Every opportunity is a *problem*, not a solution — "lawyers can't see deadlines while editing" not "add a sidebar panel"
- Every score has evidence backing it — not vibes
- Parent opportunities are genuinely distinct problem clusters, not just groupings of convenience
- Children are specific enough to be testable
- Cross-references are explicit — don't leave overlaps ambiguous
- Strategic relevance is stated for high-priority opportunities

---

## Handling common situations

**"The user just wants to paste notes and have you do everything"**
Do it. Read the notes, extract opportunities, score them, build the tree, write to Jira. Ask only if something is genuinely unclear. Don't turn a 15-minute processing task into a 15-question interview.

**"The user only talked to one person"**
That's fine — one interview is enough for a weekly session. Note the single-source limitation in the Jira description's "Gaps & open questions" section and flag what needs validation from additional perspectives.

**"The input is in German"**
Process it as-is. Opportunity titles and Jira issue summaries should be in English for consistency, but German quotes can be included verbatim as supporting evidence.

**"Nothing interesting happened this week"**
Help the user look harder. Check: Did they review any analytics? Were there any support tickets? Did they use the product themselves? A week without discovery inputs usually means discovery wasn't prioritised — surface that gently and help schedule next week.

**"A user suggested a specific solution"**
Capture it as an `Idea` issue in Jira linked to the relevant Opportunity. Don't let it become the opportunity itself — the opportunity is the problem.
