# Opportunity File Template

Use this template exactly when creating new opportunity files. Copy it, fill in every field, and delete placeholders.

---

```markdown
# Opportunities: [Short descriptive title of this source/session]

**Source**: [interview with [Name], [role] / internal feedback from [team] / analytics observation / complaint data / etc.]
**Source Date**: [YYYY-MM-DD]
**Source Author**: [Who collected/observed this]
**Stakeholder Perspective**: [lawyer / client / internal / RSV / mixed]
**Extracted**: [YYYY-MM-DD]
**Total Opportunities**: [N]

---

## Opportunity Summary

| # | Opportunity | Type | Pain | Reach | Frequency | Score | Parent |
|---|------------|------|------|-------|-----------|-------|--------|
| 1 | [Parent opportunity title] | Problem/Need | High/Medium/Low | Broad/Significant/Limited | Constant/Regular/Rare | [score] | — |
| 1.1 | [Child opportunity title] | Problem/Need | High/Medium/Low | Broad/Significant/Limited | Constant/Regular/Rare | [score] | 1 |
| 1.2 | [Child opportunity title] | Problem/Need | High/Medium/Low | Broad/Significant/Limited | Constant/Regular/Rare | [score] | 1 |
| 2 | [Parent opportunity title] | Problem/Need | High/Medium/Low | Broad/Significant/Limited | Constant/Regular/Rare | [score] | — |

---

## Opportunity Tree

```
[Parent opportunity title] [Score: N]
  ├── [Child opportunity title] [Score: N]
  └── [Child opportunity title] [Score: N]

[Parent opportunity title] [Score: N]
  ├── [Child opportunity title] [Score: N]
  └── [Child opportunity title] [Score: N]
```

---

## Detailed Opportunities

### Parent [N]: [Full opportunity title]

**Type**: Problem / Need
**Stakeholder**: [Who experiences this]
**Description**: [2-4 sentences. What is the problem, when does it occur, what are its consequences. Be specific — the reader should be able to picture the exact moment this happens in the product or workflow.]

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High/Medium/Low | [Why this rating — specific consequence or observed behaviour] |
| Reach | Broad/Significant/Limited | [Who is affected and how widely] |
| Frequency | Constant/Regular/Rare | [How often this occurs in actual use] |
| **Score** | **[N]** | |

**Supporting Evidence**:
> "[Direct quote from user or data point]"
> — [Name/Source]

**Where it occurs**: [Specific product area, workflow, or touchpoint]
**Current workaround**: [What users do today to cope — always a signal]
**Strategic relevance**: [Which Legalhero pillar(s) this connects to and why]

---

#### Child [N.N]: [Full opportunity title]

**Type**: Problem / Need
**Stakeholder**: [Who experiences this]
**Description**: [2-3 sentences. More specific than the parent — this should describe a single, observable, testable problem.]

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High/Medium/Low | [Evidence] |
| Reach | Broad/Significant/Limited | [Evidence] |
| Frequency | Constant/Regular/Rare | [Evidence] |
| **Score** | **[N]** | |

**Supporting Evidence**:
> "[Quote or data]"
> — [Source]

**Where it occurs**: [Specific location in product/workflow]
[Optional: **Proposed solution (from user)**: [If the user suggested something — note it here but keep the opportunity as a problem, not a solution]]

---

## Cross-References

### Overlaps With Existing Opportunities

| New Opportunity | Existing Opportunity | File | Notes |
|---|---|---|---|
| [New opp title] | [Existing opp title] | `[filename].md` | [How they relate — reinforcement, conflict, sub-issue] |

### New Themes Identified

1. **[Theme name]**: [Brief description of a newly emerging pattern not previously in the OST]

### Gaps & Uncertainties

1. **[Gap title]**: [What we don't yet know, what needs to be validated, what data is missing]
2. **[Gap title]**: [...]

---

## Source Notes

**Source quality**: High / Medium / Low — [Why. E.g., "live screen-share with high-performer" vs. "single verbal report, unverified"]
**Limitations**: [Single perspective? Small sample? Data not cross-validated? Note it.]
**Recommended follow-up**:
1. [Specific next action — data pull, follow-up interview question, validation test]
2. [...]
```

---

## Scoring Reference

| Score | Pain | Reach | Frequency |
|-------|------|-------|-----------|
| 3 | High — blocks workflow, causes failures, significant time cost | Broad — virtually all relevant users | Constant — every time this workflow runs |
| 2 | Medium — real friction, disrupts flow, risks errors | Significant — meaningful segment of users | Regular — multiple times per week |
| 1 | Low — minor inconvenience, easy workaround | Limited — a few specific users or edge cases | Rare — occasionally, hard to predict |

**Score = Pain × Reach × Frequency** (max 27)

## Priority Tiers

| Score | Priority | Guidance |
|-------|----------|----------|
| 18–27 | High | Actively investigate — these are worth designing solutions for now |
| 9–17 | Medium | Keep in OST, monitor for more signals, may escalate |
| 1–8 | Low | Captured for completeness — revisit if patterns emerge |

## Type Definitions

- **Problem** — a specific, observable friction or failure in the current experience
- **Need** — something missing that users require but cannot work around effectively
