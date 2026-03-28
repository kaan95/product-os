---
name: opportunity-extraction
description: Extract and size product opportunities from any input source (interview transcripts, PRDs, complaint data, research, etc.) using Teresa Torres' Continuous Discovery Habits framework. Saves structured opportunities to the discovery backlog.
---

# Extract & Size Opportunities

Extract product opportunities from the provided input and add them to the opportunity backlog, sized using Teresa Torres' Continuous Discovery Habits framework.

$ARGUMENTS

## Arguments

The user may provide the following arguments:

- **Source** (required): The input to extract opportunities from. Can be:
  - Pasted text (interview transcript, notes, feedback, etc.)
  - A file path to read
  - A reference to an existing document in the project (e.g., "the complaint insights file")

- **Source Type** (optional): What kind of input this is. Options: interview, prd, complaints, research, feedback, meeting-notes, support-tickets, other. Default: inferred from content
- **Source Date** (optional): When the source material was created/collected. Default: today
- **Source Author** (optional): Who created the source material
- **Stakeholder Group** (optional): Primary stakeholder perspective in the source. Options: client, lawyer, rsv, internal, mixed. Default: inferred from content
- **Merge Mode** (optional): How to handle opportunities that may overlap with existing ones. Options: append, merge, replace. Default: append
  - `append` — Always create new entries, even if similar ones exist
  - `merge` — Check existing opportunities and merge new evidence into existing ones where there's clear overlap; create new entries for genuinely new opportunities
  - `replace` — Replace the existing opportunity file for this source (use when re-processing a source)

## Instructions

### 1. Load Existing Context

Before extracting, review existing opportunities to understand what's already been captured:

- **Existing Opportunities**: Read all files in `.claude/product/discovery/opportunities/` to understand what's already documented
- **Product Strategy**: Skim `.claude/product/strategy/product-strategy-2026.md` to understand strategic context (helps with relevance assessment)
- **Company Context**: Reference `CLAUDE.md` for stakeholder definitions and company positioning

### 2. Read and Analyze the Source

Carefully read the entire source material. For each opportunity you identify, look for:

- **Pain points**: Explicit frustrations, complaints, things going wrong
- **Unmet needs**: Gaps, missing capabilities, workarounds people use
- **Desires**: Wishes, aspirations, "it would be great if..." statements
- **Behavioral signals**: What people do (or avoid doing) that reveals an unmet need
- **Frequency indicators**: Words like "always", "every time", "constantly", "sometimes", "rarely"
- **Reach indicators**: Words like "everyone", "most of us", "a few", "some clients", specific numbers
- **Severity indicators**: Emotional language, escalation, workarounds, time/money lost

### 3. Extract Opportunities

For each opportunity identified:

1. **Write it from the customer/stakeholder perspective** — not as a feature or solution
   - Good: "Clients wait weeks without hearing from their assigned lawyer"
   - Bad: "Build automated status update notifications"

2. **Classify the type**:
   - **Problem**: Something going wrong, a frustration, an obstacle
   - **Need**: Something required or missing
   - **Desire**: An aspirational want

3. **Size the opportunity** using three dimensions (Teresa Torres, Continuous Discovery Habits):

   **Pain Level** — How painful is this problem when it occurs?
   - `High`: Causes significant harm, financial loss, relationship damage, or blocks critical workflows. Stakeholders are visibly frustrated or escalating.
   - `Medium`: Causes meaningful inconvenience, wasted time, or suboptimal outcomes. Stakeholders are annoyed but can work around it.
   - `Low`: Minor irritation or inefficiency. Stakeholders notice but aren't significantly affected.

   **Reach** — How many people/cases are affected?
   - `Broad`: Affects most or all users/cases in the relevant segment (>60%)
   - `Significant`: Affects a meaningful portion (20-60%)
   - `Narrow`: Affects a small subset (<20%)
   - If specific numbers are available from the source, include them

   **Frequency** — How often does this occur?
   - `Constant`: Happens daily or on nearly every case/interaction
   - `Regular`: Happens weekly or on a significant share of cases
   - `Occasional`: Happens monthly or sporadically
   - `Rare`: Happens infrequently but with notable impact when it does

4. **Calculate an Opportunity Score** (for relative prioritization):
   - Pain: High=3, Medium=2, Low=1
   - Reach: Broad=3, Significant=2, Narrow=1
   - Frequency: Constant=3, Regular=2, Occasional=1, Rare=0.5
   - **Score = Pain × Reach × Frequency** (max 27, min 0.5)

5. **Capture supporting evidence**:
   - Direct quotes where available
   - Data points (numbers, percentages, counts)
   - Context: where/when this occurs in the stakeholder's experience

6. **Identify the parent opportunity** (if applicable):
   - Group related opportunities under broader parent themes
   - A parent opportunity is a higher-level framing that contains multiple sub-opportunities

### 4. Organize into Opportunity Hierarchy

Structure the extracted opportunities into Teresa Torres' Opportunity Solution Tree format:
- **Parent opportunities** are broad, strategic-level problems/needs
- **Child opportunities** are specific, actionable sub-problems
- One parent can have many children; children can also have sub-children

### 5. Check for Overlaps (if Merge Mode = merge)

If merge mode is set to `merge`:
- Compare each extracted opportunity against existing opportunity files
- If a clear match exists, note the new evidence to add to the existing opportunity
- Only create new entries for genuinely distinct opportunities
- Flag any opportunities that might overlap but where you're uncertain

### 6. Save Opportunities

Save the output as a single structured document to:
- **Path**: `.claude/product/discovery/opportunities/{source-slug}-{date}.md`
- **Naming**: Use a descriptive slug based on the source (e.g., `interview-rsv-partner-2026-03-03.md`, `support-ticket-analysis-2026-03-03.md`)

