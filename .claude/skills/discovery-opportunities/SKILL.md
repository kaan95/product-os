---
name: discovery-opportunities
description: Weekly opportunity discovery coach. Use to run a discovery session, process interview notes into structured opportunities, extract problems from feedback, or grow the Opportunity Solution Tree in Notion. Trigger phrases: "run discovery", "weekly discovery", "I just did an interview", "help me extract opportunities", "update the OST", "process this feedback", "discovery session", "analyse this interview". Also trigger when the user pastes raw interview notes, complaint data, support tickets, analytics observations, or internal feedback and wants to turn those into structured opportunities. Problem space only — solution exploration is out of scope.
---

# Discovery: Opportunity Space

This skill runs the weekly opportunity discovery session. The goal is a systematic, habit-based process for surfacing, scoring, and organising customer problems into a true Teresa Torres-style **Opportunity Solution Tree (OST)**.

**Scope boundary**: this skill covers the *problem space* only — identifying, decomposing, and structuring opportunities. Solution brainstorming and assumption testing are a separate step (`solution-brainstorm`).

---

## How the OST is stored

The OST lives in **Notion**, under the user's "Opportunities" root page (linked from the Discovery space). The hierarchy is encoded structurally — not as prose:

- The root of any subtree is the **product outcome** the discovery work serves.
- Each opportunity is a **Notion page**.
- Sub-opportunities are **child pages** of their parent opportunity's page.
- Depth is unbounded and varies across the tree — each branch is decomposed only as deep as the evidence supports.

This means: when a new sub-opportunity is created, it is created as a child of the parent's Notion page. Hierarchy is visible at a glance in Notion's page tree, and the tree can be traversed by walking child pages.

### External references

- Existing opportunities tracked in Jira Polaris (PD project) can be linked from a Notion page's body for traceability — but the Notion tree is now the source of truth.
- A user-proposed solution captured during a discovery session is created as a child page under the relevant opportunity, prefixed `Idea: `. It does not become its own opportunity — the opportunity is the underlying problem.

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

### Step 1: Orient — anchor the session to an outcome and load the relevant subtree

Discovery should serve a specific product outcome — never float freely. Before extracting anything:

