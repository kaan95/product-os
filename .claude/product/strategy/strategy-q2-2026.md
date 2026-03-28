# Q2 2026 Product Strategy
**Legal Hero — Quarterly Strategy Review**

*Created: 2026-03-19*
*Author: Product Strategy (via Strategy Advisor)*

---

## 📊 Position

Q1 built the right foundations — KPI infrastructure, AI automation pilots, and platform consolidation — but it ends with two unresolved tensions heading into Q2. First, the revenue model depends on a lawyer-tier monetization bet (Premium Package) that has never been tested at price, and must go live in May. Second, complaint volume has not improved across Q1 (stable at ~75/month, 53% legitimate), while HUK — a critical RSV partner — is trending sharply upward (11 → 20 → 26 complaints/month) with no visible intervention. The biggest near-term risk is not a missing feature. It is that LH continues to discover partner quality failures only after RSV escalation, with no proactive detection system in place. If that posture persists through Q2, RSV trust erodes faster than Premium Package can generate revenue.

---

## 💡 Insights

- **Quality is the existential risk, not a feature gap** — 65% of all PA-attributed complaints are "Keine Rückmeldung" or "Kommunikation." LH currently discovers these failures only when RSV complains. Every month without the Case Intelligence System is another month of reactive posture. The Heiko Florschütz case (1.5+ years of undetected lawyer neglect) is not an edge case — it is a system failure that will recur.

- **HUK (11→20→26) is a leading indicator of RSV churn, not a lagging complaint stat** — HUK is now the #1 complaint source at 25% of Q1 volume, with one case already escalated to Vorstand level. The trend has no visible cause or intervention. If this continues into Q2 unchecked, it becomes an RSV relationship crisis. The root cause (portfolio growth vs. quality deterioration) must be determined now, not retrospectively.

- **The Premium Package monetization logic is sound, but the V1 value proposition hinges on one unvalidated assumption** — partner interviews confirm lawyers only care about financial outcome. CTL priority for Kündigungen is a financial lever (more high-value cases). But the Fastlane document processing SLA (1-day guarantee) is a Premium benefit that currently cannot be reliably delivered — document processing AI is still at "Medium" priority and not near target. Launching a guarantee you can't consistently meet will damage the pilot.

- **86% of complaints cannot be attributed to a specific Kanzlei** — you cannot perform partner-level quality management without this data. Without it, Cyfire/Limelaw is the only identifiable quality problem because it's the only firm with attribution. The real distribution of quality failures across the partner network is unknown.

- **The Q1 strategic checkpoint question must be answered now** — the strategy doc framed end-of-Q1 as a decision gate: "Are we ready to onboard new RSV partners?" Q2 Phase 2 goals (2-3 new RSV partners) depend on this. If KPI baselines were not established by Mar 15, or if complaint trend is not understood, starting RSV expansion in Q2 is premature.

---

## 🎯 Recommendations by Time Horizon

---

## Short-term (Q2 2026, April–June)

**Core Problem**
Launch the Premium Package revenue bet while simultaneously stopping the quality erosion that threatens the RSV relationships it depends on. These are not separate workstreams — they are interdependent. RSV trust is the precondition for onboarding new partners, and Premium Package success requires happy, engaged lawyers. A Q2 that delivers revenue at the cost of HUK churn is a net loss.

**Goals**
- Launch Premium Package V1 with 10 pilot agencies by May without triggering partner churn
- Detect and intervene on stalled cases before RSV escalates — move from reactive to proactive quality posture
- Stabilize HUK complaint volume or understand its root cause before it reaches RSV leadership threshold
- Scale Q1 AI foundations to production readiness: document processing <12 hours, finance automation at 85%+

**Key Initiatives**
- **Premium Package V1** (May target): CTL priority for Kündigungen, push notifications, AI token system (20-25 free/month), Agency plan management. *De-risk: consider starting Fastlane SLA at 2-day guarantee rather than 1-day until document processing AI hits target. Do not over-promise.*
- **Case Intelligence System**: Proactive stalled-case detection, automated alerts for cases with no lawyer activity in >7 days, risk scoring dashboard for operations team. This is the single highest-leverage quality intervention available.
- **HUK Root Cause Investigation**: Immediate data pull — is HUK complaint rate rising as a share of HUK case volume, or in absolute terms? If absolute: quality deterioration. If proportional: caseload growth. Develop an intervention plan with the HUK partner team before mid-Q2.
- **Kanzlei attribution fix**: Make Kanzlei a mandatory field in the complaint workflow. This is a small ops change with outsized strategic impact — it unlocks partner-level quality accountability across the entire network.
- **Scale Q1 AI**: Document processing to <12 hours for 70%+ of docs (reprioritize OS-2713 to Highest); Finance automation from ~70% → 85% AURE auto-invoicing; Lawyer AI to first measurable adoption signal.

**Key Metrics**
- 10 Premium pilot agencies onboarded with 0 churn from pilot group
- HUK complaint volume: trend breaks or root cause documented with intervention plan active
- 30%+ of active cases receive ≥1 update in last 7 days (from current baseline)
- Document processing average: <12 hours for top 3 document types
- Complaint Kanzlei attribution rate: >50% (from 14%)
- No new high-severity (Level 3) cases involving irrecoverable errors by partner lawyers

---

## Mid-term (Q3–Q4 2026)

