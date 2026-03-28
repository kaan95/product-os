# Solution Brainstorm: Lawyer Did Not Take Next Step / Forgot About Case

**Date**: 2026-03-16 | **Score**: Not yet RICE-scored (Reach: 3) | **Constraints**: Quick to implement. Must complement (not duplicate) the existing AI-prioritized to-do list initiative (PD-9, PD-25, PD-38, PD-90).

**Opportunity**: Lawyers managing high caseloads forget to take the next step on cases, leaving clients waiting without updates. There is no system to prevent this beyond reactive complaint handling.
**Type**: Problem
**Evidence**:
- "Keine Rückmeldung" is the #1 complaint reason every month -- 39 cases in Q1 2026
- One PA managed a case for 1.5+ years without LH oversight
- Root structural cause: low RSV compensation makes extensive communication economically unviable
- Lawyers explicitly mentioned no alerting system for overdue responses (Cyfire interview)

**Key Assumption**: The AI to-do list will solve **"which case needs attention."** These solutions target what happens **after** the lawyer knows a case needs attention but still doesn't act -- because the action itself is too effortful, too slow, or too unclear.

---

## Solutions

| # | Title | Angle | Effort | Test Speed |
|---|-------|-------|--------|------------|
| 1 | One-Click Status Updates | Design / UX | S | Fast |
| 2 | Smart Case Snoozing | Design / UX | S | Fast |
| 3 | Morning Push Briefing | Technology | S | Fast |
| 4 | Automated Client Status Pings | Technology / Process | S-M | Fast |
| 5 | Contextual Quick-Reply Buttons | Design / UX | S | Fast |
| 6 | Case Aging Visual Indicators | Design / UX | S | Fast |

---

### 1. One-Click Status Updates

**Angle**: Design / UX

Add pre-written, case-context-aware status messages that the lawyer can send to the client with one click. Based on the case stage, the system offers 2-3 ready-made messages: "Your case is being reviewed," "We're waiting for documents from the opposing party," "Coverage has been confirmed, we'll proceed with [next step]." The lawyer taps one, optionally edits, and it's sent. Reduces a 10-minute email task to 5 seconds.

**Why it works**: The #1 reason lawyers don't communicate isn't that they forgot -- it's that writing an individual update email for every case is economically irrational at RSV compensation levels. If we collapse "send an update" from a 10-minute writing task to a 5-second tap, the cost-benefit equation flips. The lawyer can clear 10 status updates in the time it previously took to write one.

**Riskiest assumption**: We believe that templated status messages are "good enough" for clients -- that receiving a semi-generic update is significantly better than silence. We'll know when clients who receive one-click updates file fewer complaints than those who receive no update at all.

**Cheapest test**: Create 5 status message templates per case stage. Have an ops team member send them manually (on behalf of the lawyer) for 30 overdue cases. Measure: do clients respond positively? Does complaint rate drop? Do lawyers say "I would have sent this myself if it were one click"? -- 2 weeks -- Success: client satisfaction improves, lawyers say they'd use it. Failure: clients complain messages are too generic.

**Effort**: S

---

### 2. Smart Case Snoozing

**Angle**: Design / UX

Let lawyers explicitly snooze a case with a reason and a wake-up date. Reasons are structured: "Waiting for court date," "Waiting for client documents," "Waiting for RSV coverage decision," "Waiting for opposing party." When the snooze expires, the case pops back to the top of their list with a "Wake up: action needed" flag.

**Why it works**: Today, CaseForce can't distinguish between "I'm intentionally waiting on this case" and "I forgot about this case" -- they both look like inactivity. Snoozing lets lawyers legitimately park cases, which means every case that ISN'T snoozed is one they genuinely need to act on. It also makes "forgot" cases visible by elimination: if it's not snoozed and it's not active, the lawyer has no excuse. Combined with the AI to-do list, snoozing dramatically improves signal quality -- the AI only surfaces truly neglected cases, not ones that are legitimately parked.

**Riskiest assumption**: We believe that lawyers will actually use the snooze feature rather than ignoring it. We'll know when >50% of inactive cases are either snoozed (with a valid reason) or acted on within 48h of the feature being available.

**Cheapest test**: Add a simple "snooze" button to the case list (or simulate via a Google Form/Slack workflow). For 10 lawyers, ask them to categorize their inactive cases: "snooze with reason" or "needs action." See if the remaining "needs action" list is small enough to be actionable. -- 1 week -- Success: lawyers engage, the unsnoozed list is manageable and actionable. Failure: lawyers snooze everything to avoid accountability.

**Effort**: S

---

### 3. Morning Push Briefing

**Angle**: Technology

