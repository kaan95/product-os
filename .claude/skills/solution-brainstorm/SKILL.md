---
name: solution-brainstorm
description: Generate 5-6 diverse solution ideas for extracted opportunities using Teresa Torres' Opportunity Solution Tree framework. Solutions approach the problem from genuinely different angles to avoid first-idea bias.
---

# Solution Brainstorm

Generate diverse, testable solution ideas for product opportunities, following Teresa Torres' Continuous Discovery Habits framework.

$ARGUMENTS

## Arguments

- **Opportunity** (required): Specific title/description, file reference, `all` (Score >= 12), or `top-N`
- **Constraints** (optional): e.g., "no new headcount", "< 2 weeks to ship"
- **Angle Preference** (optional): tech, process, design, incentive, partnership, data. Default: diverse mix

## Core Principle: Diverse Solutions, Not Variations

Generate solutions that span **different angles** — never parametric variations of the same idea.

| Angle | Description |
|-------|-------------|
| **Technology** | Software, AI, or automation |
| **Process** | Change how work is done |
| **Design / UX** | Change what users see and interact with |
| **Incentive / Policy** | Change motivations or rules |
| **People** | Change who does what or how they're trained |
| **Data / Transparency** | Make information visible |
| **Partnership** | External collaboration or integration |

## Instructions

### 1. Load Context
- Read all files in `.claude/product/discovery/opportunities/`
- Read all files in `.claude/product/discovery/solutions/` (avoid duplicating existing ideas)
- Skim `.claude/product/strategy/product-strategy-2026.md`

### 2. Select Opportunities
Find the target opportunity and extract: statement, type (Problem/Need/Desire), score, and key evidence.

### 3. Generate 5–6 Solutions Per Opportunity
Each solution must use a **different angle**. For each solution, define:

1. **Title** + **Angle**
2. **Core Idea**: 1-2 sentences
3. **Why It Works**: The causal mechanism — what changes for the stakeholder?
4. **Riskiest Assumption**: One critical thing that must be true. "We believe X. We'll know when Y."
5. **Cheapest Test**: Method, what you'd do, duration, success/failure signal
6. **Effort**: S / M / L / XL

### 4. Check Overlap
Flag any solution that closely mirrors an existing file in `.claude/product/discovery/solutions/` and replace it with a fresh angle.

### 5. Save & Summarize
- Save to: `.claude/product/discovery/solutions/{opportunity-slug}-solutions-{date}.md`
- Multiple opportunities: `brainstorm-{scope}-{date}.md`

## Output Structure

```markdown
# Solution Brainstorm: {Opportunity}

**Date**: {date} | **Score**: {X} | **Constraints**: {or "None"}

**Opportunity**: {Statement from stakeholder perspective}
**Type**: Problem / Need / Desire
**Evidence**: {1-2 key data points or quotes}

---

## Solutions

| # | Title | Angle | Effort | Test Speed |
|---|-------|-------|--------|------------|
| 1 | {Title} | {Angle} | {S/M/L/XL} | {Fast/Med/Slow} |
| 2 | ... | ... | ... | ... |
| ... | | | | |

---

### 1. {Solution Title}
**Angle**: {Angle}

{1-2 sentence core idea.}

**Why it works**: {1-2 sentences on the causal mechanism}

**Riskiest assumption**: We believe {X}. We'll know when {Y}.

**Cheapest test**: {Method} — {what you'd do} — {duration} — ✅ {success signal} / ❌ {failure signal}

**Effort**: {S/M/L/XL}

---

### 2. {Solution Title}
{Same compact structure}

---

[...repeat for all 5-6 solutions...]

---

## Comparison

| Dimension | Sol 1 | Sol 2 | Sol 3 | Sol 4 | Sol 5 | Sol 6 |
|-----------|-------|-------|-------|-------|-------|-------|
| **Angle** | | | | | | |
| **Test speed** | | | | | | |
| **Upside** | High/Med/Low | | | | | |
| **Risk** | High/Med/Low | | | | | |
| **Effort** | | | | | | |

**Start here**: {Which test to run first and why — 2-3 sentences}

---

## Overlaps with Previous Brainstorms
{Note any overlaps, or "None"}

**Saved to**: `.claude/product/discovery/solutions/{filename}`
```

## Key Rules

- **Solutions are concepts, not specs** — no wireframes, no Jira-level detail
- **Don't skip the cheapest test** — a brainstorm without a validation path is just speculation
- **One riskiest assumption per solution** — the one that, if wrong, kills the idea entirely
- **Build on existing thinking** — always check `.claude/product/discovery/solutions/` first
- **English only**
- **Legalhero's three-sided market**: flag explicitly if a solution helps one group but harms another
