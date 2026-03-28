# Solution Brainstorm: Reducing External Complaints

**Date**: 2026-03-06
**Opportunities Addressed**: 3
**Solutions Generated**: 9
**Constraints**: None specified

---

## Overview

| Opportunity | Score | Solution A | Angle A | Solution B | Angle B | Solution C | Angle C |
|------------|-------|-----------|---------|-----------|---------|-----------|---------|
| Partner Lawyer Responsiveness | 27 | Case Pulse Automation | Technology | Lawyer Scorecard & Tiered Matching | Incentive/Data | Client Self-Service Case Tracker | Design |
| Proactive Case Oversight | 27 | Stalled Case Detection Engine | Technology | Portfolio Health Ritual | Process | RSV Early Warning Dashboard | Data/Partnership |
| Terminsvertreter Quality | 12 | Structured TV Briefing Protocol | Process | TV Performance Gate | Incentive | AI-Assisted TV Prep Package | Technology |

---

## Opportunity 1: Partner Lawyer Responsiveness & Communication

**Opportunity Statement**: Clients lose trust and seek alternative lawyers when partner lawyers are unresponsive for days or weeks. This is the #1 complaint driver across all months in 2026.
**Type**: Problem
**Sizing**: Pain: High | Reach: Broad | Frequency: Constant | **Score: 27**
**Source**: complaint-insights-march-2026.md (Opportunity #1), complaint-insights-jan-feb-2026.md (Opportunity Area #1)

**Evidence recap**: PA - Keine Ruckmeldung (5 in March, 24 in Jan-Feb) and PA - Kommunikation (5 in March, 15 in Jan-Feb) are the top two complaint reasons every single month. Clients describe waiting weeks with no update, calling repeatedly and getting no answer, and ultimately requesting a different lawyer or going to an RA vor Ort.

---

### Solution A: Case Pulse Automation

**Angle**: Technology / Automation

**Core Idea**
Build an automated "pulse check" system that monitors case activity and triggers escalating interventions when a lawyer hasn't communicated with a client within defined timeframes. After 3 days of no activity post-mandate, the system sends a gentle reminder to the lawyer. After 5 days, it alerts the portfolio manager. After 7 days, it auto-sends a status message to the client (e.g., "Your lawyer is reviewing your case — you'll hear from them within 48 hours") and escalates internally.

**How It Addresses the Opportunity**
The core mechanism is breaking the silence gap. Most complaint escalations happen because clients hear nothing for 2-4 weeks. By inserting automated touchpoints, the client feels informed even when the lawyer is busy. Simultaneously, internal escalation catches the cases before they become complaints. The system turns "no news" from an anxiety trigger into a monitored state.

**Target Stakeholder**: Lawyers (receive reminders), Portfolio Managers (receive escalations), Clients (receive status updates)

**Key Assumptions**
1. We believe that most PA responsiveness complaints could be prevented by a single proactive status message within the first 7 days. We'll know this is true when we see complaint rates drop for cases where an auto-message was sent vs. control group.
2. We believe that lawyers will respond to automated reminders before reaching the escalation threshold. We'll know this is true when >60% of reminders result in lawyer action within 24 hours.
3. We believe that generic status messages ("your case is being reviewed") reduce client anxiety even without case-specific content. We'll know this is true when clients who receive these messages rate satisfaction higher than those who don't.

**Cheapest Test**
- **Method**: Concierge test (manual version of automation)
- **Description**: For 2 weeks, have one operations team member manually check all cases assigned in the last 7 days for any with no lawyer activity. For those cases, manually send a templated status email to the client and flag the lawyer. Track whether these cases generate fewer RSV complaints than the control group (cases from the prior 2 weeks with no intervention).
- **Duration**: 2 weeks
- **Success signal**: Complaint rate for intervened cases drops by >40% compared to control period
- **Failure signal**: Clients respond negatively to generic messages ("this tells me nothing") or lawyers feel micromanaged and push back

**Effort Estimate**: M (full automation with CaseForce integration, SLA engine, templated messages)
**Strategic Fit**: Strong — directly enables Pillar 3 (SLA Enforcement) and Pillar 1 (Case Workflow Orchestration)

**Risks**
- Lawyers perceive automated reminders as nagging or surveillance, damaging the LH-lawyer relationship. *Mitigation*: Frame as "client experience support" not monitoring; let lawyers customize their reminder preferences.
- Generic auto-messages set false expectations if the lawyer still doesn't act. *Mitigation*: Internal escalation must be coupled with the client-facing message — don't just message the client, also push the lawyer.

---

### Solution B: Lawyer Scorecard & Tiered Matching

**Angle**: Incentive / Data

**Core Idea**
Create a transparent lawyer performance scorecard that tracks responsiveness metrics (time to first contact, average response time, complaint rate) and directly ties performance to case allocation. High-performing lawyers get more cases and first pick of desirable case types. Low performers get fewer cases, then a warning, then offboarding. Make the scorecard visible to the lawyer so they know exactly where they stand.

**How It Addresses the Opportunity**
This shifts the incentive structure. Currently, there's no consequence for being slow to respond — lawyers get the same case flow regardless of performance. By making responsiveness a first-class metric that affects their livelihood (case volume = revenue), lawyers are incentivized to prioritize communication. The visibility component means lawyers self-correct before LH needs to intervene.

**Target Stakeholder**: Lawyers (see their scorecard, feel incentive effects), Portfolio Managers (use scores for allocation decisions)

**Key Assumptions**
1. We believe that lawyers will change behavior when they can see their responsiveness score relative to peers. We'll know this is true when average first-contact time improves within 30 days of scorecard launch.
2. We believe that tying case allocation to performance will not cause a lawyer supply crisis (i.e., enough lawyers perform well enough to handle volume). We'll know this is true when the top 70% of lawyers by score can absorb the volume currently handled by 100%.
3. We believe that the data to calculate responsiveness scores already exists in CaseForce (last activity timestamps, message logs). We'll know this is true when we can generate a prototype scorecard from existing data for 50+ lawyers.

**Cheapest Test**
- **Method**: Data analysis + interview
- **Description**: (1) Pull existing CaseForce data and calculate a "responsiveness score" for all active lawyers — see if there's meaningful differentiation (is it a few bad apples or a systemic issue?). (2) Share the prototype scorecard with 5 lawyers in an interview and gauge reaction: do they find it fair? Would it change their behavior?
- **Duration**: 3-5 days
- **Success signal**: Clear differentiation in scores (some lawyers consistently fast, others consistently slow); lawyers say "yes, this would motivate me to respond faster"
- **Failure signal**: Data is too noisy to produce meaningful scores; lawyers react with hostility or say it wouldn't change anything

**Effort Estimate**: L (requires data pipeline, UI, integration with matching algorithm, change management)
**Strategic Fit**: Strong — directly enables Pillar 3 (Performance Measurement) and Pillar 4 (Data-Driven Infrastructure). Aligns with strategy's "tiered lawyer system" and "offboarding of low performers."

**Risks**
- Lawyers game the metric (quick low-quality responses to appear responsive). *Mitigation*: Combine responsiveness with quality metrics (client satisfaction, case outcome).
- Creates adversarial relationship with lawyer network, especially during rollout. *Mitigation*: Grandfather existing lawyers with a grace period; position as "helping you see how you compare" not "punishing you."
- Low-performing lawyers leave the network, creating capacity gaps. *Mitigation*: Gradual rollout; only enforce allocation changes after sufficient data.

---

### Solution C: Client Self-Service Case Tracker

**Angle**: Design / UX

**Core Idea**
Build a simple client-facing portal (or even a status page linked from SMS/email) where clients can see their case status at any time: current stage, last activity, next expected milestone, and a way to send a message to their lawyer. The key insight: many "responsiveness" complaints are actually "transparency" complaints — the lawyer may be working on the case, but the client has no way to know.

**How It Addresses the Opportunity**
This decouples "feeling informed" from "lawyer actively communicating." A client who can log in and see "Stage: Coverage confirmed. Lawyer is preparing your claim letter. Expected: this week." feels much less anxious than one staring at a silent inbox. It also gives clients an alternative to calling the RSV to complain — they can message the lawyer directly through the portal, which is lower friction for everyone.

**Target Stakeholder**: Clients (primary user), Lawyers (case status must be kept current)

**Key Assumptions**
1. We believe that a significant portion of "no response" complaints are actually "no visibility" complaints — clients want to know what's happening, not necessarily to talk to the lawyer. We'll know this is true when clients who have portal access file fewer RSV complaints even if lawyer response times don't change.
2. We believe that case status data in CaseForce is granular enough to generate meaningful client-facing status updates. We'll know this is true when we can map 80%+ of active cases to a clear, client-understandable stage.
3. We believe that clients will actually use a self-service portal. We'll know this is true when >30% of clients check their status at least once in the first week.

**Cheapest Test**
- **Method**: Fake door + concierge
- **Description**: Send 50 clients a link to a "case status page" (a simple static page showing their current case stage, last update date, and a message box). The status is manually populated by an ops team member from CaseForce data. Measure: (a) how many clients click the link, (b) how many use the message feature, (c) do these 50 clients generate fewer complaints over the next 30 days?
- **Duration**: 2-3 weeks
- **Success signal**: >40% click rate, positive client feedback, measurable complaint reduction
- **Failure signal**: Clients don't click, or click but say the information is too vague to be useful

**Effort Estimate**: L (full portal with real-time data, authentication, messaging)
**Strategic Fit**: Strong — directly supports Pillar 1 (Multi-Stakeholder Communication) and Phase 3 vision (Client Portal). Listed as a Phase 3 initiative in strategy doc.

**Risks**
- Showing a stale or inaccurate status is worse than showing nothing — it confirms neglect rather than hiding it. *Mitigation*: Only show status for cases where data is reliably current; show "last updated" timestamp so clients can judge freshness.
- Lawyers resist keeping status current (adds work). *Mitigation*: Auto-derive status from CaseForce workflow stages rather than requiring manual lawyer input.
- Pulls forward a Phase 3 initiative to Phase 1 — may distract from foundation work. *Mitigation*: Start with a minimal version (static page, no auth) to validate before investing in full portal.

---

### Comparison: Partner Lawyer Responsiveness

| Dimension | Solution A: Case Pulse | Solution B: Scorecard & Tiering | Solution C: Client Tracker |
|-----------|----------------------|-------------------------------|--------------------------|
| **Angle** | Technology | Incentive / Data | Design / UX |
| **Speed to test** | Fast (2 weeks manual) | Fast (3-5 days data + interviews) | Medium (2-3 weeks) |
| **Upside if it works** | High — directly prevents complaints | High — systemic behavior change | Medium — reduces perceived pain but doesn't fix root cause |
| **Downside risk** | Low — easy to stop | Medium — lawyer relationship risk | Low — worst case clients ignore it |
| **Effort (full build)** | M | L | L |
| **Strategic alignment** | Strong (Pillar 3) | Strong (Pillar 3 + 4) | Strong (Pillar 1, Phase 3) |

**Trade-offs**: Solution A is the fastest to show results — it directly intervenes in the complaint-generating gap. Solution B is the most structurally impactful — it changes incentives so the problem self-corrects over time, but it's harder to implement and risks lawyer pushback. Solution C addresses the symptom (client anxiety) more than the cause (lawyer inaction), but it's a strategic asset that serves multiple purposes beyond complaints.

**Recommended first test**: Solution B's data analysis (3-5 days) — pull lawyer responsiveness data from CaseForce to understand if the problem is concentrated in a few lawyers or systemic. This insight directly informs whether A or B is the right structural approach. If it's a few bad actors, B (scorecard + offboarding) is the answer. If it's systemic, A (automation) is needed because you can't offboard everyone.

---

## Opportunity 2: Proactive Case Oversight

**Opportunity Statement**: Legalhero has no proactive system to detect stalled or neglected cases before the RSV escalates a complaint. By the time a complaint arrives, client trust is already damaged.
**Type**: Need
**Sizing**: Pain: High | Reach: Broad | Frequency: Constant | **Score: 27**
**Source**: complaint-insights-march-2026.md (Opportunity #10)

**Evidence recap**: 2 explicit "PO - Kontrolle" cases in March. But this is the *root enabler* — most PA responsiveness complaints could have been caught earlier if LH had visibility into case activity. In Jan-Feb, an offboarded lawyer managed a case for 1.5+ years without LH oversight.

---

### Solution A: Stalled Case Detection Engine

**Angle**: Technology / Automation

**Core Idea**
Build an automated monitoring system that flags cases meeting "stalled" criteria: no lawyer activity in X days, no client contact in Y days, missed SLA milestones, or a combination of signals. Flagged cases appear in a daily "attention needed" queue for Portfolio Managers, sorted by urgency. The system learns from historical patterns — cases that eventually generated complaints are used to calibrate the detection thresholds.

**How It Addresses the Opportunity**
This shifts LH from reactive (wait for RSV complaint) to proactive (detect before complaint). The causal mechanism: if a Portfolio Manager sees a case flagged as "no activity for 7 days" and intervenes (pings the lawyer, contacts the client), the complaint never materializes. Over time, the system also surfaces systemic patterns (e.g., "Kanzlei X has 12 stalled cases — structural problem").

**Target Stakeholder**: Portfolio Managers (primary), Lawyers (receive nudges), Operations leadership (see systemic patterns)

**Key Assumptions**
1. We believe that stalled cases can be reliably detected from CaseForce activity data (message timestamps, document uploads, status changes). We'll know this is true when a prototype detection rule correctly identifies 80%+ of cases that generated complaints in Jan-Feb.
2. We believe that Portfolio Managers will act on flagged cases within 24 hours if the queue is clear and actionable. We'll know this is true when intervention rate exceeds 80% within 24h during pilot.
3. We believe that early intervention (before client escalates) actually prevents the complaint rather than just delaying it. We'll know this is true when intervened cases show <5% subsequent complaint rate.

**Cheapest Test**
- **Method**: Retrospective data analysis
- **Description**: Take all 188 complaints from Jan-Mar 2026. For each, look at the case timeline in CaseForce: when was the last lawyer activity before the complaint was filed? Could a simple rule ("no activity for 7 days") have caught 80%+ of them? What's the false positive rate (cases with 7+ days of inactivity that did NOT generate complaints)?
- **Duration**: 2-3 days
- **Success signal**: A simple rule catches >70% of complaint cases with a manageable false positive rate (<3:1 false positive to true positive ratio)
- **Failure signal**: No clear pattern — stalled cases look identical to normally progressing cases in the data

**Effort Estimate**: M (data pipeline, alerting system, PM queue UI)
**Strategic Fit**: Strong — core enabler for Pillar 3 (Quality Assurance) and Pillar 4 (Data-Driven Infrastructure, automated quality detection)

**Risks**
- Alert fatigue: too many false positives and PMs start ignoring the queue. *Mitigation*: Start with very conservative thresholds (only flag 10+ day gaps); tune over time.
- CaseForce data may not capture all lawyer-client interactions (e.g., phone calls not logged). *Mitigation*: Accept imperfect data; even catching 60% of stalled cases is a massive improvement over 0%.

---

### Solution B: Portfolio Health Ritual

**Angle**: Process / People

**Core Idea**
Implement a structured weekly "Portfolio Health Review" ritual where each Portfolio Manager reviews their active cases against a simple checklist: (1) Any case with no activity in 7+ days? (2) Any case past an SLA milestone? (3) Any case where the client has reached out but the lawyer hasn't responded? This is a low-tech, high-discipline approach that works before any automation is built. Give PMs a shared Google Sheet or simple Notion view as their review tool.

**How It Addresses the Opportunity**
The current gap isn't just technological — it's also that no one's job is to proactively look for stalled cases. This solution makes it someone's explicit weekly responsibility. The checklist creates a forcing function for oversight. It also generates data on how many cases are stalled (which informs whether Solution A is worth building).

**Target Stakeholder**: Portfolio Managers (primary)

**Key Assumptions**
1. We believe that a 30-minute weekly review per PM is sufficient to catch the highest-risk cases. We'll know this is true when PMs can complete the review for their portfolio within the time allocation.
2. We believe that PMs can effectively intervene when they identify a stalled case (i.e., they have the authority and channels to push a lawyer or reassign). We'll know this is true when >70% of identified stalled cases are resolved within 48 hours of PM intervention.
3. We believe that the information needed for the review is accessible today (even if manually). We'll know this is true when PMs can answer the 3 checklist questions for their portfolio using existing tools.

**Cheapest Test**
- **Method**: Pilot process
- **Description**: Run the weekly Portfolio Health Review with 1 PM for 2 weeks. Give them a simple spreadsheet listing their active cases with "days since last activity" column (manually pulled from CaseForce). Track: how many stalled cases found, how many intervened on, how many complaint-prevented, time spent.
- **Duration**: 2 weeks
- **Success signal**: PM finds 5+ stalled cases per week that would have become complaints; intervention resolves most within 48h
- **Failure signal**: PM finds nothing (data already well-monitored) or can't effectively intervene (no authority, no escalation path)

**Effort Estimate**: S (process design, checklist template, 30 min/week per PM)
**Strategic Fit**: Moderate — establishes the habit and surfaces the need for Pillar 3 (SLA enforcement) but doesn't scale without automation

**Risks**
- PMs don't sustain the habit after initial enthusiasm. *Mitigation*: Make it a standing meeting with a manager; track completion.
- Manual review misses cases because the data is hard to access. *Mitigation*: Treat this as a stepping stone to Solution A; document exactly what data is needed to make the review easier.

---

### Solution C: RSV Early Warning Dashboard

**Angle**: Data / Partnership

**Core Idea**
Build a lightweight dashboard for RSV partners that shows the real-time health of their case portfolio with LH: number of active cases, average response time, cases at risk (no activity in 7+ days), and complaint trend. Share this proactively with RSV account managers on a weekly basis. The key insight: if RSV partners can see portfolio health before individual complaints surface, it shifts the relationship from "reactive fire-fighting" to "collaborative quality management."

**How It Addresses the Opportunity**
This doesn't directly prevent complaints — it changes the *nature* of the RSV-LH relationship. When an RSV partner can see "you have 5 cases with no activity in 10+ days," they know LH is monitoring and managing it, even if individual cases slip. It builds trust and gives RSV partners a reason to give LH more cases (transparency = trust = growth). It also creates external accountability pressure on LH to keep the numbers clean.

**Target Stakeholder**: RSV account managers (primary), LH operations leadership (use same dashboard internally)

**Key Assumptions**
1. We believe that RSV partners value proactive transparency over reactive explanations. We'll know this is true when RSV contacts express preference for the dashboard over the current complaint-response workflow.
2. We believe that sharing "cases at risk" data won't cause RSVs to panic or lose confidence — it'll build trust. We'll know this is true when RSVs who see the dashboard don't increase their complaint rate and express positive sentiment.
3. We believe that the case data needed for this dashboard can be aggregated reliably. We'll know this is true when prototype dashboard numbers match manually verified case status.

**Cheapest Test**
- **Method**: Manual report + interview
- **Description**: For one RSV partner (pick the most collaborative one), manually prepare a "Portfolio Health Report" (1-page PDF) showing: active cases, average response time, cases at risk, resolved complaints. Share it with their account manager. Interview them: Is this useful? Would you want this weekly? Does it change your perception of LH?
- **Duration**: 1 week
- **Success signal**: RSV contact says "this is exactly what we need" and asks for it regularly
- **Failure signal**: RSV contact says "this makes me worried about all these at-risk cases" (transparency backfires)

**Effort Estimate**: M (dashboard UI, data aggregation, RSV access management)
**Strategic Fit**: Strong — directly enables Phase 2 goal (RSV Customer Success), Pillar 4 (Data-Driven Infrastructure), and addresses Strategic Risk 1 (RSV Partner Churn)

**Risks**
- Transparency about at-risk cases scares RSV partners instead of building trust. *Mitigation*: Always pair "at-risk" data with "intervention taken" data — show the problem AND the response.
- Dashboard data accuracy issues embarrass LH. *Mitigation*: Validate data thoroughly before sharing; start with one trusted RSV partner.

---

### Comparison: Proactive Case Oversight

| Dimension | Solution A: Detection Engine | Solution B: Health Ritual | Solution C: RSV Dashboard |
|-----------|---------------------------|-------------------------|-------------------------|
| **Angle** | Technology | Process | Data / Partnership |
| **Speed to test** | Fast (2-3 day data analysis) | Fast (2 week pilot) | Medium (1 week) |
| **Upside if it works** | High — scalable, automated | Medium — effective but manual | High — builds RSV trust AND catches issues |
| **Downside risk** | Medium — alert fatigue | Low — easy to stop | Medium — transparency could backfire |
| **Effort (full build)** | M | S | M |
| **Strategic alignment** | Strong (Pillar 3+4) | Moderate (Pillar 3) | Strong (Pillar 4 + RSV success) |

**Trade-offs**: Solution A is the long-term answer — automated, scalable, data-driven. But it requires engineering investment. Solution B is the "do it today" answer — zero tech needed, validates the concept of proactive oversight. Solution C is the most strategically valuable — it turns an internal quality problem into an RSV relationship asset — but carries risk if data quality isn't solid.

**Recommended first test**: Solution A's retrospective data analysis (2-3 days). This costs almost nothing and answers the foundational question: can stalled cases actually be detected from existing data? The answer directly informs whether to invest in automation (A) or fall back to manual process (B). Run this in parallel with starting Solution B's pilot — they're complementary, not competing.

---

## Opportunity 3: Terminsvertreter (TV) Quality & Preparation

**Opportunity Statement**: Substitute lawyers sent to court hearings arrive unprepared, late, or behave unprofessionally, causing irrevocable legal harm to clients in high-stakes moments.
**Type**: Problem
**Sizing**: Pain: High | Reach: Significant | Frequency: Regular | **Score: 12**
**Source**: complaint-insights-march-2026.md (Opportunity #5)

**Evidence recap**: 4-5 TV-related complaints in March, including both high-severity cases (Jorg Nowak: irrevocable 1,000 EUR settlement after 30 years; Sofia Sovera: TV arrived late, no briefing, laughed at client). TV failures are uniquely damaging because court hearings are irreversible.

---

### Solution A: Structured TV Briefing Protocol

**Angle**: Process

**Core Idea**
Create a mandatory, standardized TV briefing protocol that must be completed before any court appearance. The protocol includes: (1) Written briefing document (case summary, client goals, negotiation boundaries, minimum acceptable outcomes) signed off by the primary lawyer. (2) Mandatory phone call between primary lawyer and TV at least 48 hours before the hearing. (3) Confirmation checklist that the TV has all required documents. No TV can appear in court without the briefing being marked complete in CaseForce.

**How It Addresses the Opportunity**
Most TV failures stem from the same root cause: the TV walks into court without knowing the case. A structured briefing closes this gap by making preparation mandatory and verifiable. The "minimum acceptable outcome" field is critical — it prevents the Jorg Nowak scenario where a TV accepts a catastrophic settlement because they had no mandate boundaries.

**Target Stakeholder**: Primary Lawyers (must complete briefing), TVs (receive briefing), Portfolio Managers (verify completion)

**Key Assumptions**
1. We believe that the primary cause of TV failure is inadequate briefing, not TV incompetence. We'll know this is true when properly briefed TVs achieve outcomes comparable to primary lawyers.
2. We believe that primary lawyers will complete the briefing protocol if it's mandatory and takes <30 minutes. We'll know this is true when compliance rate exceeds 90% within the first month.
3. We believe that a written "minimum acceptable outcome" field prevents catastrophic settlements. We'll know this is true when no TV accepts a settlement below the documented minimum.

**Cheapest Test**
- **Method**: Pilot process
- **Description**: For the next 10 TV assignments, require the primary lawyer to fill out a 1-page briefing template (case summary, client goals, min/max settlement range, key arguments, documents needed) and have a 15-minute phone call with the TV. Track: did the TV feel prepared? Did the hearing outcome meet expectations? Compare with recent TV outcomes without the protocol.
- **Duration**: 2-4 weeks (depends on hearing schedule)
- **Success signal**: TVs report feeling prepared; no outcome below documented minimum; client satisfaction higher
- **Failure signal**: Primary lawyers refuse to complete the briefing or do it superficially; TVs say it didn't help

**Effort Estimate**: S (template design, CaseForce checkbox, process enforcement)
**Strategic Fit**: Strong — directly enables Pillar 3 (Process Standardization, Quality Gates)

**Risks**
- Primary lawyers treat it as box-checking, writing superficial briefings. *Mitigation*: Portfolio Managers spot-check briefing quality; tie briefing quality to lawyer scorecard.
- The 48-hour advance requirement is unrealistic for last-minute TV assignments. *Mitigation*: Have an expedited version (30-min phone briefing minimum) for urgent cases.

---

### Solution B: TV Performance Gate

**Angle**: Incentive / Policy

**Core Idea**
Implement a strict quality gate for the Terminsvertreter pool: (1) Only approved TVs can take court appearances (separate vetting from general lawyer onboarding). (2) After every TV appearance, the client and primary lawyer each rate the TV (prepared? professional? outcome?). (3) TVs with scores below threshold are removed from the pool. (4) TVs with excellent scores get higher compensation per appearance.

**How It Addresses the Opportunity**
Currently there's no consequence for a TV doing a bad job and no reward for doing a good one. This creates a quality feedback loop: good TVs are incentivized to stay in the pool, bad TVs are filtered out. Over time, the average quality of TV appearances increases structurally.

**Target Stakeholder**: TVs (rated and incentivized), Primary Lawyers (rate TVs), Clients (rate TVs)

**Key Assumptions**
1. We believe that the TV pool contains both high and low performers, and filtering will improve average quality. We'll know this is true when performance ratings show meaningful variance (not everyone scores 3/5).
2. We believe that TVs respond to financial incentives (higher pay for better ratings). We'll know this is true when top-rated TVs accept more assignments and maintain quality.
3. We believe that client and lawyer ratings of TVs are reliable quality signals. We'll know this is true when ratings correlate with objective outcomes (e.g., settlement quality, complaint incidence).

**Cheapest Test**
- **Method**: Survey + data analysis
- **Description**: For the last 20 TV appearances, retroactively survey the primary lawyer and client: "How prepared was the TV? Would you want this TV again?" Cross-reference with case outcomes. See if there's a pattern — are certain TVs consistently rated poorly?
- **Duration**: 1 week
- **Success signal**: Clear differentiation — some TVs consistently good, others consistently bad. Filtering would meaningfully improve quality.
- **Failure signal**: Ratings are uniformly mediocre (systemic problem, not bad-apple problem) or sample too small to differentiate

**Effort Estimate**: M (rating system, TV management dashboard, compensation tiers)
**Strategic Fit**: Strong — aligns with strategy's "tiered lawyer system" and "offboarding of low performers"

**Risks**
- Shrinking the TV pool creates availability problems — not enough TVs for court dates. *Mitigation*: Only remove truly bad performers; invest in recruiting better TVs simultaneously.
- TVs feel surveilled and leave voluntarily. *Mitigation*: Frame as "quality recognition program" not surveillance; lead with the financial upside.

---

### Solution C: AI-Assisted TV Prep Package

**Angle**: Technology

**Core Idea**
Use AI to auto-generate a comprehensive TV preparation package from the case file: a 2-page case summary, key timeline, parties involved, relevant legal arguments, negotiation boundaries (from primary lawyer input), and a checklist of documents to bring. The package is auto-generated 72 hours before the hearing and sent to the TV. The primary lawyer only needs to review and add the negotiation boundaries — the rest is automated.

**How It Addresses the Opportunity**
The bottleneck in TV preparation is the primary lawyer's time. Most lawyers don't brief the TV because it takes 30-60 minutes they don't have. By automating 80% of the briefing (case summary, timeline, documents), the lawyer only needs to spend 5-10 minutes adding the strategic elements (negotiation range, key arguments to make). This makes comprehensive TV preparation the default rather than the exception.

**Target Stakeholder**: TVs (receive prep package), Primary Lawyers (review and augment)

**Key Assumptions**
1. We believe that AI can generate an accurate, useful case summary from CaseForce data. We'll know this is true when lawyers rate AI-generated summaries as 80%+ accurate in a blind test.
2. We believe that reducing lawyer prep effort from 30+ minutes to 5-10 minutes will increase briefing completion from rare to near-universal. We'll know this is true when briefing completion rate exceeds 90% with AI-assisted prep.
3. We believe that TVs who receive comprehensive prep packages perform measurably better. We'll know this is true when client satisfaction with TV appearances improves after rollout.

**Cheapest Test**
- **Method**: Wizard of Oz
- **Description**: For the next 5 TV assignments, have an internal team member (not AI) manually prepare a 2-page case summary from CaseForce data. Send it to the primary lawyer for review (takes 5 min). Send the reviewed package to the TV. Track: Did the TV find it useful? Did the lawyer find the review burden acceptable? Was the hearing outcome satisfactory?
- **Duration**: 2-4 weeks
- **Success signal**: TVs say "this is exactly what I needed"; lawyers say "5 min review is fine"; hearing outcomes improve
- **Failure signal**: Case summaries from CaseForce data are too incomplete to be useful; lawyers say "I still had to rewrite everything"

**Effort Estimate**: M-L (AI model for case summarization, integration with hearing calendar, automated delivery)
**Strategic Fit**: Strong — leverages Pillar 2 (AI-Powered Automation, Lawyer Assistance AI) for a high-impact use case

**Risks**
- AI-generated summaries contain errors that TVs rely on in court. *Mitigation*: Primary lawyer review is mandatory; mark AI-generated content as "draft — verify."
- CaseForce data isn't rich enough for meaningful summaries (incomplete case files). *Mitigation*: Wizard of Oz test reveals this quickly; if data is too thin, fall back to Solution A.

---

### Comparison: Terminsvertreter Quality

| Dimension | Solution A: Briefing Protocol | Solution B: Performance Gate | Solution C: AI Prep Package |
|-----------|----------------------------|---------------------------|---------------------------|
| **Angle** | Process | Incentive | Technology |
| **Speed to test** | Fast (next 10 TV assignments) | Fast (1 week retroactive survey) | Medium (2-4 weeks wizard of oz) |
| **Upside if it works** | High — directly prevents unprepared TVs | High — structural quality improvement | High — scales prep without lawyer effort |
| **Downside risk** | Low — easy to iterate | Medium — TV availability risk | Medium — AI accuracy risk |
| **Effort (full build)** | S | M | M-L |
| **Strategic alignment** | Strong (Pillar 3) | Strong (Pillar 3) | Strong (Pillar 2+3) |

**Trade-offs**: Solution A is the simplest and fastest — a checklist and mandatory call. It works if primary lawyers are willing to invest 30 minutes. Solution B is structural but slower — it improves the TV pool over time through filtering, but doesn't help with the next court hearing. Solution C is the most ambitious — it makes good preparation the default by removing the effort barrier. Best long-term answer but highest technical risk.

**Recommended first test**: Solution A (briefing protocol) immediately on the next 10 TV assignments AND Solution B's retroactive survey simultaneously. Solution A validates whether structured briefing improves outcomes; Solution B reveals whether the problem is systemic or concentrated in specific TVs. Together, these two cheap tests inform whether to invest in the AI approach (C) or whether process + filtering (A+B) is sufficient.

---

## Next Steps

### Recommended Assumption Tests (Priority Order)

| # | Opportunity | Solution | Assumption to Test | Test Method | Duration |
|---|------------|----------|--------------------|-------------|----------|
| 1 | Proactive Oversight | Stalled Case Detection | Can stalled cases be detected from CaseForce activity data? | Retrospective data analysis on 188 Jan-Mar complaints | 2-3 days |
| 2 | PA Responsiveness | Scorecard & Tiering | Is poor responsiveness concentrated in few lawyers or systemic? | Pull responsiveness scores from CaseForce for all lawyers | 3-5 days |
| 3 | TV Quality | Briefing Protocol | Does structured briefing improve TV hearing outcomes? | Pilot on next 10 TV assignments | 2-4 weeks |
| 4 | PA Responsiveness | Case Pulse Automation | Do generic status messages reduce client anxiety and complaints? | Manual concierge test on 50 cases | 2 weeks |
| 5 | Proactive Oversight | Health Ritual | Can PMs effectively catch and resolve stalled cases in weekly reviews? | 1 PM pilot for 2 weeks | 2 weeks |
| 6 | TV Quality | Performance Gate | Are TV quality issues concentrated in specific individuals? | Retroactive survey of last 20 TV appearances | 1 week |

**Recommended sequencing**: Tests 1+2 can run in parallel this week (pure data analysis, no process changes). Their results directly inform which solutions to pilot next. Tests 3+6 can also start immediately since TV assignments happen on their own schedule. Tests 4+5 should start after 1+2 complete, informed by the findings.

### Solutions That Overlap with Previous Brainstorms
No existing solution files found — this is the first brainstorm.

---

## References

- **Opportunity Sources**:
  - `.claude/product/discovery/opportunities/complaints/complaint-insights-march-2026.md`
  - `.claude/product/discovery/opportunities/complaints/complaint-insights-jan-feb-2026.md`
  - `.claude/product/discovery/opportunities/interview-cyfire-lh-product-2026-03-03.md`
  - `.claude/product/discovery/opportunities/survey-partner-lawyers-2026-03-03.md`
- **Existing Solution Files**: None (first brainstorm)
- **Product Strategy**: `.claude/product/strategy/product-strategy-2026.md`
