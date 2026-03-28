# Solution Brainstorm: Lawyers Forget / Neglect Cases

**Date**: 2026-03-10
**Opportunities Addressed**: 1
**Solutions Generated**: 3
**Constraints**: None specified
**Note on Overlap**: The prior brainstorm (`complaint-reduction-brainstorm-2026-03-06.md`) covered this space from an **internal/operations lens** — detecting stalled cases in a PM queue, running portfolio health rituals, and building RSV transparency dashboards. Those solutions are NOT repeated here. This brainstorm focuses exclusively on **lawyer-facing product experiences** that prevent neglect from the inside out.

---

## Overview

| Opportunity | Score | Solution A | Angle A | Solution B | Angle B | Solution C | Angle C |
|------------|-------|-----------|---------|-----------|---------|-----------|---------|
| Lawyers forget / neglect cases | 27 | Friction-Free Next Action Design | Design / UX | Personal Inactivity Digest | Data / Transparency | Social Accountability Layer | Incentive / People |

---

## Opportunity: Lawyers Forget / Neglect Cases

**Opportunity Statement**: Lawyers managing high caseloads lose track of cases that require action — especially older, less urgent ones — leaving clients waiting for weeks or months without any update. There is currently no mechanism within the lawyer-facing product experience that reliably surfaces these forgotten cases and prompts the right action.

