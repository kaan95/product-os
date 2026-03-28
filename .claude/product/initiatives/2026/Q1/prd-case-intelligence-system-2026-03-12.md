# PRD: Case Intelligence System

**Author**: Product Management
**Created**: 2026-03-12
**Last Updated**: 2026-03-12
**Status**: Draft
**Quarter**: Q1–Q2 2026
**Strategic Pillar**: AI-Powered Automation
**Priority**: Critical
**Jira Epic**: —

---

## Executive Summary

The Case Intelligence System (CIS) gives lawyers a single, AI-powered priority view of their entire caseload — surfacing only what matters, with a concrete next step for every flagged case. It is the first implementation of the AI Lawyer Initiative's maturity model (steps 1+2: Summarize & Prioritize) and the primary mechanism for reducing client complaints from their current rate to below 1%. Today, Legalhero discovers neglected cases only after the RSV escalates; the CIS inverts this from reactive to proactive.

---

## Problem Statement

### What is the problem?
Lawyers and operational teams have no unified, intelligent view of case health. Risk is invisible until it erupts into a complaint. Cases stall for days or weeks — not because lawyers are negligent, but because they lack a structured signal telling them which of their 50+ active cases needs attention today. The result: preventable complaints, RSV escalations, and long-term partner and client churn.

### Who is affected?
- **Partner lawyers**: Overwhelmed by caseload, no prioritization signal, manually tracking deadlines across cases
- **Internal ops teams**: Discovering neglect reactively via RSV escalation, spending time firefighting instead of orchestrating quality
- **Clients**: Waiting weeks without status updates, filing complaints when silence persists
- **RSV partners**: Receiving client escalations that should have been prevented at the case level

### How do we know this is a problem?
- **Jan–Feb 2026**: 146 complaints analyzed; 54% justified, 42% attributable to partner lawyers — "Keine Rückmeldung" (no response) is the single largest driver with 24 cases
- **March 2026**: 42 complaints; 31% PA-attributable; one case managed for 1.5+ years without any LH oversight
- **Cyfire/Limelaw session (Feb 2026)**: Mirko (managing lawyer, ~30 attendees) stated "99% of complaints = missing or too-slow lawyer responses"
- **Current state**: Legalhero has **zero proactive case monitoring**. All neglect is discovered post-escalation.
- **Strategy**: The AI Lawyer Initiative names this the primary short-term problem to solve

### What happens if we don't solve it?
- Complaint rate remains above acceptable threshold, risking RSV partner churn
- Ops teams stay in reactive firefighting mode, unable to scale without headcount
- The AI Lawyer vision (steps 3–5 of the maturity model) has no validated foundation to build on
- Cyfire/Limelaw structural quality issues compound without a detection mechanism

### Current State
Lawyers manage cases through CaseForce but have no priority queue or risk signal. Ops teams monitor cases manually and episodically. The only feedback loop that surfaces neglect is the RSV complaint — by which point the damage is done. There is no automated flagging, no attention routing, and no suggested next actions.

---

## Goals & Success Metrics

### Objective
Reduce client complaints to <1% by giving lawyers and ops teams a proactive, AI-generated signal that surfaces case risk before it becomes a complaint.

### Key Results

| Key Result | Baseline | Target | Measurement |
|-----------|----------|--------|-------------|
| Overall complaint rate | ~2–3% | <1% | Monthly complaint tracking |
| PA-attributable complaint rate | ~42% of complaints | <0.7% absolute | Monthly complaint attribution |
| At-risk cases caught proactively vs. reactively | ~0% proactive | >60% proactive | % of complaints pre-empted by CIS flag |
| Lawyer daily active usage of priority queue | 0 | >50% of active lawyers | Product analytics |
| Time from risk signal to lawyer action | N/A (no signal exists) | <24 hours | Signal timestamp → first action timestamp |

### Leading Indicators
- % of cases with no activity >7 days that are flagged and acted on before client contacts LH
- Ops team intervention rate on CIS-flagged cases (vs. RSV-escalated cases)
- Pre-drafted action acceptance rate (% of suggested actions executed by lawyers)

### Guardrail Metrics
- Lawyer notification volume must not increase (alert fatigue is an existing pain — survey confirms)
- CIS flags must not surface false positives that erode lawyer trust in the system