1. **Identify the target outcome** for this session. Default: the quarterly product outcome the user has named (or the one most clearly served by the inputs they're bringing). The user's quarterly outcomes page is the source of truth — fetch it via Notion if the user hasn't pasted them. The session will operate on the subtree under that outcome.
2. **Load the existing subtree** from Notion. Walk the child / grandchild / great-grandchild pages of the outcome root. Build a flat list of `{path, title, score}` so cross-referencing in Step 6 is fast. Use `notion-fetch` for the root and `notion-query-data-sources` if the OST root is database-backed.
3. **If no subtree exists yet under the chosen outcome**, create the outcome root page (just a header) before extracting opportunities.

If the user can't articulate the outcome this discovery serves, pause and ask — don't guess. An OST without an outcome at the top is a list of grievances.

### Step 2: Intake the inputs

Ask the user what they're bringing to this session. Typical entry points:

**A. Post-interview processing** — the user has notes/transcript from a session they just ran. Go deep: extract every distinct problem or need mentioned, no matter how small. Don't filter yet — you're in listening mode.

**B. Weekly review with mixed inputs** — the user has several signals from the week (interview + complaints + analytics). Process each source separately, then consolidate.

**C. Quick add** — a single piece of feedback or observation that should be captured before it's forgotten. See "Common situations" for how to handle this without doing a full tree pass.

If the user hasn't provided inputs yet, ask: *"What did you learn this week? Walk me through it — I'll handle the structuring."*

### Step 3: Extract raw opportunities

As you process each input, capture raw opportunity statements in this form:

> **[User type] [pain verb] [specific situation]**

Phrase from the customer's perspective. Where possible, lift verbatim language from the source.

Examples:
- *Partner lawyers lose case context when switching to the document editor*
- *Operations team has no visibility into email delivery failures*
- *Clients with non-German backgrounds don't respond to email communication*

Don't score yet. Don't cluster yet. Don't jump to solutions. Just surface every distinct problem or need.

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

### Step 4: Decompose into the tree

This is the heart of the skill. The OST is multi-level — depth varies across the tree, driven by the evidence.

#### Decomposition pass (apply repeatedly until no branch decomposes further)

1. For the current set of opportunities at level *N* under the outcome root, ask: *Do any of these contain genuinely distinct sub-problems that have their own evidence and would warrant their own solution?*
2. **If yes** → split that opportunity into 2–5 sub-opportunities at level *N+1*. Re-phrase the parent so it remains true at the higher level of abstraction.
3. After each split, run a **MECE check**:
   - **Mutually exclusive**: does each piece of evidence belong under exactly one sub-opportunity? If a quote could fit under two siblings, the boundary between them is wrong — re-cut.
   - **Collectively exhaustive**: if every sub-opportunity were resolved, would the parent be resolved? If a chunk of the parent's evidence has no home among the children, you're missing a sub-opportunity.
4. **Stopping rule** for any branch — stop decomposing when *either*:
   - There's no further evidence that meaningfully separates one sub-problem from another, **or**
   - The opportunity is already narrow enough that a single solution could plausibly address it.

Depth will vary across the tree. **Don't force symmetry.** Some branches stop at level 2; others reach level 4. That's correct — it reflects where evidence is rich vs. thin.

#### Worked example (3 levels)

```
Outcome: <product outcome that anchors this subtree>
└── Customers feel out of the loop on the work being done for them [Level 1]
    ├── Customers don't get proactive updates on progress [Level 2]
    │   ├── No update after a major milestone is hit [Level 3]
    │   └── No update during long wait periods on external dependencies [Level 3]
    ├── Customers can't reach the team when they try to get an update themselves [Level 2]
    │   ├── Long wait times on the inbound channel [Level 3]
    │   └── Async messages (email, in-app) go unanswered [Level 3]
    └── Customers find out the work is finished only after the fact [Level 2 — leaf, evidence doesn't yet support deeper splits]
```

Notice that the third level-2 branch stops at level 2 — its evidence doesn't yet support a meaningful further split. That's fine. Depth is driven by evidence, not symmetry.

### Step 5: Score each opportunity

Use Pain × Reach × Frequency. Each dimension is rated on a 1–3 scale:

| Dimension | 1 | 2 | 3 |
|-----------|---|---|---|
| **Pain** | Low — minor inconvenience, easy workaround | Medium — real friction, disrupts flow, risks errors | High — blocks key workflow, causes failures, significant time cost |
| **Reach** | Limited — a few specific users or edge cases | Significant — a meaningful segment of users | Broad — virtually all relevant users are affected |
| **Frequency** | Rare — occasionally, hard to predict | Regular — multiple times per week | Constant — every time the user performs this workflow |

**Score = Pain × Reach × Frequency** (max 27).

**Scoring calibration:**
- Score ≥ 18: High priority — directly worth investigating for solutions
- Score 9–17: Medium priority — keep in OST, monitor for reinforcing signals
- Score ≤ 8: Low priority — captured but not actioned unless patterns emerge

**Scoring across levels:**
- A parent's score should be **≥ the maximum of its children's scores** — it represents the aggregate problem cluster, which is at least as large as any individual sub-problem.
- If a sibling-set has scores that all exceed the parent's, the parent statement is too narrow — re-phrase upward and re-score.
- A parent score should not be a simple sum of its children either; it's a holistic reflection of how broad and painful the parent-level problem is.

Be honest. Don't inflate scores to justify working on something you like.

### Step 6: Cross-reference against the existing tree

Cross-referencing is no longer "is this a parent or a child" — it's "where in the tree does this go?" For each new raw opportunity:

- **Exact match at any depth** — a node already captures this problem. → **Reinforce**: append the new evidence to that page; update the score if the new data changes it.
- **New sibling at depth *N*** — fits as a peer of existing nodes under an existing parent. → **Create** as a child of that parent.
- **New sub-branch under an existing intermediate** — the new opportunity is a more specific instance of an existing intermediate node, and that intermediate has no children yet (or has children that don't cover this case). → **Create** as a child of that intermediate, possibly triggering further decomposition of the intermediate's other children to maintain MECE.
- **New top-level branch under the outcome root** — no place in the existing tree at any depth. → Pause: is the evidence strong enough to introduce a new top-level branch? Torres' guidance is to be slow about adding top-level branches — they imply the outcome's problem space wasn't well understood. If you create one, document why.
- **Contradiction** — new evidence challenges an existing node. → Don't silently overwrite. Append the evidence with a note flagging the tension and what needs validation.

State every cross-reference decision explicitly before writing.

### Step 7: Outcome connection

Outcome connection is now **structural**: every opportunity inherits the outcome of its tree root. There's no per-opportunity "outcome connection" line — the page's position in the tree encodes it. The outcome root page itself carries the outcome reference (link to the user's outcomes page).

If a new piece of evidence doesn't connect to the outcome the session is anchored on, it doesn't belong in this subtree. Either it serves a different outcome (and belongs in another subtree) or it indicates the chosen outcome doesn't fit the evidence — flag both possibilities to the user.

### Step 8: Write to Notion

For every change identified in Step 6, perform the corresponding Notion write:

**Creating a new opportunity (at any depth):**
- Use `notion-create-pages` with `parent.type = "page_id"` set to the **immediate parent opportunity's page ID** (or the outcome root's page ID for a new top-level branch).
- Page title = the opportunity statement (`[User type] [pain verb] [specific situation]`).
- Page body uses this template:

```markdown
## Score
Pain: [1–3] | Reach: [1–3] | Frequency: [1–3] → Total: [score]/27 ([Low/Medium/High] priority)

## Evidence
- [Source type, date]: "[verbatim quote or observation]"
- [Source type, date]: "[verbatim quote or observation]"

## Gaps & open questions
- [What would need to be true to raise the score?]
- [What would further validation look like?]
```

**Updating an existing opportunity:**
- Use `notion-update-page` (or `notion-fetch` then write back the updated body).
- Append new evidence to the Evidence section. Do not overwrite existing evidence.
- Update the score if the new data changes it; note the score change in the Evidence reinforcement.

**Capturing a user-proposed solution:**
- Create a child page under the relevant opportunity with title prefix `Idea: `. Don't make it its own opportunity — the opportunity is the problem behind the suggested solution.

**Re-parenting (rare but happens):**
- If the cross-reference revealed an existing top-level opportunity that should actually be a child of a new intermediate, move it. Use `notion-move-pages` rather than recreating.

### Step 9: Deliver the discovery summary

Lead with a **tree rendering of the affected subtree(s)** so the user can see the shape of what changed. Use `NEW`, `REINFORCED`, or `MOVED` markers on each line.

```
Outcome: <root>
  ├── <Opportunity> (NEW, score 27)
  │   ├── <Sub-opportunity> (NEW, score 18)
  │   └── <Sub-opportunity> (REINFORCED, score 12)
  ├── <Opportunity> (REINFORCED, score 24)
  │   └── <Sub-opportunity> (NEW, score 14)
  └── <Opportunity> (NEW, score 9)
```

Then:

```
**New nodes**: N (X high priority, Y medium, Z low)
**Reinforced nodes**: N
**Moved / re-parented**: N

**Top opportunities this week**:
  1. [Notion link] [Title] — Score: [N] — [One-line description]
  2. ...

**Key themes emerging**:
  - [Theme 1]
  - [Theme 2]

**Recommended next focus**:
  [The 1–2 opportunities most worth investigating further, and why]

**Gaps to fill next week**:
  - [Specific validation question or interview focus area]
```

---

## Quality checks

Before writing to Notion, verify:
- Every opportunity is a *problem*, not a solution — "lawyers can't see deadlines while editing" not "add a sidebar panel".
- Every score has evidence backing it — not vibes.
- After each branching, MECE was verified explicitly: every evidence quote sits under exactly one sub-opportunity, and the sub-opportunities together cover the parent.
- No top-level opportunity is a flat statement that could be decomposed against the available evidence — if you can already see two clearly distinct sub-problems inside it, decompose before writing.
- Parent scores ≥ max(child scores). If not, re-phrase the parent broader or re-score.
- Cross-references are explicit — don't leave overlaps ambiguous.
- The chosen outcome is actually served by the new branches; if not, flag.

---

## Handling common situations

**"The user just wants to paste notes and have you do everything"**
Do it. Read the notes, extract opportunities, decompose into the tree, score them, write to Notion. Ask only if something is genuinely unclear. Don't turn a 15-minute processing task into a 15-question interview.

**"The user only talked to one person"**
That's fine — one interview is enough for a weekly session. Note the single-source limitation in the page's "Gaps & open questions" section and flag what needs validation from additional perspectives.

**"The input is in German"**
Process it as-is. Opportunity titles should be in English for consistency, but German quotes can be included verbatim as supporting evidence.

**"Nothing interesting happened this week"**
Help the user look harder. Check: did they review any analytics? Were there any support tickets? Did they use the product themselves? A week without discovery inputs usually means discovery wasn't prioritised — surface that gently and help schedule next week.

**"A user suggested a specific solution"**
Capture it as a child page under the relevant opportunity, with title prefix `Idea: `. Don't let it become the opportunity itself — the opportunity is the problem.

**"The new evidence doesn't fit anywhere in the existing tree"**
Pause. Two possibilities: (a) this is a missed branch under the current outcome root — an area of the problem space the tree doesn't yet cover; (b) it serves a *different* outcome and belongs in a different subtree. Surface both possibilities to the user and let them decide. Don't silently force-fit it under the closest-matching node.

**"The user wants a quick add and a full tree pass feels too heavy"**
Accept the quick add as a leaf at the most plausible location, mark its title with the prefix `[provisional] `, and queue a re-tree pass for the next full session. The provisional marker prevents the leaf from being treated as authoritative until it's properly placed.

**"The tree is getting too wide or too deep"**
Torres heuristics:
- At any branch with >5 siblings, look for two that could merge under a new intermediate. Excessive width usually means the parent is too vague.
- A single branch deeper than 4 levels often means lower levels have crossed into solution-space — the leaves are starting to describe *how to fix* rather than *what's wrong*. Pull them back into the problem space or move them to `solution-brainstorm`.