**Type**: Problem
**Sizing**: Pain: High | Reach: Broad | Frequency: Constant | **Score: 27**
**Source**: complaint-insights-march-2026.md (Opportunity #10: Proactive Case Oversight), complaint-insights-jan-feb-2026.md (PA - Keine Rückmeldung: 24 cases), interview-cyfire-lh-product-2026-03-03.md (Parent Opportunity 1: No automated alerts for overdue responses, Score: 18)

**Evidence**:
- "Keine Rückmeldung" (no response) is the #1 complaint reason every month — 24 cases in Jan-Feb, 5+ in March 2026
- Proactive case oversight identified as a new critical opportunity in March: "currently relies on RSV complaints to discover neglect"
- Lawyers explicitly mentioned no alerting system for overdue responses in the Cyfire interview
- One PA managed a case for 1.5+ years without LH oversight (Jan-Feb complaints)
- Root structural cause: low RSV compensation makes extensive communication economically unviable — nudges must have near-zero cognitive load to overcome this

---

### Solution A: Friction-Free Next Action Design

**Angle**: Design / UX

**Core Idea**
Redesign the lawyer's default CaseForce landing view so that the first thing they see when they log in is not a generic case list, but an **"Action Required" queue** — pre-sorted by urgency (days since last activity), with a pre-drafted suggested action for each case. For a case with 10 days of inactivity, the system pre-fills a message template ("I wanted to give you a quick update on your case — we are currently...") that the lawyer can send in one click. The path of least resistance becomes taking action, not ignoring the case.

**How It Addresses the Opportunity**
The cognitive bottleneck isn't malice — it's overwhelm. A lawyer with 80 cases can't mentally prioritize them all. By collapsing the decision down to "here are your 3 most at-risk cases, and here's what to do about each," the nudge works with the lawyer's attention rather than against it. The pre-drafted message removes the effort barrier: "I need to write something" becomes "I need to press send."

**Target Stakeholder**: Lawyers (primary)

**Key Assumptions**
1. We believe that the main reason lawyers don't follow up is decision overhead, not unwillingness. We'll know this is true when lawyers who receive a pre-drafted message template take action within 24h at a significantly higher rate than those who just receive a notification.
2. We believe that lawyers will use the pre-drafted message template rather than ignoring it or always rewriting it from scratch. We'll know this is true when >50% of prompted messages are sent using the template with minimal edits.
3. We believe that surfacing cases sorted by inactivity (rather than the current sort order) won't cause lawyers to feel that earlier cases are deprioritized. We'll know this is true when lawyers say the new sort feels intuitive and helpful in user testing.

**Cheapest Test**
- **Method**: Wizard of Oz + A/B test
- **Description**: For 2 weeks, an ops team member manually identifies each lawyer's most-overdue case each morning and sends them a Slack/WhatsApp message: "Good morning! [Client Name]'s case hasn't had any activity in [X] days — here's a message you can send: [template text]. Want me to send it for you, or will you handle it?" Track action rate vs. control group (lawyers who don't receive the nudge).
- **Duration**: 2 weeks
- **Success signal**: Lawyers in the nudge group take action on the flagged case within 24h at a rate >2x the control group; >40% use or adapt the pre-drafted message
- **Failure signal**: Lawyers ignore the nudge, say it's annoying, or say they already knew about the case and had a reason for the delay

**Effort Estimate**: M (redesigned case list view, inactivity sorting engine, message template system with pre-fill)
**Strategic Fit**: Strong — directly enables Pillar 1 (Platform Orchestration, Case Workflow) and Pillar 3 (Process Standardization, SLA enforcement at the UX layer)

**Risks**
- Pre-drafted messages feel too generic and damage the lawyer-client relationship if sent as-is. *Mitigation*: Always show a preview and require one-click confirmation before sending; make it clear it's a template, not auto-send.
- Lawyers tune out the "Action Required" queue if it's always full and they can never clear it. *Mitigation*: Cap the queue at 5-7 cases maximum; prioritize ruthlessly by risk, not just inactivity.

---

### Solution B: Personal Inactivity Digest

**Angle**: Data / Transparency (Self-directed)

**Core Idea**
Send each lawyer a **personalized weekly digest email** (Monday morning) showing their own case activity statistics: how many cases have had no lawyer activity for 3, 7, and 14+ days, with direct links to each. Include a comparison to their own previous week ("You had 4 overdue cases last week — this week you have 7") and optionally a network percentile ("You're in the top 30% of lawyers for response times"). The digest is purely informational — no actions are forced, no management is involved. It's a personal mirror.

**How It Addresses the Opportunity**
Most lawyers don't neglect cases consciously — they lose track. This solution creates a regular moment of structured self-reflection that gives the lawyer a clear, ranked picture of where their attention is most needed. The comparison to their own past performance activates self-improvement instincts without feeling like surveillance. The network percentile (if used carefully) adds social motivation: "I want to stay in the top third."

**Target Stakeholder**: Lawyers (primary — receives and acts on the digest)

**Key Assumptions**
1. We believe that lawyers open and act on weekly digest emails (not just ignore them). We'll know this is true when email open rate exceeds 50% and click-through to the linked cases exceeds 25%.
2. We believe that seeing their own inactivity data motivates action, rather than causing lawyers to feel criticized and disengage. We'll know this is true when case activity rates increase in the week following each digest send.
3. We believe that the data to generate personalized inactivity stats per lawyer already exists in CaseForce in a form that can be queried reliably. We'll know this is true when a prototype digest can be generated for 10 lawyers using existing data.

**Cheapest Test**
- **Method**: Manual email pilot
- **Description**: Manually generate a 1-page case inactivity report for 5-10 lawyers using existing CaseForce data (pull cases per lawyer, last activity date). Send it by email Monday morning for 3 weeks. Interview the lawyers after week 1: Did they read it? Did they act? Was it useful or stressful? Track whether those lawyers' case activity rates change in the days following each email.
- **Duration**: 3 weeks (3 emails) + 1 week debrief
- **Success signal**: >60% open rate; lawyers report it as useful; measurable increase in case activity rate in the 2 days after each digest
- **Failure signal**: Lawyers ignore it, find it demotivating ("I have too many cases, this just makes me feel bad"), or the data reveals too many edge cases (e.g., cases where inactivity is valid — case closed, waiting for court date)

**Effort Estimate**: S-M (data query layer, email templating engine, edge case handling for valid inactivity reasons)
**Strategic Fit**: Strong — enables Pillar 4 (Data-Driven Infrastructure: making case performance visible to the primary stakeholder) and supports the strategy's "measurable, comparable, optimizable" legal services vision

**Risks**
- Lawyers perceive the digest as monitoring and push back politically, especially in a freelance/partner context where autonomy is valued. *Mitigation*: Frame as a personal tool ("your weekly case health check") not a management report; make it opt-in initially.
- Edge cases pollute the data: cases where inactivity is intentional (waiting for a document, case in court queue, client hasn't responded). *Mitigation*: Allow lawyers to snooze/mark cases as "waiting on external input" to exclude them from the digest.
- Email is the wrong channel — lawyers may prefer in-app. *Mitigation*: Start with email (cheapest to test), migrate to in-app notification once adoption is proven.

---

### Solution C: Social Accountability Layer

**Angle**: Incentive / People (Social)

**Core Idea**
Create a lightweight **peer visibility layer** within CaseForce where lawyers can opt in to see a simple team leaderboard: average response time, cases handled this week, and cases currently overdue — compared to peers in their same practice area. Critically, this is **opt-in and anonymized for bad metrics**: lawyers see their own scores prominently but peers are shown as "Lawyer A", "Lawyer B" — except for top performers, who are named. The goal is to leverage social comparison (upward social comparison for high performers, mild accountability for laggards) without creating a shaming culture.

**How It Addresses the Opportunity**
The economic incentive to be responsive is weak for many lawyers (low RSV compensation). But social incentives — particularly around professional reputation among peers — can be a powerful motivator. Seeing that "Lawyer A" has zero overdue cases while you have 12 creates a kind of professional discomfort that prompts action. It also surfaces role models: lawyers who see a peer maintaining a clean slate at high volume may adopt their habits or ask for tips.

**Target Stakeholder**: Lawyers (primary — see their own performance in context of peers)

**Key Assumptions**
1. We believe that lawyers care about their standing relative to peers in their practice area, and this social comparison motivates behavior. We'll know this is true when lawyers who can see peer rankings have lower case inactivity rates than those who can't.
2. We believe that the opt-in/anonymized design will result in meaningful adoption (>40% opt-in rate), not just avoidance. We'll know this is true when opt-in rate exceeds 40% within 30 days of launch.
3. We believe that social accountability works for case neglect specifically, not just for faster responses (i.e., it changes the inactivity behavior, not just the messaging speed). We'll know this is true when overdue case counts drop, not just first-contact time.

**Cheapest Test**
- **Method**: Interview + survey
- **Description**: Interview 8-10 lawyers with a simple scenario: "We're considering showing you how your case response times compare to other lawyers in your practice area. Here's a mock-up [show screenshot]. Would you find this useful? Would it affect your behavior? Would you opt in?" Also ask: "What would make you feel competitive vs. surveilled?" Use insights to decide whether the social angle resonates before building anything.
- **Duration**: 1 week (interviews only)
- **Success signal**: >60% say they'd opt in; >50% say it would motivate them to keep their overdue count low; lawyers suggest specific features (e.g., "I'd want to see my trend over time")
- **Failure signal**: Strong rejection — lawyers say it feels like surveillance, creates unnecessary competition, or they'd opt out immediately; or strong indifference ("I don't care what other lawyers do")

**Effort Estimate**: M (leaderboard data layer, opt-in management, anonymization logic, in-app UI component)
**Strategic Fit**: Moderate — supports Pillar 3 (Quality Measurement) and Pillar 4 (Data Infrastructure), but less directly than the other solutions; highest value as a retention and engagement feature for high performers

**Risks**
- Creates a toxic competitive culture, especially between full-time and part-time lawyers who have very different caseloads. *Mitigation*: Normalize by caseload size, not raw numbers; only compare within same practice area and case volume tier.
- Low opt-in rate makes the leaderboard meaningless (comparisons not relevant with few participants). *Mitigation*: Consider showing data aggregated at the practice-area level so even a 20% opt-in generates meaningful benchmarks.
- The design requirement for anonymization is complex and could fail (lawyers deduce identities from context). *Mitigation*: Keep peer data at very high aggregation level initially; only name top performers with explicit consent.

---

### Comparison: Lawyers Forget / Neglect Cases

| Dimension | Solution A: Friction-Free Next Action | Solution B: Personal Inactivity Digest | Solution C: Social Accountability |
|-----------|--------------------------------------|---------------------------------------|----------------------------------|
| **Angle** | Design / UX | Data / Transparency | Incentive / People |
| **Speed to test** | Fast (2 weeks wizard of oz) | Fast (3-4 weeks manual email) | Fast (1 week interviews) |
| **Upside if it works** | High — directly removes the effort barrier to action | Medium-High — creates habit of self-monitoring | Medium — motivates high performers, uncertain for laggards |
| **Downside risk** | Low — worst case lawyers ignore the queue | Low — worst case lawyers opt out of email | Medium — cultural risk if framed badly |
| **Effort (full build)** | M | S-M | M |
| **Strategic alignment** | Strong (Pillar 1 + 3) | Strong (Pillar 4) | Moderate (Pillar 3 + 4) |

**Trade-offs**: Solution A is the most direct product intervention — it removes friction from the action itself and works even for lawyers who wouldn't engage with a digest or leaderboard. But it requires the most UX design investment. Solution B is the lowest-effort build with high testability — a manual email can validate the concept within weeks. Solution C has the highest ceiling (peer motivation is powerful) but also the highest risk of misfire, and requires a cultural read of the lawyer community first. The three solutions are also **complementary**: A (in-product nudge) + B (out-of-product reflection moment) + C (social motivation) cover the full loop of prevention, awareness, and accountability.

**Recommended first test**: Run Solution C's interview this week (pure research, no engineering). Simultaneously start Solution B's manual email pilot. Both are near-zero cost and the findings directly inform whether A's product investment is worth making. If interviews show lawyers care about peer standing → prioritize C alongside A. If lawyers prefer private self-awareness → double down on B and A. If both fall flat → revisit the root cause hypothesis (maybe it's a workload/tooling issue, not a motivation issue).

---

## Relationship to Prior Brainstorm

The `complaint-reduction-brainstorm-2026-03-06.md` addressed this opportunity from an **internal ops lens**:
- **Stalled Case Detection Engine** (Technology) — LH ops detects stalled cases and pushes the lawyer
- **Portfolio Health Ritual** (Process) — PMs manually review case portfolios weekly
- **RSV Early Warning Dashboard** (Data/Partnership) — RSV partners see at-risk cases proactively

This brainstorm adds the **lawyer-facing complement**:
- Solution A (Friction-Free Next Action) combines with the Detection Engine — the engine identifies the case, the UX makes the action effortless
- Solution B (Personal Digest) is the outbound version of the PM Health Ritual — rather than ops watching the lawyer, the lawyer watches themselves
- Solution C (Social Accountability) adds a motivation layer that neither the detection engine nor the health ritual provides

For full picture: run Solution A + Detection Engine together. Detection Engine = surface the signal; Friction-Free Next Action = remove the barrier to acting on it.

---

## Next Steps

### Recommended Assumption Tests (Priority Order)

| # | Solution | Assumption to Test | Test Method | Duration |
|---|----------|--------------------|-------------|----------|
| 1 | Social Accountability | Do lawyers respond positively to peer comparison as a motivator? | 8-10 lawyer interviews with mock-up | 1 week |
| 2 | Personal Inactivity Digest | Do lawyers act on a weekly inactivity report? | Manual email pilot (5-10 lawyers, 3 sends) | 3-4 weeks |
| 3 | Friction-Free Next Action | Does a nudge + pre-drafted message produce 2x action rate vs. control? | Manual Wizard of Oz (ops sends nudge daily) | 2 weeks |

**Note**: Tests 1 and 2 can start in parallel this week. Test 3 should start after Test 1's interviews, as their findings inform the tone and design of the nudge.

---

## References

- **Opportunity Sources**:
  - `.claude/product/discovery/opportunities/complaints/complaint-insights-march-2026.md` (Opportunity #10)
  - `.claude/product/discovery/opportunities/complaints/complaint-insights-jan-feb-2026.md` (PA - Keine Rückmeldung)
  - `.claude/product/discovery/opportunities/interview-cyfire-lh-product-2026-03-03.md` (Parent Opportunity 1, child: no automated alerts)
- **Existing Solution Files**: `complaint-reduction-brainstorm-2026-03-06.md` — see overlap notes above
- **Product Strategy**: `.claude/product/strategy/product-strategy-2026.md`
- **Related Jira**: CF-4006 (Nudge Lawyers to Take Action on Inactive Cases via To-Do List & Case List)