If merge mode is `replace` and a file for this source already exists, overwrite it.

### 7. Summarize to User

After saving, present:
- Total number of opportunities extracted
- Top 5 opportunities by score
- Any opportunities that overlap with previously documented ones
- The saved file path

## Output Structure

```markdown
# Opportunities: {Source Description}

**Source**: {Source type and description}
**Source Date**: {Date}
**Source Author**: {Author, if known}
**Stakeholder Perspective**: {client / lawyer / rsv / internal / mixed}
**Extracted**: {Current date}
**Total Opportunities**: {Count}

---

## Opportunity Summary

| # | Opportunity | Type | Pain | Reach | Frequency | Score | Parent |
|---|------------|------|------|-------|-----------|-------|--------|
| 1 | {Short description} | Problem/Need/Desire | H/M/L | Broad/Significant/Narrow | Constant/Regular/Occasional/Rare | {X} | {Parent name or —} |
| 2 | ... | ... | ... | ... | ... | ... | ... |

---

## Opportunity Tree

```
{Parent Opportunity 1} [Score: X]
  ├── {Child Opportunity 1.1} [Score: X]
  ├── {Child Opportunity 1.2} [Score: X]
  │   └── {Sub-child 1.2.1} [Score: X]
  └── {Child Opportunity 1.3} [Score: X]

{Parent Opportunity 2} [Score: X]
  ├── {Child Opportunity 2.1} [Score: X]
  └── {Child Opportunity 2.2} [Score: X]
```

---

## Detailed Opportunities

### {Parent Opportunity 1}: {Title}

**Type**: Problem / Need / Desire
**Stakeholder**: {Who experiences this}
**Description**: {2-3 sentence description from the stakeholder's perspective}

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | {High/Medium/Low} | {Why this rating — what harm does it cause?} |
| Reach | {Broad/Significant/Narrow} | {Why this rating — how many affected? Include numbers if available} |
| Frequency | {Constant/Regular/Occasional/Rare} | {Why this rating — how often does it occur?} |
| **Score** | **{X}** | |

**Supporting Evidence**:
> "{Direct quote or data point}"
> — {Source context}

> "{Additional quote or data point}"
> — {Source context}

**Where it occurs**: {Point in the stakeholder journey/workflow where this happens}
**Current workaround**: {How stakeholders cope today, if mentioned}
**Strategic relevance**: {Brief note on how this connects to product strategy, if applicable}

---

#### Child: {Opportunity 1.1 Title}

**Type**: Problem / Need / Desire
**Stakeholder**: {Who experiences this}
**Description**: {Description from stakeholder's perspective}

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | {Rating} | {Evidence} |
| Reach | {Rating} | {Evidence} |
| Frequency | {Rating} | {Evidence} |
| **Score** | **{X}** | |

**Supporting Evidence**:
> "{Quote or data}"
> — {Context}

---

[Continue for all opportunities...]

---

## Cross-References

### Overlaps with Existing Opportunities
{List any opportunities that overlap with previously documented ones, with file references}

### New Themes Identified
{List any entirely new themes or patterns not previously captured}

### Gaps & Uncertainties
{List opportunities where the sizing is uncertain due to limited data — flag for further discovery}

---

## Source Notes

**Source quality**: {How rich/reliable was this source for opportunity extraction?}
**Limitations**: {What couldn't be determined from this source?}
**Recommended follow-up**: {Suggestions for further discovery to validate or refine these opportunities}
```

## Sizing Guidance

When sizing, follow these principles from Teresa Torres:

1. **Use evidence, not gut feeling**: Base ratings on what the source material actually says. If the source doesn't provide enough information for a confident rating, mark it as uncertain and flag for follow-up.

2. **Pain Level is about severity, not frequency**: A problem that causes catastrophic harm once a year can be High pain even if rare. Pain Level captures "how bad is it when it happens?"

3. **Reach is about breadth of impact**: How many people in the relevant stakeholder group experience this? Look for quantitative signals (percentages, counts) and qualitative signals ("everyone", "some clients").

4. **Frequency is about recurrence**: How often does this opportunity surface? Daily irritation vs. quarterly inconvenience. Look for temporal language and repetition patterns.

5. **The score is directional, not definitive**: The multiplicative score helps with rough prioritization. A 27 is clearly bigger than a 2. But don't over-index on precise scores — the dimensional breakdown (Pain × Reach × Frequency) is more useful for understanding the shape of the opportunity.

6. **When data is ambiguous, be conservative**: It's better to underestimate and be surprised than to overestimate and waste effort on a small opportunity.

7. **Separate evidence from inference**: If you're inferring a rating (e.g., "this is probably Broad reach because it's a systemic process issue"), say so explicitly. Distinguish hard data from reasonable assumptions.

## Important Notes

- **Opportunities are NOT solutions**: Never frame an opportunity as a feature to build. Frame it as a problem, need, or desire from the stakeholder's world.
- **Stay faithful to the source**: Don't invent opportunities that aren't supported by the source material. If you infer something implicit, mark it clearly.
- **Preserve specificity**: "Clients don't know what's happening with their case" is better than "Communication is bad." Be specific about who, what, and when.
- **Include counter-evidence**: If the source contains information that contradicts or qualifies an opportunity, include that too.
- **Write in English**: All opportunity documentation should be in English, even if the source material is in German. Preserve original German quotes in the evidence where useful.
- **One file per source**: Each extraction run produces one file. The opportunity tree within that file may reference parent opportunities that span multiple sources — that's fine.
- **Flag strategic opportunities**: If an opportunity clearly connects to a strategic pillar from the product strategy, note the connection.