**Core Problem**
Scale the Premium Package from pilot to full launch and begin RSV partner expansion — but only once quality posture is demonstrably improved. The strategy's Phase 2 gate ("Is platform quality consistent at 2-3x scale?") cannot be answered yes until the Case Intelligence System is live and complaint data is clean enough to detect partner-level issues.

**Goals**
- Trial-to-Premium conversion >30%; take rate reaches 48.72%; revenue path to €8.2M
- 2-3 new RSV partners successfully onboarded with documented quality SLAs
- Lawyer performance management live: bottom performers identified, top performers rewarded with case flow

**Key Initiatives**
- **Premium Package V2** (Q3): PLG free trial (2 months) for new agencies, auto-downgrade, upgrade CTAs at all touchpoints, plan comparison UI, self-service conversion. Success depends on V1 retention — do not rush if pilot churn is above zero.
- **RSV Onboarding Program**: Systematic onboarding playbook, RSV partner dashboards (key missing initiative from strategy), QBR process with NPS tracking. This is a prerequisite for Phase 2 RSV expansion.
- **Lawyer Performance Dashboards**: Visible performance scores per lawyer (resolution time, satisfaction, SLA compliance). Tie CTL distribution directly to quality score. This is the structural fix for PA responsiveness — not AI, not notifications, but accountability.
- **Terminsvertreter (TV) Quality Initiative**: TV briefing process redesign, mandatory pre-hearing documentation checklist, TV vetting upgrade. Scored 12 in Q1 opportunities. With irrevocable errors happening in Q1, this cannot wait until Q4. At minimum, a discovery sprint in Q3 should define the TV quality playbook.
- **Platform Orchestration** (begin scoping): Matching algorithm improvements, multi-stakeholder communication hub. No dedicated initiative currently exists for core orchestration — the strategy's highest-investment pillar (40% R&D) has no Q1-Q2 initiative. Q3 is the time to scope this properly.

**Key Metrics**
- Take rate: 48.72%
- Trial-to-Premium conversion: >30%
- RSV partner NPS: >80 across existing partners
- Lawyer performance dashboards live for 100% of active partners
- New RSV partners: 2-3 successfully onboarded
- Complaint rate (legitimate): <1% of cases (Q1 target not yet visible as met)

---

## Long-term (3+ years)

**Vision**
Legal Hero becomes the undisputed infrastructure layer for RSV legal case management in the German-speaking market — with defensible moats in network effects (more RSV + more lawyers = smarter platform), data depth (case outcome prediction, cost modeling), and process standardization (the quality standard RSVs require). The multi-sided platform model (RSV pays for orchestration, lawyers pay for efficiency, clients pay for premium experience) is the revenue architecture that enables category leadership.

**Goals**
- €13.2M ARR (take rate at 52%, Premium V3 fully live)
- 10+ RSV partners, 5,000+ active lawyers, 100K+ cases/year
- Platform recognized as category standard in German RSV legal tech

**Key Bets**
- **Lawyer-side SaaS**: Once 10+ RSV partners are committed, introduce lawyer-side practice management tools as a separate revenue stream. The platform reach (5,000+ lawyers) makes this a highly efficient distribution channel.
- **Data products**: Anonymized legal market benchmarks sold to RSV partners (case duration by Rechtsgebiet, win rates by legal area, cost benchmarks). The data moat only becomes a revenue moat if it is productized.
- **Geographic expansion** (Austria/Switzerland): Identical market structure (RSV + lawyers + clients), same regulatory family. Geographic expansion is a multiplier once the German platform model is proven.

**Indicators of Success**
- RSV customer retention >95% with documented NPS >80 — this is the health signal that platform quality is delivering at scale
- Lawyer Premium adoption >30% of active network — indicates value proposition is real, not just financial pressure
- Case Intelligence System preventing >50% of potential complaints before RSV escalation — the shift from reactive to proactive is what makes the platform structurally defensible

---

## ❓ Open Questions

- **Q1 checkpoint: are we actually ready for RSV expansion?** The strategy required all 12 outcome baselines by Mar 15. Are they in place? If not, beginning Phase 2 (RSV onboarding) in Q2 is building on unmeasured foundations. This needs a clear answer before Q2 planning is finalized.

- **Fastlane SLA feasibility for Premium V1**: The 1-day document processing guarantee is a core Premium differentiator. But document processing AI (OS-2713) is still Medium priority and not near target. Can Fastlane be operationally delivered in V1 without AI readiness — through a dedicated ops queue — or should it launch as a 2-day SLA with a 1-day upgrade path?

- **HUK trend: portfolio growth or quality failure?** This must be answered with data before mid-Q2. The intervention strategy is completely different depending on the answer. Escalating to Vorstand before LH has an answer is worse than the complaint volume itself.

- **TV quality: who owns it?** Terminsvertreter quality scored 12 in Q1 opportunities and produced 2 Level-3 complaints including an irrevocable settlement. There is no scoped initiative addressing this. Is this an operations problem (briefing process), a partner management problem (TV vetting), or a product problem (system-enforced briefing checklist)? It needs an owner in Q2.

- **Premium pilot partner selection**: Which 10 agencies are the V1 pilot candidates? They need to (a) have sufficient Kündigungen volume to benefit from CTL priority, (b) be friendly enough to absorb rollout friction, and (c) not be the same agencies generating quality complaints. Has this selection been made?

- **Platform Orchestration resourcing gap**: The strategy allocates 40% of R&D to Platform Orchestration. Q1 has no initiative for it. When does this work begin, and who owns it? Q2 is the right time to scope the matching algorithm and communication hub — waiting longer creates compounding technical debt.