---

## Strategic Alignment

### Strategic pillar
**AI-Powered Automation** (35% R&D allocation). The CIS is the foundational layer for the AI Lawyer Initiative — without proactive case detection and prioritization (steps 1+2 of the maturity model), steps 3–5 (recommendation, drafting, full automation) have no validated base to build on.

### OKR connection
- **Business Objective 4 – Customer Satisfaction**: Primary driver of <1% complaint rate and <0.7% PA-attributable complaint outcomes
- **Business Objective 1 – Lawyer Efficiency**: Priority queue and pre-drafted action steps reduce per-case cognitive overhead
- **AI Initiatives (OS-2831)**: CIS is the operational implementation of AI-powered case summaries and action proposals on the lawyer side

### Trade-offs
- By prioritizing CIS in Q1–Q2, we delay further investment in client-facing communication features and premium monetization (Phase 3 AI gating)
- Ops-first rollout means lawyers don't see the interface immediately — acceptable given the need to validate signals before exposing to partners

---

## Target Users & Stakeholders

### Primary Users

| Persona | Role | Key Need | Current Pain |
|---------|------|----------|-------------|
| Partner Lawyer | Handles 30–80+ active cases | Know which case needs attention right now | No structured signal; mentally tracking all cases |
| Legal Staff / Assistant | Supports lawyers at a Kanzlei | Surface urgent tasks for the lawyer | No visibility into case-level risk or priority |
| LH Ops Team | Quality oversight and escalation management | Catch neglect before RSV escalates | Fully reactive; no proactive tooling |

### Secondary Stakeholders
- **RSV Partners**: Benefit from fewer escalations; should be informed of proactive oversight capability as a quality differentiator
- **Managing Partners** (e.g., Mirko at Cyfire): Track lawyer workload and case health at portfolio level — CIS data could power a managing-partner view in later phases

### Jobs to Be Done
- **When** I open CaseForce in the morning, **I want to** see exactly which cases need my attention today and why, **so I can** work through my day without missing anything critical.
- **When** a case has been stalling, **I want to** receive a clear signal with a suggested next action, **so I can** resolve it quickly without having to reconstruct the case history.
- **When** an ops team member reviews the case portfolio, **I want to** see which cases are at risk, **so I can** intervene before a client complains to the RSV.

---

## Solution Overview

### Proposed Approach
A persistent, AI-generated case priority dashboard embedded in CaseForce — the lawyer's daily starting point. The AI monitors all active cases continuously, scores each case for risk and urgency, and surfaces a ranked, structured view that replaces manual case triage. Every flagged case comes with a plain-language reason and a single concrete next action.

### Key Capabilities

1. **Priority Queue**: A ranked list of cases the lawyer must address today and this week, organized into four distinct risk categories
2. **Risk-Based Sectioning**: Four sections (Complaint Risk, Client Awaiting Response, Action Required, Complaint Risk Score Overview) give the lawyer a mental model for why each case is surfaced
3. **Priority Score (0–100)**: A per-case urgency score that drives sort order, calculated from deadline proximity, last client contact, complaint signals, case status, and court date imminence
4. **Pre-Drafted Actions**: Where applicable (especially in "Client Awaiting Response"), AI-generated draft messages are available in the row for one-click review and send
5. **Temporal Grouping**: Every section splits cases into "Needs Attention Today" and "Needs Attention This Week" to reduce overwhelm
6. **Ops View**: An internal mirror of the dashboard for LH ops teams, enabling proactive intervention before RSV escalation

### What This Is NOT
- A full case management interface — this is a prioritization layer, not a replacement for the case detail view
- A client-facing product — all outputs are internal (lawyer and ops)
- A notification system — the CIS replaces notification noise with a structured, pull-based daily view
- A document summarization tool (that is a separate AI capability in OS-2831, though summaries feed the CIS context)

---

## Dashboard Specification

### Layout
Full-page interface with four named sections. Each section is divided into two temporal groups:
- **Needs Attention Today** — action required on the current business day
- **Needs Attention This Week** — action due within the next 5 working days

### Case Row Fields

