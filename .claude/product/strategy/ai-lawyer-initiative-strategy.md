# AI Lawyer Initiative — Strategy

*Created: 2026-03-12*

## Position

The AI Lawyer Initiative has a clear strategic direction — reduce complaints now, build toward full case automation — but the current notes conflate three things: an immediate operational fix, a product capability roadmap, and a long-term vision. The 5-step maturity model is the spine of the entire strategy and should structure all three horizons. The core strength is that discovery data (complaint analysis, Cyfire session) directly validates the problem. The key risk: step 4 (Navigator → Copilot) is the hardest capability jump and receives the least attention.

---

## The 5-Step AI Maturity Model

| Step | Capability | Horizon |
|------|-----------|---------|
| 1 | **Summarize & Understand** — AI reads every case, creates context summary | Short-term |
| 2 | **Prioritize & Focus** — AI tells lawyers which cases need attention today | Short-term |
| 3 | **Recommend & Decide** — AI suggests concrete actions; lawyer decides | Mid-term |
| 4 | **Draft & Review** — AI prepares the work; lawyer approves (Navigator → Copilot) | Mid-term |
| 5 | **Automate End-to-End** — AI handles cases autonomously; lawyer for decisions only | Long-term |

---

## Insights

- **The 5-step model IS the strategy — it spans all three horizons, not just mid-term.** Restructuring around this makes the narrative more coherent and shows a credible path to the vision.
- **Short-term is a defensive play; name it clearly.** The immediate goal isn't "efficiency" — it's preventing complaints by catching neglected cases before the RSV escalates. Discovery confirms: 99% of complaints = missing/slow responses, and LH has zero proactive detection today.
- **Step 4 (Navigator → Copilot) is where the moat is built.** The differentiation is when Legalhero's AI *prepares the work* — drafts the document, pre-fills the email — so lawyers approve in seconds. This is the hardest step technically and the stickiest for retention.
- **"Lawyers only approve things" needs a governance model now.** What specifically requires a lawyer signature vs. what can be fully automated? Defining this early shapes the product architecture and manages regulatory risk.
- **The data flywheel is the real long-term moat, not the AI itself.** Proprietary German legal case data + outcomes + document patterns = an asset competitors can't replicate.

---

## Short-term (this year)

**Core Problem**

Operational teams and lawyers lack a unified, intelligent view of case health. Risks are discovered reactively — usually after a client complains or the RSV escalates. The goal of the Case Intelligence System is to invert this: proactive detection, directed attention, suggested action.

**Goals**

- Complaints become an exception and are proactively prevented by lawyers
- Operational teams move from reactive fire-fighting to proactive quality orchestration
- Lawyers have a clear priority queue to know which cases need their attention
- Lawyers work more efficiently through AI-assisted work

**Key Initiatives**

- AI Case Monitor: single view that summarizes every case and surfaces a priority queue per lawyer (maturity steps 1+2)
- Ops-first rollout: internal flagging tool before lawyer-facing product
- One nudge mechanism: automated trigger for cases with no activity in 7 days → pre-drafted action
- KPI infrastructure: complaint attribution and AI action-execution rates (OS-2477)

**Key Metrics**

- Reduction in complaint rate (primary, target: <1%)
- Time from risk signal to lawyer action
- Percentage of at-risk cases caught proactively vs. reactively
- Lawyer daily active usage of priority queue
- Operational team intervention rate on flagged cases

---

## Mid-term (next 1–2 years)

**Core Problem**

Surfacing risk is not enough — lawyers need the AI to not just tell them what to do, but prepare the work so they can approve in seconds. This is the Navigator → Copilot transition: the hardest capability jump and the point where Legalhero's moat becomes defensible.

**Goals**

- AI moves from surfacing problems to proposing and preparing solutions (maturity steps 3+4)
- Lawyers approve work in <2 minutes instead of writing from scratch
- Premium partner access is tied to AI engagement, creating a retention mechanism
- Automation tolerance is validated by case type and action category

**Key Initiatives**

- Step 3: Action recommendations with one-click execution ("Case X needs a status update — here's a draft. Send?")
- Step 4: Full work preparation — AI pre-drafts documents, emails, filings for lawyer review
- Premium Package Phase 3: gate advanced AI features (steps 3+4) behind premium tier
- Structured validation: which case types and actions do lawyers trust AI to prepare?

**Key Metrics**

- % of AI-suggested actions executed by lawyers (target: >30%)
- Document/email draft time (target: <2 minutes for lawyer review + approval)
- AI feature engagement rate among Premium partners
- AI output accuracy (must exceed 90% before advancing to step 4)

---

## Long-term (3+ years)

**Vision**

AI steers and orchestrates legal work end-to-end. Legalhero operates an AI legal workforce that partner lawyers plug into: they get case inflow and AI tools; Legalhero gets the operational leverage. The AI Lawyer is not a feature — it is Legalhero's platform infrastructure.

**Goals**

- Routine cases handled end-to-end by autonomous AI agents (maturity step 5)
- Lawyers function as decision-makers and exception handlers, not case processors
- Legalhero's proprietary case data creates a compounding moat that competitors cannot replicate

**Key Bets**

- Automation boundary defined: specific case types, actions, and decisions that can be fully automated within German legal frameworks (RDG, BRAO)
- Data flywheel formalized: every case outcome (settlement, verdict, complaint, duration) feeds back into the model
- Platform play: AI Lawyer positioned as Legalhero infrastructure, not point feature

**Indicators of Success**

- % of cases processed without lawyer active involvement
- AI model accuracy improvement rate over time (compounding data advantage)
- Lawyer-to-case ratio (fewer lawyers needed per case volume = margin expansion)
- RSV willingness to expand case volume based on AI-driven quality and speed guarantees

---

## Open Questions

- **What's the automation boundary under German law?** Fully automated case handling faces regulatory scrutiny (RDG, BRAO). What's the minimum lawyer touchpoint required, and does the architecture account for this?
- **Do lawyers accept being "approvers"?** Discovery shows openness to communication automation, but is there a threshold where they feel replaced rather than empowered? Needs explicit validation.
- **What's the accuracy gate between maturity steps?** One bad AI recommendation at step 3 poisons adoption at step 4. Define the minimum validated accuracy bar before advancing.
- **Is the maturity model linear?** A large firm might be ready for step 3 immediately; a small PA firm might need step 1 for months. Does the product support non-linear adoption paths?
