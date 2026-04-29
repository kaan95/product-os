# ScheduleSync — Q2 2026 Roadmap

*Fictional reference example. Use it for tone, calibration, and structure — not as a template to copy verbatim.*

*This quarter is about turning new signups into engaged teams. We're closing the loop between "tried it once" and "uses it weekly," and starting to charge the segments that already see value.*

---

## Quarter at a Glance

| Objective | KRs | Status |
|---|---|---|
| Make new teams successful in their first two weeks | 2 | Planned |
| Convert engaged free teams into paying customers | 2 | Planned |

Framing: **OKR** · Horizon: Q2 2026 (Apr 1 – Jun 30) · Generated 2026-04-29

---

## Objective 1: Make new teams successful in their first two weeks

> Most of our churn happens before the second meeting is ever scheduled. If a team hits "active" in week two, they retain at 4× the rate of teams that don't. The single biggest lever on revenue this year is the first 14 days.

### KR 1.1 — % of new teams that schedule 3+ meetings in the first 14 days rises from 22% → 45%

- **Baseline**: 22% (Q1 2026 cohort, 8-week trailing avg)
- **Target**: 45% by end of Q2
- **Why it matters**: 3 meetings in 14 days is the strongest leading indicator of 90-day retention we've found.

**Initiatives in service of KR 1.1**

| Initiative | Type | Owner | Notes |
|---|---|---|---|
| Guided first-meeting setup | Bet | Onboarding squad | Replace empty calendar with a 90-second guided flow; A/B against current state |
| Calendar import on day 1 | Bet | Integrations squad | Most teams stall because their existing meetings aren't visible — pull them in immediately |
| Re-engagement nudge at day 5 | Bet | Lifecycle squad | Email + in-app for teams that haven't scheduled a 2nd meeting |

### KR 1.2 — Time-to-first-scheduled-meeting drops from 4.1 days → under 2 days (median)

- **Baseline**: 4.1 days (Q1 2026 cohort)
- **Target**: < 2 days
- **Why it matters**: Faster first value = lower drop-off. Self-reported "I forgot about it" is the #1 churn reason in week 1.

**Initiatives in service of KR 1.2**

| Initiative | Type | Owner | Notes |
|---|---|---|---|
| One-click "schedule with my team" CTA | Bet | Onboarding squad | Surface immediately after signup; no calendar config required |
| Mobile signup flow rebuild | Committed | Mobile squad | 38% of signups are mobile; current flow is broken on Android. Was committed in Q1 carry-over. |

---

## Objective 2: Convert engaged free teams into paying customers

> We've grown free signups 3× year-over-year but free→paid conversion has been flat at 2.4%. Several engaged segments (10+ user teams, recurring meetings) are clearly getting value but never see a reason to upgrade.

### KR 2.1 — Free→paid conversion rises from 2.4% → 4.0% within 60 days of signup

- **Baseline**: 2.4% (Q1 2026)
- **Target**: 4.0%
- **Why it matters**: Hitting this rate at current signup volume = ~€340K incremental ARR.

**Initiatives in service of KR 2.1**

| Initiative | Type | Owner | Notes |
|---|---|---|---|
| Usage-based upgrade prompts | Bet | Monetization squad | Trigger when a team hits a paid-tier feature (analytics view, 4th integration, 11th seat) |
| Annual-plan checkout option | Bet | Monetization squad | 70% of paid customers said they would have taken annual at signup if offered |

### KR 2.2 — Paid-tier feature engagement (among paid teams) rises from 31% → 55% MAU

- **Baseline**: 31% MAU on paid features
- **Target**: 55%
- **Why it matters**: Paid teams who use ≥1 paid feature retain at 92% annually; those who don't, at 47%. Activation of paid features *after* upgrade is the next-biggest churn lever.

**Initiatives in service of KR 2.2**

| Initiative | Type | Owner | Notes |
|---|---|---|---|
| Admin dashboard v2 | Bet | Platform squad | The current dashboard is the most-requested paid feature but the most-abandoned post-upgrade |

---

## Committed Work (non-KR)

These are happening regardless of the KRs above. They're obligations, foundations, or risk reduction — not bets.

| Initiative | Rationale | Owner |
|---|---|---|
| GDPR data-export endpoint | Regulatory deadline 2026-05-31 | Platform squad |
| Migrate auth service off legacy library | Security advisory, EOL 2026-06 | Platform squad |
| Enterprise SSO for ACME contract | Contracted go-live 2026-06-15 | Integrations squad |

---

## What we're NOT doing this quarter

- **AI meeting summaries** — interesting, but no evidence it moves activation or conversion. Revisit Q3 once paid retention is stabilized.
- **Slack-native scheduling experience** — large surface area, low confidence on impact. Defer until we see whether usage-based prompts (KR 2.1) saturate.
- **Internationalization beyond EN/DE** — the conversion problem is concentrated in our existing markets; expansion is a Q4 question.
- **Redesigning the marketing site** — out of squad scope; flagged to growth team separately.

---

## Open Questions / Risks

- KR 1.1 baseline of 22% is from an 8-week window. We don't yet know how much of the recent dip is seasonal vs. structural — first-week action: pull a 2024 same-quarter baseline.
- Mobile signup rebuild (KR 1.2) depends on a new SDK from the platform squad; if that slips past 2026-05-15, KR 1.2 is at risk.
- Annual-plan checkout (KR 2.1) requires finance sign-off on revenue-recognition treatment — open with finance as of 2026-04-22.
- We're assuming admin-dashboard friction is the main blocker to paid-feature adoption (KR 2.2). If post-launch data doesn't move, we'll need to investigate other causes before adding more dashboard work.

---

## Sources

- Outcomes file: *(none yet — outcomes drafted inline this quarter; should be promoted to `product-outcomes` next cycle)*
- Strategy: *fictional Q1 2026 strategy memo, "Activation before expansion"*
- Generated: 2026-04-29 · Framing: OKR · Horizon: Q2 2026