| Field | Description |
|-------|-------------|
| Case Number | Unique identifier |
| Client Name | Full name or company |
| Reason Surfaced | Plain-language explanation of why this case is flagged |
| Concrete Action Step | Single, specific next action for the lawyer |
| Priority Score | 0–100 urgency score |

Rows are compact by default; expandable for full context.

### Section Definitions

**1. Complaint Risk**
Cases where a complaint is likely based on behavioral signals: unanswered messages, long wait times, negative developments. Sorted by complaint likelihood score (highest first). Each row includes a recommended de-escalation action.

**2. Client Awaiting Response**
Cases where the client is waiting on a reply. Pre-drafted response messages available inline for one-click review and send.

**3. Action Required**
Cases with a specific legal task pending or overdue (not covered by sections 1–2):
- Lawsuit to file or revise
- Reply brief (Replik) to draft
- Email to opposing counsel
- Expiring deadlines
- Court hearings without assigned TV
- Missing Vollmacht

Displays current case status (e.g. *Awaiting Opponent*, *Awaiting Document*, *Blocked*) alongside the action step.

**4. Complaint Risk Score Overview**
At-a-glance ranking of all cases by long-term complaint risk, independent of immediate action needs. Factors: communication frequency, time since last update, case duration, outcome trajectory.

### Priority Score Calculation
Inputs (weighted):
- Deadline proximity
- Time since last client contact
- Complaint risk factors (communication gaps, negative sentiment signals)
- Whether the case is blocked vs. actively progressing
- Court date imminence

Score thresholds:
- **80–100**: Same-day urgency — appears in "Needs Attention Today"
- **50–79**: This-week priority — appears in "Needs Attention This Week"
- **<50**: Monitoring only — surfaced in Complaint Risk Score Overview

---

## Assumptions & Risks

### Key Assumptions

| Assumption | Risk if Wrong | Validation Method | Status |
|-----------|--------------|-------------------|--------|
| AI can accurately detect cases at risk from existing case data | CIS surfaces false positives, lawyers stop trusting it | Pilot with ops team reviewing AI flags before lawyer rollout | Untested |
| Lawyers will adopt a pull-based dashboard as their daily routine | Low engagement, habit not formed | Usage analytics in first 4 weeks post-launch | Untested |
| Pre-drafted action messages are good enough to send without significant edits | Lawyers dismiss them, no efficiency gain | Track edit rate and send rate in pilot | Untested |
| Ops teams will act on AI flags proactively | Ops continues reactive behavior despite tooling | Monitor ops intervention rate before vs. after CIS | Untested |
| Priority score accurately reflects complaint risk | Wrong cases surfaced, real risks missed | Retrospective: did flagged cases correlate with eventual complaints? | Untested |

### Risks & Mitigations

| Risk | Likelihood | Impact | Mitigation |
|------|-----------|--------|-----------|
| Alert fatigue — CIS flags too many cases | Medium | High | Cap daily "Today" rows; ruthless scoring threshold; pilot with 5 lawyers first |
| Low lawyer adoption — habit not formed | Medium | High | Ops-first rollout to validate signal quality; make CIS the default landing page |
| AI accuracy too low to trust | Medium | High | Require >90% signal accuracy in internal ops pilot before lawyer-facing rollout |
| Scope creep into full case management features | High | Medium | Strict "prioritization layer only" constraint; no case editing from CIS in Phase 1 |
| Cyfire/Limelaw structural issues mask CIS impact | Low | Medium | Track complaint rate by firm; separate Cyfire metrics from overall baseline |

### Open Questions

1. What data sources feed the risk score calculation? — Owner: Engineering + Data
2. What is the minimum data completeness threshold for a case to be included in CIS? — Owner: Product + Engineering
3. How does CIS handle cases where the lawyer is on vacation / cases are delegated? — Owner: Product
4. Should ops and lawyers see the same view or different prioritization logic? — Owner: Product
5. How do we prevent surfacing the same case every day if the lawyer takes no action? — Owner: Product + Engineering

---

## Scope & Phasing

### Phase 1: MVP — Ops-First Internal Dashboard (Q1 2026)
Validate signal quality before exposing to lawyers. Build the risk detection and scoring engine; surface it internally.

