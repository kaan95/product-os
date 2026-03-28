---
name: prd
description: Create a focused Product Requirement Document (PRD) for an initiative, aligned with Legalhero's product strategy.
---

# Create Product Requirement Document

Generate a focused, readable PRD for the following initiative:

$ARGUMENTS

## Arguments

The user may provide the following optional arguments:

- **Quarter**: Target quarter (e.g., "Q2 2026"). Default: current quarter
- **Project**: Jira project key (e.g., "OS"). Default: OS
- **Priority**: Strategic priority. Options: critical, high, medium, low. Default: high
- **Create Epic**: Create a Jira epic. Options: yes, no. Default: no

## Instructions

### 1. Load Strategic Context

Before writing, review:

- **Product Strategy**: Read `.claude/product/strategy/product-strategy-2026.md`
- **Current Initiatives**: Read `.claude/product/initiatives/` folder for the target quarter
- **Company Context**: Reference `CLAUDE.md` for company mission

### 2. Research & Context Gathering

- If the initiative relates to a specific domain, review relevant docs in `.claude/documentation/`
- If there are existing Jira epics or stories, fetch them using Atlassian MCP tools
- If discovery insights exist, check `.claude/product/discovery/`

### 3. Write the PRD

Follow the output structure below. Keep it concise — the PRD should be scannable and actionable. Nobody reads 20-page PRDs.

### 4. Save the PRD

Save to `.claude/product/initiatives/{year}/{quarter}/`:
- Filename: `prd-{initiative-slug}-{date}.md`

### 5. Optionally Create Jira Epic

If `Create Epic: yes`:
- Create a Jira epic in the specified project
- Use the PRD title as epic summary
- Include a condensed version in the epic description
- Return the Jira epic URL

## Output Structure

```markdown
# PRD: {Initiative Title}

**Author**: Product Management
**Created**: {Date}
**Last Updated**: {Date}
**Status**: Draft | In Review | Approved | In Progress
**Quarter**: {Target Quarter}
**Strategic Pillar**: {Pillar Name}
**Priority**: {Priority Level}
**Jira Epic**: {Link, if created}

---

## Executive Summary

[2-3 sentences: what this is, why it matters, what success looks like.]

---

## Problem

### What is the problem?
[Clear, specific description. Focus on the problem, not the solution.]

### Evidence
[Data, user feedback, interviews, or competitive pressure that proves this is real. Be specific — bullet points are fine.]

### Impact of inaction
[What happens if we don't solve this? Quantify where possible.]

---

## Goals & Success Metrics

### Objective
[One sentence: the outcome we want.]

### Key Results
| Key Result | Baseline | Target |
|-----------|----------|--------|
| [Metric 1] | [Current] | [Target] |
| [Metric 2] | [Current] | [Target] |

---

## Solution

### Approach
[High-level description. Focus on "what" and "why", leave "how" to engineering.]

### Key Capabilities
1. **{Capability 1}**: [One-liner]
2. **{Capability 2}**: [One-liner]
3. **{Capability 3}**: [One-liner]

### Out of Scope
[What this is NOT. Prevent scope creep.]

---

## Scope & Phasing

### Phase 1: MVP
- [ ] {Feature 1}
- [ ] {Feature 2}
- [ ] {Feature 3}

**Target**: {Timeline}
**Success Criteria**: {What proves it worked}

### Phase 2: Enhanced (if applicable)
- [ ] {Feature 1}
- [ ] {Feature 2}

**Target**: {Timeline}

### Phase 3: Full Vision (if applicable)
- [ ] {Feature 1}
- [ ] {Feature 2}

---

## Risks & Open Questions

### Key Risks
| Risk | Mitigation |
|------|-----------|
| [Risk 1] | [How to mitigate] |
| [Risk 2] | [How to mitigate] |

### Open Questions
1. [Question] — Owner: [who]
2. [Question] — Owner: [who]

---

## Dependencies

| Team / Dependency | What's needed | Effort |
|-------------------|--------------|--------|
| [Team 1] | [Contribution] | [S/M/L/XL] |
| [Team 2] | [Contribution] | [S/M/L/XL] |

**Overall Size**: {T-shirt size}

---

## Decision Log

| Date | Decision | Rationale | Decided By |
|------|----------|-----------|-----------|
| {Date} | {Decision} | {Why} | {Who} |

---

## References

- [Links to strategy docs, Jira, meeting notes, designs, etc.]
```

## Writing Principles

1. **Keep it short**: If nobody reads it, it doesn't matter how thorough it is. Aim for 2-4 pages max for most PRDs.
2. **Problems before solutions**: The Problem section should be the strongest part.
3. **Evidence over opinions**: Back up claims with data or user feedback.
4. **Scope ruthlessly**: Define what's OUT as clearly as what's IN.
5. **Think in phases**: Always define an MVP that delivers value fast.
6. **No filler sections**: Skip any section that doesn't add value for this specific initiative. If there are no risks worth calling out, don't add a risks section just to have one.
7. **Tables over prose**: Use tables and bullet points over paragraphs wherever possible.

## Important Notes

- Always write in English
- Load strategic context BEFORE writing
- If the initiative doesn't align with a strategic pillar, flag it
- Quantify success metrics — no vague goals like "improve experience"
- The PRD is a living document — update as discovery progresses
- Don't over-specify the solution — leave room for engineering and design
- If creating a Jira epic, keep the description focused and reference the full PRD file