Every morning at 8:00am, send the lawyer a brief push message (WhatsApp, SMS, or email) with their daily case summary: "Good morning. 3 cases need your attention today. #1: Meier -- no client contact in 12 days -- suggest: send status update. Tap to open." Direct deep link into CaseForce. No app download needed. Essentially the AI to-do list, but delivered proactively to the lawyer's phone instead of waiting for them to log in.

**Why it works**: The AI to-do list is powerful but passive -- the lawyer has to open CaseForce to see it. Many lawyers don't log in daily. A morning push message reaches them before their day fills up, in the channel they already check (WhatsApp/SMS). It's the difference between "information available" and "information delivered."

**Riskiest assumption**: We believe that lawyers will read and act on a daily morning message rather than muting it. We'll know when >60% of morning messages are opened and >30% result in case activity within 4 hours.

**Cheapest test**: Manually send 10 lawyers a WhatsApp message at 8am for 2 weeks with their top 3 overdue cases (pulled from CaseForce the evening before). Track open rates, case activity within 4 hours, and lawyer feedback. -- 2 weeks -- Success: lawyers act on the flagged cases; several say "keep doing this." Failure: messages ignored, lawyers say it's annoying.

**Effort**: S (WhatsApp Business API or simple email, data query, template)

---

### 4. Automated Client Status Pings

**Angle**: Technology / Process

If a lawyer hasn't communicated with the client in 7 days, the system automatically sends a brief, friendly status message to the client on behalf of Legalhero (not the lawyer): "We wanted to let you know your case is being handled. Current stage: [Coverage confirmed / Claim submitted / Awaiting court date]. Your lawyer will be in touch with a detailed update soon. Questions? Reply here." This buys the lawyer time, keeps the client informed, and prevents the silence that triggers complaints.

**Why it works**: The majority of "Keine Rückmeldung" complaints aren't about legal substance -- they're about silence. Clients don't need a detailed legal update every week; they need to know they haven't been forgotten. An automated ping from LH ("your case is being handled") breaks the silence at near-zero cost. It's not a substitute for lawyer communication -- it's a safety net that prevents the 2-week silence gap that triggers RSV escalation.

**Riskiest assumption**: We believe that a generic status message from LH (not the lawyer) reduces client anxiety enough to prevent complaint escalation. We'll know when clients who receive auto-pings file complaints at <50% the rate of those who don't.

**Cheapest test**: For 50 cases with 7+ days of lawyer inactivity, manually send a templated email from a Legalhero address: "We wanted to update you..." Track: do these clients file fewer complaints over the next 14 days vs. a control group of 50 similar cases that don't receive the message? -- 3 weeks -- Success: complaint rate drops >40% for the test group. Failure: clients respond with "I want to hear from MY lawyer, not you" or the message sets expectations that aren't met.

**Effort**: S-M (auto-trigger based on inactivity, case stage mapping for status text, email delivery)

**Three-sided market note**: Helps clients (less silence) and RSVs (fewer complaints). Lawyers might feel uncomfortable if LH messages clients "on their behalf" -- key is to send it from LH, not from the lawyer. Frame as platform-level service, not lawyer impersonation.

---

### 5. Contextual Quick-Reply Buttons

**Angle**: Design / UX

In the case detail view, show 3-4 contextual action buttons based on the current case stage and what the AI to-do list recommends. For example, at "Coverage Confirmed" stage: [Send claim letter to opposing party] [Update client on coverage status] [Request missing documents from client]. Each button pre-fills the appropriate message or action with case-specific data already inserted. The lawyer reviews, optionally edits, and executes.

**Why it works**: Even when a lawyer knows which case needs attention (thanks to the AI to-do list), they still face a blank screen: "OK, now what do I do?" Contextual quick-reply buttons answer that question instantly. They turn the AI's recommendation into an executable action with one click. This is the natural extension of the to-do list: the list says "act on this case," the buttons say "here's exactly how."

**Riskiest assumption**: We believe that we can accurately predict the right 3-4 actions per case stage, and that lawyers will trust and use these suggestions. We'll know when >40% of prompted actions are executed (with or without edits).

**Cheapest test**: For the top 5 most common case stages, define the 3 most common next actions (from ops team knowledge). Mock them up as buttons in a Figma prototype. Show to 5 lawyers: "If you saw these on your case view, would you use them? Are these the right actions?" -- 1 week -- Success: lawyers say "yes, these are exactly what I'd do" and would click them. Failure: lawyers say the suggestions are wrong or they need full customization every time.

**Effort**: S (builds directly on top of the AI to-do list initiative)

---

### 6. Case Aging Visual Indicators

**Angle**: Design / UX

Add color-coded aging indicators to the existing case list view. Green = active (activity in last 3 days). Yellow = cooling (5+ days). Orange = at risk (10+ days). Red = critical (14+ days). No new features, no new views -- just a visual layer on what already exists. The case list becomes a heat map of urgency. Red cases are visually impossible to ignore.