- [ ] AI case risk scoring engine (Priority Score 0–100)
- [ ] Ops-facing dashboard: Complaint Risk + Action Required sections
- [ ] Temporal grouping (Today / This Week)
- [ ] Case row format: Case Number, Client Name, Reason Surfaced, Action Step, Priority Score
- [ ] Manual flagging capability for ops to override or dismiss signals

**Target**: End of Q1 2026
**Success Criteria**: Ops team catches >30% of at-risk cases proactively (before RSV escalation) using CIS. Signal accuracy >90% (validated retrospectively against complaint data).

### Phase 2: Lawyer-Facing Dashboard (Q2 2026)
Roll out the priority queue to lawyers once signal quality is validated.

- [ ] Lawyer-facing version of all four sections
- [ ] Pre-drafted action messages in "Client Awaiting Response" rows
- [ ] Expandable case rows with full AI-generated case context
- [ ] Default landing page behavior in CaseForce
- [ ] Push notification (single daily digest, not per-event) linking to CIS

**Target**: Q2 2026
**Success Criteria**: >50% of active lawyers open CIS daily. Complaint rate trending toward <1%.

### Phase 3: AI Copilot Integration (Mid-term)
Connect CIS to action-taking capabilities — when CIS says "send a status update", the AI has already drafted it.

- [ ] One-click send of pre-drafted emails from CIS
- [ ] Document drafting initiated from CIS action step
- [ ] Premium partner feature gating tied to CIS engagement rate

### Explicitly Out of Scope (all phases)
- Client-facing view of case priority or risk
- Full case editing or document upload from CIS
- RSV partner-facing reporting (separate initiative)
- Managing-partner portfolio view (Phase 3 consideration)

---

## Dependencies & Resources

### Team Dependencies

| Team | Contribution | Effort Estimate |
|------|-------------|----------------|
| AI/Data Squad | Risk scoring model, case data pipeline, signal accuracy validation | L |
| CaseForce Frontend | Dashboard UI, case row components, expandable rows, temporal grouping | M |
| Backend/API | CIS data API, case metadata aggregation, ops override capabilities | M |
| Ops Team | Pilot participants, signal feedback, adoption validation | Ongoing |

### External Dependencies
- Case data completeness (CIS is only as good as the data it reads — email verification, document processing, and case status accuracy all feed signal quality)
- OS-2831 (AI Initiatives – Lawyer Side): case summaries generated by OS-2831 should feed CIS "Reason Surfaced" field
- OS-2477 (KPI Tracking): measurement infrastructure required to track CIS success metrics

### Estimated Effort
**Overall Size**: L (Phase 1) + M (Phase 2) — expect 8–12 weeks combined for MVP through lawyer rollout

---

## Decision Log

| Date | Decision | Rationale | Decided By |
|------|----------|-----------|-----------|
| 2026-03-12 | Ops-first rollout before lawyer-facing | Validates AI signal quality without risking lawyer trust on unproven outputs | PM |
| 2026-03-12 | Pull-based dashboard instead of push notifications | Notification fatigue is a top lawyer pain point; structured daily view is less disruptive | PM |
| 2026-03-12 | Four-section structure over single ranked list | Sections give lawyers a mental model for *why* a case is surfaced, not just *that* it is | PM |

---

## References & Related Documents

- [Product Strategy 2026–2028](../../strategy/product-strategy-2026.md)
- [AI Lawyer Initiative Strategy](../../strategy/ai-lawyer-initiative-strategy.md)
- [Q1 2026 Initiatives](initiatives-q1-2026.md) — see OS-2831 (AI Lawyer Side), OS-2477 (KPI Tracking)
- [Complaint Insights March 2026](../../discovery/opportunities/complaints/complaint-insights-march-2026.md)
- [Complaint Insights Jan–Feb 2026](../../discovery/opportunities/complaints/complaint-insights-jan-feb-2026.md)
- [Lawyer Case Neglect Solutions](../../discovery/solutions/lawyer-case-neglect-solutions-2026-03-10.md)
- [Complaint Reduction Brainstorm](../../discovery/solutions/complaint-reduction-brainstorm-2026-03-06.md)
- [Cyfire Product Interview](../../discovery/opportunities/interview-cyfire-lh-product-2026-03-03.md)
- Designs: TBD
- Technical Spec: TBD
