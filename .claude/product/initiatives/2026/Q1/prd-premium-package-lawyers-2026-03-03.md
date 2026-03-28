# PRD: Premium Package Lawyers

**Author**: Product Management (Kaan Ozgiray)
**Created**: 2026-03-03
**Last Updated**: 2026-03-17
**Status**: In Progress
**Quarter**: Q2 2026
**Strategic Pillar**: Platform Orchestration + Data-Driven Infrastructure
**Priority**: Critical
**Jira Discovery**: [PD-78](https://legal-hero.atlassian.net/browse/PD-78)

---

## Executive Summary

Introduce a two-tier partner model (Basic vs. Premium) that exchanges higher share for prioritized case access, fastlane document processing, and AI features. New agencies get a 2-month free trial with PLG-driven self-service conversion.

**Projected impact**: +€280K revenue in Year 1 (starting May), take-rate from ~46% to 48.72%, revenue €5.6M → €8.2M (+47%). Year 2: take-rate 52%, revenue €13.2M (+59%). Investment: ~5 FTEs (Team Anwaltseffizienz).

---

## Problem

### What is the problem?

Take rate from partner lawyers has plateaued at ~46%. Increasing prices without additional value isn't viable — partners already see 50-50 as the upper limit. Meanwhile, AI features (summaries, actions, doc generation) are available to all partners for free with no monetization path and no differentiation between engaged and passive partners.

### Evidence

- **Partner Survey**: All respondents would only accept higher shares if net income increases
- **Partner Interviews (2 deep-dives)**: Lawyers care exclusively about financial outcome, not AI features
- **Sales Feedback**: Conversion drops significantly at or above 50% share
- **Financial Model**: gerichtliches Arbeitsrecht 50% → 60% = +€74K/month
- **Case Supply**: Only ~70% of inbound cases accepted — redistribution capacity exists
- **March 4 Model**: €280K additional revenue in first year, GP1 margin +80% YoY

### Impact of inaction

- Revenue growth limited to case volume growth only — no margin lever
- ~€840K/year unrealized revenue on gerichtliche Arbeitsrecht alone
- AI features stay free forever with no monetization path
- Competitors could offer tiered models first

---

## Goals & Success Metrics

### Objective

Increase average take rate through a tiered model that delivers measurable value to lawyers while growing platform revenue per case.

### Key Results

| Key Result | Baseline | Target |
|-----------|----------|--------|
| Average take rate | ~46% | 48.72% (Y1), 52% (Y2) |
| Annual platform revenue | €5.6M | €8.2M (Y1), €13.2M (Y2) |
| GP1 margin growth | Baseline | +80% YoY |
| Premium pilot partners | 0 | 10 (May-July) |
| Take rate Arbeitsrecht | ~50% | 54% (+4%) |
| Take rate Verkehrsrecht | Baseline | +10% + €229 fixed fee |
| Take rate Mietrecht | Baseline | +5% |

---

## Solution

### Approach

**Basic Plan** (default): Standard share rates, standard CTL, 20-25 free AI tokens/month, standard doc processing.

**Premium Plan** (voluntary upgrade): Higher share (e.g., 60% gerichtl. Arbeitsrecht), CTL priority for Kundigungen, unlimited AI, fastlane doc processing (1-day guarantee), push notifications for new cases.

**PLG Strategy**: 2-month free Premium trial for new agencies → auto-downgrade to Basic → upgrade CTAs at all touchpoints (AI limit reached, email drafting, empty case list, token counter). Plan applies to entire organization, not per seat. Activity-based seat billing (inactive = not charged).

### Key Capabilities

1. **CTL Priority Cases** — Premium partners see Kundigungen first
2. **Fastlane Document Processing** — 1-business-day guarantee for Premium
3. **Push Notifications** — Real-time alerts for new CTL cases
4. **Agency Plan Management** — Assign agencies to Basic/Premium; toggle features on/off per plan
5. **AI Token System** — 20-25 free tokens/month (Basic), unlimited (Premium), counter in UI
6. **Per-Kanzlei Share Config** — Flexible rate per agency and per Rechtsgebiet/flow type
7. **Trial Mode** — 2-month Premium trial, auto-downgrade, PLG upgrade CTAs
8. **Plan Comparison UI** — Side-by-side Basic vs. Premium

### Out of Scope

- Forced price increases or mandatory migration
- Client-facing changes
- RSV partner pricing changes
- Full billing system rewrite
- ML-based case matching (V1-V2 use simple priority)
- Per-seat plan management (plans are per agency)

---

## Scope & Phasing

### V1: Core Premium — Pilot with 10 Agencies (Q2 2026, May-July)

- [ ] CTL Priority Cases for Premium partners
- [ ] Fastlane Document Processing (1-day guarantee)
- [ ] Push Notifications for new CTL cases
- [ ] Agency Plan Management (Basic vs. Premium)
- [ ] Feature Toggle System (on/off/limited per plan)
- [ ] Per-Kanzlei / Per-Flow-Type Share Configuration
- [ ] AI Token System (20-25 free/month Basic, unlimited Premium)
- [ ] Kundigung case limit for non-Premium

**Target**: May 2026
**Success Criteria**: 10 pilot agencies onboarded, billing processes differentiated shares correctly, no increase in partner churn

### V2: PLG & Self-Service Conversion (Q3 2026)

- [ ] 2-month Premium trial for new agencies + auto-downgrade
- [ ] PLG upgrade CTAs at all key touchpoints
- [ ] Plan Comparison UI
- [ ] Contract Versioning System + AGBs update
- [ ] Active Seat Billing (activity-based)
- [ ] Business Case Calculator for Sales
- [ ] Range-based pricing materials

**Target**: Q3 2026
**Success Criteria**: Trial-to-Premium conversion >30%, self-service upgrades >50% of conversions, take rate reaches 48.72%

### V3: AI Gating & Performance (Q4 2026)

- [ ] Advanced AI feature gating (refined limits per feature type)
- [ ] Efficiency dashboards for Premium partners
- [ ] Gamification (ranking, XP, variable payout)
- [ ] ML-based priority distribution
- [ ] Enterprise tier exploration

**Target**: Q4 2026
**Success Criteria**: 20% of AI-active partners upgrade based on AI value, take rate reaches 52%

---

## Risks & Open Questions

### Key Risks

| Risk | Mitigation |
|------|-----------|
| Partner backlash when they learn about different terms | Phased rollout; pilot with friendly partners first; no public announcement initially |
| Billing system changes delayed | Start technical spike now; manual workaround for first pilots if needed |
| Not enough Kundigungen to fulfill Premium promise | Analyze CTL data first; don't over-commit on volume |
| New partner conversion drops >30% | Monitor weekly; adjust pricing/ranges; prepare fallback |
| Fastlane 1-day SLA consistently missed | Build monitoring; start with 2-day guarantee and tighten |
| AI features still don't feel valuable | V1 focuses on case access + fastlane (proven motivators), not AI |

### Open Questions

1. **Min viable billing change for per-Kanzlei shares?** — Owner: Kaan & Engineering
2. **Do existing contracts allow differentiated pricing, or new Vertragsgeneration needed?** — Owner: Legal
3. **How many Kundigungen can be redirected without starving Basic partners?** — Owner: Operations/Data
4. **Right AI token limit (20 vs. 25/month)?** — Owner: Product (analyze during pilot)
5. **What defines "active seat" for billing?** — Owner: Product + Finance
6. **Fastlane ops model: dedicated queue, staff, or SLA-based prioritization?** — Owner: Operations

---

## Dependencies

| Team / Dependency | What's needed | Effort |
|-------------------|--------------|--------|
| Engineering (Backend) | Billing per-Kanzlei; CTL priority; feature toggles; token system; push notifications | XL |
| Engineering (Frontend) | Plan comparison UI; token counter; upgrade CTAs; admin panel | L |
| Finance Operations | Validate billing; pilot invoices; seat billing rules | M |
| Sales | Pilot partner pitches; conversion feedback | M |
| Legal | Contract review; AGBs update; compliance sign-off | S |
| Operations | Fastlane doc processing; pilot partner management | M |
| Business (Alex/Elmar) | Business case calculator; financial modelling | M |

**Overall Size**: XL (3-4 months V1+V2, 6+ months through V3)

---

## Decision Log

| Date | Decision | Rationale | Decided By |
|------|----------|-----------|-----------|
| 2026-02-26 | New partners at 55% (Arbeitsrecht) / 50% (Verkehrsrecht) | Need new baseline above 50-50 | Team |
| 2026-02-26 | Premium targets 60% share for gerichtl. Arbeitsrecht | +€70K/month; €5K case value makes €200 extra acceptable | Team |
| 2026-02-26 | Primary sell is case access, not AI features | Interviews confirm only financial outcome motivates lawyers | Team |
| 2026-02-26 | Range-based pricing in sales conversations | Avoids psychological barrier of fixed % above 50 | Team |
| 2026-03-04 | PLG strategy with 2-month free trial | Self-service conversion more scalable than sales-driven | Lukas & Kaan |
| 2026-03-04 | 20-25 free AI tokens/month, each action = 1 token | Creates upgrade pressure without frustration; Lovable-style model | Lukas & Kaan |
| 2026-03-04 | Plan upgrade per organization, not per seat | Simplifies billing; consistent experience per Kanzlei | Lukas & Kaan |
| 2026-03-04 | Activity-based seat billing | Fair model; prevents pushback on unused seats | Lukas & Kaan |
| 2026-03-04 | Take-rate: AR +4%, MR +5%, VR +10% + €229 fixed | Based on financial model showing €280K additional Y1 revenue | Lukas & Kaan |
| 2026-03-17 | V1 scope defined | Minimum features for tangible Premium value and pilot | Kaan |

---

## References

- **Strategy**: [Product Strategy 2026-2028](../../strategy/product-strategy-2026.md)
- **Jira**: [PD-78](https://legal-hero.atlassian.net/browse/PD-78), [PD-82](https://legal-hero.atlassian.net/browse/PD-82) (CTL Detail), [PD-83](https://legal-hero.atlassian.net/browse/PD-83) (CTL Prio), [PD-84](https://legal-hero.atlassian.net/browse/PD-84) (Push Notifications), [PD-85](https://legal-hero.atlassian.net/browse/PD-85) (BI Report)
- **Meetings**: [Premium Produkt (Feb 26)](https://www.notion.so/3135e8cace39802b8c6cc6ee4a87312b), [Check-In (Mar 4)](https://www.notion.so/3195e8cace39804db2c4f6d70d347d00)
- **Revenue Strategy**: [Increase Revenue](../../strategy/increase-revenue.md)