**Why it works**: The current case list treats all cases the same visually. A case with activity yesterday looks identical to one that's been dormant for 3 weeks. Color-coding exploits a basic psychological principle: red = danger = attention. Lawyers scanning their case list will naturally gravitate toward red items. This is the simplest possible intervention -- zero workflow change, zero learning curve, just visual urgency.

**Riskiest assumption**: We believe that visual urgency indicators will change scanning and clicking behavior -- that lawyers will prioritize red cases over green ones. We'll know when average time-to-action for cases that would be "red" decreases after the feature launches.

**Cheapest test**: No test needed for validation -- this is low-risk enough to ship directly. If testing is desired: create a simple mockup showing the color-coded list and show to 5 lawyers. Ask: "Does this change which case you'd click first?" -- 1 day -- Success: lawyers say "obviously yes." Failure: lawyers say "I already know which cases are old."

**Effort**: S (CSS-level change + query for last activity date, which likely already exists)

---

## Comparison

| Dimension | Sol 1: One-Click Status | Sol 2: Smart Snooze | Sol 3: Morning Push | Sol 4: Auto Client Ping | Sol 5: Quick-Reply Buttons | Sol 6: Aging Colors |
|-----------|------------------------|--------------------|--------------------|------------------------|--------------------------|-------------------|
| **Angle** | UX | UX | Technology | Tech/Process | UX | UX |
| **Mechanism** | Reduce effort to communicate | Separate "waiting" from "forgot" | Deliver to-do proactively | Break client silence automatically | Turn recommendations into actions | Make urgency visible |
| **Complements AI to-do list?** | Yes -- makes acting on items effortless | Yes -- improves signal quality | Yes -- delivers it outside the app | Independent -- safety net layer | Yes -- natural extension | Yes -- visual urgency layer |
| **Test speed** | 2 weeks | 1 week | 2 weeks | 3 weeks | 1 week | 1 day |
| **Upside** | High | Med-High | Med-High | High | High | Med |
| **Risk** | Low | Low | Low | Med (client perception) | Low | Low |
| **Effort** | S | S | S | S-M | S | S |

**Start here**: These solutions form a **stack**, not alternatives:

1. **Ship now** (no test needed): **Sol 6 (Aging Colors)** -- pure visual layer, zero risk, immediate impact
2. **Test this week**: **Sol 2 (Smart Snooze)** -- dramatically improves signal quality for the AI to-do list
3. **Test next week**: **Sol 1 (One-Click Status)** + **Sol 5 (Quick-Reply Buttons)** -- together they make acting on the AI to-do list effortless
4. **Test in parallel**: **Sol 4 (Auto Client Ping)** -- independent safety net that catches what the lawyer-facing solutions miss
5. **Layer on after AI to-do list ships**: **Sol 3 (Morning Push)** -- delivers the to-do list to the lawyer's phone

---

## Overlaps with Previous Brainstorms

**`lawyer-case-neglect-solutions-2026-03-10.md`**:
- Sol A (Friction-Free Next Action) -- **Partial overlap** with Sol 1 (One-Click Status) and Sol 5 (Quick-Reply Buttons). The prior brainstorm's version was a full case list redesign. These are lighter, more focused implementations of the same principle (reduce effort to act). Can be seen as the "quick-ship" versions of Sol A.
- Sol B (Personal Inactivity Digest) -- **Conceptual overlap** with Sol 3 (Morning Push). Digest is weekly email with stats; Morning Push is daily actionable notification. Different cadence, different content, different channel.
- Sol C (Social Accountability Layer) -- **No overlap**.

**`complaint-reduction-brainstorm-2026-03-06.md`**:
- Case Pulse Automation -- **Partial overlap** with Sol 4 (Auto Client Ping). Pulse includes lawyer reminders + escalation + client message. Sol 4 focuses purely on the client-facing auto-message as a standalone quick win.
- All other solutions -- **No overlap**.

**Existing AI to-do list initiative (PD-9, PD-25, PD-38, PD-90)**:
- These 6 solutions are explicitly designed to **complement** the initiative, not replace it. The to-do list answers "which case?" -- these solutions answer "now what?" (Sol 1, 5), "how do I get there?" (Sol 3), "is this really neglected?" (Sol 2), "what does the client see?" (Sol 4, 6).

---

## References

- **Jira**: PD-46, PD-9, PD-25, PD-38, PD-90
- **Prior brainstorms**: `lawyer-case-neglect-solutions-2026-03-10.md`, `complaint-reduction-brainstorm-2026-03-06.md`
- **Opportunity data**: `complaint-opportunities-q1-2026.md` (Opportunity #1, #2, #11)
- **Strategy**: Pillar 1 (Platform Orchestration), Pillar 3 (Process Standardization)

**Saved to**: `.claude/product/discovery/solutions/lawyer-case-neglect-solutions-2026-03-16.md`
