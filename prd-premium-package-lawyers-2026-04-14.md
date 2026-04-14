# PRD: Premium Package for Lawyers

**Author**: Product Management (Kaan)
**Created**: 2026-04-14
**Last Updated**: 2026-04-14
**Status**: In Progress
**Quarter**: Q2 2026
**Strategic Pillar**: Revenue & Margin Optimization / Lawyer Efficiency
**Priority**: Critical
**Jira Epic**: [CF Board](https://legal-hero.atlassian.net/jira/software/c/projects/CF/boards/14/timeline)
**Source Meetings**: 6 meetings (Feb 26 – Apr 8, 2026)

---

## Executive Summary

The Premium Package for Lawyers introduces a tiered model (Basis / Premium) that increases Legalhero's take rate from ~46% to 48.72% in Year 1 and 52% in Year 2. Instead of a hard price increase — which risks lawyer churn at the 50% psychological threshold — lawyers voluntarily opt into Premium in exchange for prioritized case access and AI efficiency tools. The first launch target is May 1, 2026 with 10 pilot firms.

---

## Problem

### What is the problem?
Legalhero's current take rate (~46%) leaves significant margin on the table. A straightforward price increase is not viable: lawyer interviews consistently show that crossing the 50/50 split feels unpartnerschaftlich, causing drop-off in both onboarding and retention. At the same time, lawyers only upgrade if there is a tangible financial benefit — efficiency messaging alone is insufficient.

### Who is affected?
- **Legalhero (internal)**: Revenue and GP1 margin are constrained by the fixed take rate.
- **Partner lawyers (Kanzleien)**: Currently lack differentiated incentives; top-performing firms have no upgrade path.
- **Operations team**: Has no mechanism to steer case quality distribution toward higher-value partners.

### Why now?
- 60% of total revenue comes from gerichtliches Arbeitsrecht, where case values (avg. €5,000+) justify a higher share.
- ~240 Kündigungen cases per month are a scarce, high-value resource that can serve as an upgrade hook for 20–25 firms.
- CaseForce migration of the phone team starts April, enabling CTL changes without touching the legacy system.

---

## Goal & Success Metrics

| Metric | Baseline | Target (Q2/Q3 2026) |
|--------|----------|----------------------|
| Take Rate | ~46% | 48.72% |
| Take Rate Year 2 | — | 52% |
| Pilot Partner Firms | 0 | 10 (by May 1) |
| Additional Annual Revenue (Y1) | — | +€280K |
| Revenue Run Rate (Y2) | €5.6M | €13.2M |
| GP1 Margin Change (Y2) | — | +80% |

---

## Solution

### Approach: Basis / Premium Tiering (not a hard price increase)

Rather than raising rates for all lawyers, we introduce an opt-in Premium tier. The decision to use a tiered model (instead of a blanket increase) was deliberate: it is repeatable, reversible, and gives lawyers agency — which dramatically reduces churn risk.

### Revenue Share Structure

| Legal Field | Basis Share (LH) | Premium Share (LH) |
|---|---|---|
| Arbeitsrecht (außergerichtlich) | 50% | 50% (unchanged) |
| Arbeitsrecht (gerichtlich) | 50% | 60% |
| Verkehrsrecht | 50% | 50% (unchanged) |
| Mietrecht | 50% | 60% |

Shares are configurable per-firm and per-flow-type in the backend. No monthly fixed fee in Phase 1 (was discussed and explicitly rejected due to complexity and weak sales argument).

### Trial & Onboarding

- New firms onboard directly into Premium trial (first month at old 50% share — no hard cut on day one).
- From the second payout cycle, the new share (60%) applies.
- No "Trial" branding externally — communication focuses on "the first payout still runs under old conditions."
- After trial: firm can stay on Premium (accepting 60% share) or drop to Basis.

### Premium Value Proposition for Lawyers

**Hook (short-term, Phase 1 — May to September):**

1. **Priority CTL Access** — Premium lawyers see new cases 1 hour before Basis lawyers in the Case Transfer List.
2. **Kündigungen Filter** — Dedicated filter in the CTL showing only Kündigungen cases to Premium lawyers (random sorting within the list to avoid all premium lawyers racing for the same top positions).
3. **Exclusive Premium Cases (Starred)** — Every 10th or 15th qualifying high-value case (criteria: Kündigungen with high Streitwert/Bruttomonatsgehalt, Zahlungsfälle, Unfallfälle) is marked with a star and visible only to Premium partners. **Important**: No active case allocation — lawyers still pull cases themselves (legal compliance requirement).
4. **Higher case acceptance limits** — Manually configurable higher caps for Premium firms.

**Retention value (long-term, Phase 2 — September+):**

5. **Unlimited AI Features** — Summaries, Email Drafting, Action Proposals, document generation without token limits (Basis gets limited free tier).
6. **Prioritized Backoffice Services** — Faster billing/payout, prioritized coverage requests (Deckungsanfragen), prioritized case intake, dedicated partner management contact.

### Communication Strategy

- Lead with **"more money through better cases"** — not software features.
- Avoid feature-heavy sales pitch; lawyers care about net income at month end.
- Sales document to compare Basis vs. Premium must be ready by May 1.

---

## Rollout Plan

### Phase 1 — May 1 to September 2026

- **Launch**: 10 pilot firms. Candidates: Liftcheck, Muno, Shamana. Explicitly exclude: Margentan.
- **Mechanism**: CTL prioritization as primary hook (Kündigungen).
- ~240 Kündigungen/month supports ~20–25 Premium firms before the hook loses scarcity value.
- Payout system adjustment target: May 5 (minor gap vs. May 1 launch is acceptable).
- New firms: Can be configured immediately even before payout system is ready.

### Phase 2 — September 2026+

- AI efficiency features must deliver measurable value once the case-access hook saturates (when 15–20+ firms are on Premium).
- Target: AI-To-Do-Liste, beA integration, full token system, PLG upgrade flows.

---

## Technical Requirements (MVP — May 1)

### 1. Agency Plan Management (Subscription Table)
New table to track firm subscription status without modifying the existing agency model.
- Fields: firm ID, subscription_type (basic/premium), start_date, end_date, trial flag
- Supports free trial windows, manual adjustments for mid-month sign-ups
- Estimate: 3 story points

### 2. CTL Priority Filter for Premium Lawyers
- Premium lawyers get a Kündigungen-specific filter in the CTL.
- Random sorting within results (prevent all premium lawyers from racing for identical first-position cases).
- Implementation in CaseForce only (not legacy CTL — phone team migrates to CaseForce in April).
- Estimate: 3 story points

### 3. Payout Calculation with Subscription-based Shares
- Subscription status is checked at monthly payout time (simplified approach — no case-by-case double accounting).
- Hard cut after trial month.
- No separate payout per case type; unified per-firm share from second payout onward.
- Estimate: 2 story points

### 4. Premium Case Marking Logic
- Backend: Logic to flag every 10th or 15th qualifying case as a "premium case."
- Qualifying criteria: Kündigungen with high Streitwert/Bruttomonatsgehalt, Zahlungsfälle, Unfallfälle.
- Premium cases are only visible in the CTL for Premium firms.

### 5. Premium Flag & Configuration in Firm Database
- Premium flag per firm in the CaseForce database.
- Connection between firm config and payout calculation.
- Configurable now for new firms, even before full payout system is live.

### 6. Premium CTL View (Two-View Architecture)
- Premium firms see a separate/enhanced CTL view with priority cases and filter.
- Basis firms see unchanged CTL.

---

## Out of Scope (Phase 1)

The following were discussed but explicitly deferred to Phase 2 or later:

- Push notifications for new cases (on hold — risk of notification overload and cases disappearing before lawyers can claim them)
- AI token counting / freemium limits for Basis plan
- Feature toggle on/off per plan
- PLG upgrade CTAs in product
- Plan comparison UI (Basis vs. Premium)
- beA integration
- Monthly fixed fee / seat-based billing
- Seat activity metric

---

## Open Questions

| Question | Owner | Due |
|---|---|---|
| How are percentage shares shown in monthly invoices? | Alex / Finance | Apr 21 |
| Which AI features get restricted on Basis plan (and at what token limit)? | Kaan | May 1 |
| How does Premium work for large multi-user firms (user-based?)? | Kaan / Lukas | May 15 |
| Is a written contract addendum legally required, or is verbal/verbal-digital sufficient? | Alex (Legal) | Apr 30 |
| How many Kündigungen cases can a Premium firm pull per month (cap)? | Kaan | Apr 21 |

---

## Risks

| Risk | Likelihood | Impact | Mitigation |
|---|---|---|---|
| AI efficiency features not ready by September → hook saturates | Medium | High | Cap Premium at 15–20 firms until AI features ship; do not oversell the efficiency story |
| Kündigungen volume insufficient for 20+ firms | Medium | Medium | Monitor case volume; restrict max Premium firms to stay within scarcity model |
| Lawyer churn at 60% share | Low | High | Trial period + "first payout at old rate" reduces perceived shock |
| Legal compliance on case allocation | Low | Critical | No active allocation; lawyers still pull cases themselves; legal review of contract addendum |

---

## Dependencies

- Phone team CaseForce migration (April) — required for CTL work to bypass legacy system.
- Payout team + Finance alignment on share calculation timing.
- Sales document ready before first pilot firm is approached.
- Legal review of contract addendum.

---

## Contract & Legal

- No new full contract required — current contracts don't specify shares (only außergerichtliche Fixgebühr).
- Solution: Premium addendum or extended Leistungsverzeichnis.
- Legal review pending (Alex): whether written agreement is legally required or verbal sign-off suffices.
- Contract versioning system to be built as part of Phase 2.

---

## Appendix: Meeting Log

| Date | Title | Key Outcomes |
|---|---|---|
| Feb 26, 2026 | LH Premium Produkt | Strategic direction set; two-pillar model (case access + AI efficiency); RISE matrix planned |
| Mar 4, 2026 | Lukas / Kaan Check In | Financial model confirmed (+47% revenue Y1, +59% Y2); technical prerequisites listed |
| Mar 18, 2026 | Kick Off | Agency plan table (3 SP), CTL filter (3 SP), payout config (2 SP); push notifications put on hold |
| Mar 26, 2026 | Follow Up | Decision: Basis-Premium model confirmed; 3-week dev estimate; rollout plan phased |
| Apr 1, 2026 | Follow Up | May 1 target locked; 60/40 share confirmed; trial = first month at 50%, hard cut from month 2 |
| Apr 8, 2026 | Check Premium | Pricing finalized (no fixed fee); premium CTL benefits defined; legal compliance requirement clarified |
