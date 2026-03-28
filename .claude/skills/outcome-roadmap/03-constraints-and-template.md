# Step 4: Handle Constraints and "Forced" Outputs

Not everything on a roadmap is outcome-driven. Teams always have some work that needs to happen regardless of KRs — security patches, legal compliance, committed partnerships. These are legitimate and should be included, but clearly separated.

Add a **Committed Work** section at the end of the roadmap. These items don't need to be framed as outcomes. Just be honest: "This is happening because we have to, not because it directly moves our KRs." Listing them here prevents them from polluting the outcome sections above.

---

# Step 5: Produce the Roadmap

Write a clean Markdown file. The roadmap should feel readable — something a stakeholder can scan in 5 minutes and understand what the team is focused on, why it matters, and how success will be measured.

## Roadmap Template

```markdown
# [Product/Team Name] — Q[N] [Year] Roadmap
*[One sentence framing: what this quarter is about, what the team is optimizing for]*

---

## Quarter at a Glance

| Objective | Key Results | Status |
|---|---|---|
| [O1 short name] | [KR count] | Planned |
| [O2 short name] | [KR count] | Planned |

---

## Objective 1: [Title]

> *[1–2 sentences on why this objective matters this quarter — what's the underlying business or user context?]*

### Key Result 1.1: [Measurable outcome statement]
- **Baseline**: [current state, if known]
- **Target**: [desired state by end of quarter]
- **Why this matters**: [one sentence connecting this KR to the objective]

**Initiatives in service of KR 1.1:**

| Initiative | Type | Owner | Notes |
|---|---|---|---|
| [Name] | Bet | [Team] | [Any important context] |
| [Name] | Committed | [Team] | [Why it's committed] |

### Key Result 1.2: [Measurable outcome statement]
...

---

## Objective 2: [Title]
...

---

## Committed Work (Non-KR)

These items are planned for the quarter but don't directly contribute to the KRs above. They represent obligations, technical foundations, or risk reduction.

| Initiative | Rationale | Owner |
|---|---|---|
| [Name] | [Why it's happening] | [Team] |

---

## What We're NOT Doing This Quarter

*[Optional but valuable — a brief list of things the team considered and deliberately deprioritised, with a one-line rationale for each. This prevents scope creep and helps stakeholders understand the trade-offs made.]*

---

## Open Questions / Risks

*[Things that could affect the roadmap — dependencies, unknowns, assumptions that need validation.]*
```
