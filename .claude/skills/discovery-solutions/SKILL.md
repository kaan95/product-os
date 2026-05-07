---
name: discovery-solutions
description: Brainstorm 3–5 diverse solution ideas for the leaves of an Opportunity Solution Tree (OST) stored in Notion. Partner skill to `discovery-opportunities`: that skill builds the problem-space tree, this skill explores the solution space at the leaves. Reads opportunities from the user's "Opportunities" Notion root (or a named subtree) and returns ideas in chat — no Notion writes, no local files. Trigger phrases: "brainstorm solutions", "explore solutions", "discovery solutions", "what could we build for this opportunity", "ideate on this opportunity", "solutions for the OST". Also trigger when the user names an outcome or opportunity and asks what to build / try / explore.
---

# Discovery: Solution Space

This skill is the solution-space companion to `discovery-opportunities`. Where that skill structures problems into an Opportunity Solution Tree (OST) in Notion, this skill takes the **leaves** of that tree and generates diverse, testable solution ideas — following Teresa Torres' Continuous Discovery Habits framework.

**Scope boundary**: solution ideation only. No prioritisation, no specs, no Jira tickets. Output is chat-only — nothing is written back to Notion or local files.

$ARGUMENTS

---

## Arguments

- **Subtree** (optional): outcome / opportunity title, or a Notion link to the page that anchors the subtree. Defines the root to brainstorm under. If omitted → list the top-level children of the "Opportunities" page and ask the user which to use.
- **Constraints** (optional): e.g., "no new headcount", "<2 weeks to ship", "must work in current backend".
- **Angle preference** (optional): tech, process, design, incentive, people, data, partnership. Default: a diverse mix.

---

## Core principle: diverse solutions, not variations

Generate solutions that span **different angles** — never parametric variations of the same idea. If two solutions could be A/B/C-tested as variants of one concept, they count as one angle.

| Angle | Description |
|-------|-------------|
| **Technology** | Software, AI, or automation |
| **Process** | Change how the work is done |
| **Design / UX** | Change what users see and interact with |
| **Incentive / Policy** | Change motivations or rules |
| **People** | Change who does what or how they're trained |
| **Data / Transparency** | Make information visible |
| **Partnership** | External collaboration or integration |

---

## Workflow

### Step 1: Locate the subtree root

- **User gave a Notion link** → extract the page ID and `notion-fetch` directly.
- **User gave a title** → `notion-search` for it, prefer matches whose ancestor chain contains "Opportunities", then `notion-fetch`.
- **User gave nothing** → `notion-search` for the page titled "Opportunities" (the OST root), list its direct child pages (the outcome subtrees), and ask the user which subtree to brainstorm under. **Do not** default to the entire tree — that produces unfocused output.

### Step 2: Walk the subtree to find leaves

Recursively follow child pages from the chosen root using `notion-fetch`. A **leaf** = any opportunity page with no child pages of its own.

Build a flat list: `[{title, page_id, score, evidence_summary, gaps}]`.

**Skip rules:**
- Pages whose title starts with `Idea:` — these are user-suggested *solutions* captured by `discovery-opportunities`, not opportunities.
- Pages whose title starts with `[provisional]` — not yet authoritative; only include if the user explicitly opts in.

### Step 3: Extract context per leaf

Parse each leaf's page body using the template `discovery-opportunities` writes:

- `## Score` line → e.g. `Pain: 3 | Reach: 2 | Frequency: 3 → Total: 18/27 (High priority)`. Capture the total.
- `## Evidence` bullets → condense into a 1–2 sentence summary.
- `## Gaps & open questions` → carry forward as flags. If a leaf is too thin (no evidence, or evidence so vague that any solution would be guesswork), don't fabricate context — flag it for the recap and skip brainstorming.

### Step 4: Generate 3–5 diverse solutions per leaf

Each solution must use a **different angle** from the table above. Apply user-supplied constraints if provided.

For each solution, produce only:

1. **Title** + **Angle**
2. **Core idea** — 1–2 sentences. What is it, concretely? (Concept, not spec.)
3. **Riskiest assumption** — the one belief that, if wrong, kills the idea entirely. Phrase as: *"We believe X. We'll know when Y."*

Do **not** produce: "Why it works", cheapest-test design, effort sizing, comparison tables, or recommendation rankings. Keep it lean — this is a thinking aid, not a decision document.

### Step 5: Return everything in chat

Group by leaf opportunity. **No Notion writes. No local file writes.** Close with a short recap.

---

## Output format

```markdown
## Solutions for "{Outcome subtree name}"

### {Leaf Opportunity Title}  (Score: {N}/27)
{1–2 sentence evidence summary}

1. **{Title}** — *{Angle}*
   {1–2 sentence core idea.}
   *Riskiest assumption*: We believe {X}. We'll know when {Y}.

2. **{Title}** — *{Angle}*
   …

[…3–5 solutions per leaf…]

---

### {Next Leaf Opportunity Title}  (Score: {N}/27)
…

---

**Recap**: {N} leaves brainstormed · {M} solutions generated · {K} leaves skipped

**Skipped / flagged** (if any):
- {Title} — {what's missing, e.g. "no evidence section yet"}
```

---

## Key rules

- **Solutions are concepts, not specs** — no wireframes, no Jira-level detail.
- **Each solution = a different angle.** Two solutions in the same angle is a sign you've slipped into variations.
- **One riskiest assumption per solution** — the one that, if wrong, kills the idea entirely.
- **Don't fabricate context.** If a leaf has no evidence on its Notion page, flag it and skip — don't invent the problem to make the solutions sound good.
- **English only** — including for Notion-pages whose evidence is in another language. Quote evidence verbatim if helpful, but solution titles, angles, and assumptions stay in English.
- **No writes.** This skill is read-only against Notion and writes nothing locally. If the user wants to capture a solution, that's what `discovery-opportunities` does (as an `Idea:` child page).
