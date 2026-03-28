# Interview Synthesis - Andrés Jansen (DE Lawyer)

**Interview Date**: 2026-02-17
**Interview Type**: Internal User (Lawyer using CaseForce)
**Synthesized**: 2026-02-24
**Synthesized By**: Claude (Product Interview Synthesis)

---

## Executive Summary

Andrés Jansen is a German lawyer on the Legalhero team based in the Wiesbaden area who handles employment law cases (Arbeitsrecht) including termination, appeals, and accident/tort matters. The session was a product feedback interview conducted by the product team, combining a case walkthrough with targeted questions about workflow and specific CaseForce features.

Three clear themes emerged: (1) **case list structure and navigation** is sub-optimal — new cases are buried at the bottom and require scrolling rather than surfacing prominently; (2) **document upload should be integrated with client communication** — currently a two-step process that wastes 5-10 minutes per document; and (3) **the AI case summary is read regularly but needs format improvement** — full sentences should be replaced with bullet points. These are all relatively quick to address and would have immediate daily impact.

A fourth, more nuanced finding concerns **proactive client communication and the "days since contact" indicator**: the feature exists but the lawyer's rational for not contacting a client in 200 days reveals a gap between what the metric measures and what actually matters — a "no contact needed" status is missing, and the current implementation may create false urgency or be quietly ignored.

---

## Interview Context

**Interviewee**: Andrés Jansen
**Company/Segment**: Legalhero Germany (Wiesbaden area)
**Use Case**: Daily case management — appeals (Berufungsverfahren), employment law (Arbeitsrecht), accident/tort cases (Schadensregulierung)
**Current Solution**: CaseForce (migrated from legacy system)
**Interview Focus**: Case walkthrough, case list UX, AI summary feedback, document workflow

---

## Key Insights

### 🎯 Top Insights (Prioritized)

#### 1. New Cases Are Buried at the Bottom of the Case List — Priority: 🔴 Critical

**What We Learned**:
When the case list is sorted by deadline (Frist), newly assigned cases with no deadline land at the very bottom of the list. Lawyers know this and deliberately scroll to the bottom to find unworked new cases — treating "bottom of list" as a proxy for "new/unstarted." This was the opposite behavior in the legacy system, where new cases appeared at the top. The lawyer found the current list "unübersichtlich" (confusing/unclear).

**Evidence from Interview**:
> "Da weiß ich, dass so die aktuelleren Fälle liegen hier unten, ja."
("That's where I know the more recent cases are — down at the bottom, yes.")

> "Das ist so ein bisschen anders als früher im Legacy. Da waren die, glaube ich, sehr weit oben."
("That's a bit different from the legacy system. There they were, I think, right at the top.")

> "Findest du, dass das eine gute Lösung ist, dass du immer ganz unterscrollen musst?"
("Do you think it's a good solution that you always have to scroll all the way down?")
[Lawyer's response: "Ich finde es grundsätzlich irgendwie etwas unübersichtlich." / "I find it fundamentally a bit unclear/disorganized."]

**Why This Matters**:
New case awareness and prompt first action is critical for SLA compliance and client satisfaction. If the primary mechanism for discovering new cases is "scroll to the bottom," it is fragile — easily overlooked and not intuitive for new or less experienced lawyers. It also creates an implicit coupling between "deadline sort" and "case age" that breaks down as soon as a new case has a deadline set (it would jump up and no longer read as "new").

**Root Cause**:
The case list default sort (by deadline/Frist) doesn't accommodate a "new / no deadline" state. Cases with no deadline get sorted to the bottom as a byproduct of the algorithm, not by design. There is no explicit "New" flag or dedicated "New Cases" section.

**Recommended Action**:
- [ ] Add a dedicated "New Cases" section or badge at the top of the case list, showing cases assigned within the last X days with no activity
- [ ] Alternatively: add a sort option or filter for "New / Unstarted" cases
- [ ] Evaluate showing new cases at top within the deadline-sort order (similar to legacy behavior)
- [ ] Confirm with more lawyers whether "new at top" was universally preferred in legacy or whether it created other problems

**Impact if Addressed**: Eliminates a daily discovery risk for new cases; improves SLA compliance by ensuring lawyers notice new assignments immediately.
**Effort Estimate**: Low-Medium
**Priority Score**: 21/25

---

#### 2. Document Upload and Client Communication Are Unnecessarily Disconnected — Priority: 🟡 High

**What We Learned**:
When a lawyer uploads a document (e.g., a court expert report, a letter), they frequently also need to send it to the client. Currently, this requires two separate steps: upload the document, then manually compose and send a separate email using a text template (Textbaustein). The lawyer explicitly proposed the fix: after upload, the system should ask "Do you want to send this document to the client?" — similar to how CaseForce prompts for appointment type after creating an appointment.

**Evidence from Interview**:
> "Wenn ich ein Dokument hochlade und vom System gefragt werde, soll das Dokument an den Mandanten versandt werden. Das fände ich eine tolle Optimierung."
("If I upload a document and the system asks me whether the document should be sent to the client — I'd find that a great optimization.")

> "Einfach würde wieder 10 Minuten Zeit wegnehmen. 5 Minuten. Wie auch immer."
("Simply would save another 10 minutes. 5 minutes. However long.")

**Why This Matters**:
This is a high-frequency, low-friction improvement. Uploading documents and notifying clients is a routine step in nearly every case progression event (court orders, expert reports, contracts, letters). Saving 5-10 minutes per instance compounds across hundreds of cases. It also reduces the risk of forgetting to notify the client — a service quality issue.

**Root Cause**:
The document module and the email/communication module are not integrated. Document upload is a standalone action with no downstream workflow hooks.

**Recommended Action**:
- [ ] After successful document upload, show a prompt/modal: "Would you like to send this document to [client name]?"
- [ ] Pre-populate a standard Textbaustein (text template) in the compose view, with the document already attached
- [ ] Allow the lawyer to customize the message before sending or dismiss to skip
- [ ] Track skip rate and send rate to understand actual usage

**Impact if Addressed**: Saves 5-10 minutes per document-share event; reduces client notification omissions; improves perceived service quality.
**Effort Estimate**: Low-Medium
**Priority Score**: 20/25

---

#### 3. AI Case Summary Uses Full Sentences — Should Use Bullet Points — Priority: 🟢 Medium

**What We Learned**:
Andrés reads the AI case summary regularly, which is a positive signal. However, he finds the format too verbose — full sentences rather than concise bullet points. He wants to skim key facts quickly, not read paragraphs.

**Evidence from Interview**:
> "Ich schaue sie mir regelmäßig an, ich würde sie aber eben verkürzen auf Stichpunkte, also nicht als zusammenfassende Sätze."
("I look at them regularly, but I would shorten them to bullet points — not as full summarizing sentences.")

**Why This Matters**:
Lawyers operate in a high-context, time-pressured environment. The AI summary is most valuable as a fast re-orientation tool ("bring me back up to speed on this case in 15 seconds"). Full sentences slow that down. This is a quick content/format change with no structural redesign needed.

**Root Cause**:
The AI prompt generating the summary was likely optimized for completeness and fluency (full sentences) rather than scannability. The format choice doesn't match how lawyers actually consume this information in context.

**Recommended Action**:
- [ ] Update the AI summary prompt to output structured bullet points instead of full paragraph sentences
- [ ] Test new format with 2-3 lawyers before rolling out broadly
- [ ] Consider a hybrid: short bullet points for key facts, with an option to expand for full narrative

**Impact if Addressed**: Faster case re-orientation; higher daily utility of an already-used feature.
**Effort Estimate**: Very Low (prompt change)
**Priority Score**: 16/25

---

#### 4. "Days Since Client Contact" Metric Is Not Contextually Meaningful — Priority: 🟢 Medium

**What We Learned**:
The case list shows a hourglass indicator with the number of days since last client contact. During the walkthrough, a case showed 200 days with no contact. The product team asked why — the lawyer had a completely valid reason (the client had low interest in the case, the expert report confirmed favorable outcome, the matter was pending a court date with nothing actionable for the client). The system flagged the case as potentially neglected; the reality was the opposite.

**Evidence from Interview**:
> "Da bin ich, also wie gesagt, grundsätzlich ist jetzt von Seiten des Mandanten nicht mehr das große Interesse da."
("As I said, fundamentally, the client no longer has much interest in the case.")

> "Das Gutachten, werden wir auch noch machen, kann das Gutachten natürlich an den Mandanten noch mal geschickt werden, um einfach ihm auch das Gefühl... aber am Ende ist das jetzt für mich jetzt nicht so entscheidend."
("We could still send the expert report to the client to give them the feeling... but in the end it's not so critical for me.")

**Why This Matters**:
A metric that shows 200 days no contact creates false alarm for cases in a "waiting" phase (pending court date, pending expert opinion, waiting for counterparty response). This could cause two problems: (1) lawyers dismiss the indicator as noise because it fires in cases that don't need action; (2) genuinely neglected cases get lost in the noise. The metric needs contextual intelligence — it should distinguish between "waiting intentionally" and "stuck/neglected."

**Root Cause**:
The "days since contact" metric measures communication activity as a proxy for case health, but not all case stages require active client communication. There is no "pause" or "waiting" state that contextualizes the absence of contact as intentional.

**Recommended Action**:
- [ ] Add a "Waiting" or "Pending" status or tag that suppresses the contact-days alert for cases where the next step is awaiting a third party (court, counterparty, expert)
- [ ] Alternatively, allow lawyers to set a "Next expected event" date — if that date hasn't passed, the hourglass doesn't turn red
- [ ] Research with more lawyers: what is the right threshold for proactive contact alerts vs. stage-appropriate silence?

**Impact if Addressed**: Reduces alert fatigue; makes the metric actionable rather than ambient noise; supports better case health monitoring.
**Effort Estimate**: Medium
**Priority Score**: 15/25

---

#### 5. Complex and Atypical Cases (Replik, Berufung) Consume Disproportionate Time — Priority: 🟡 High (Strategic)

**What We Learned**:
Standard templates (Vorlagen) work well for typical case types (termination, standard sick leave, performance cases). But complex or atypical cases — fraud allegations, embezzlement (Untreue, Unterschlagung), or detailed appellate briefs (Berufungserwiderung) — require heavily custom work where templates provide little leverage. A single appeals case took 12 hours (2 days x 6 hours). Similarly, all Replik filings (counter-briefs responding to the defendant's reply) are inherently time-intensive even with templates.

**Evidence from Interview**:
> "Das war jetzt tatsächlich mal so ein Fall, wo ich jetzt wenig mit eigenen Vorlagen arbeiten konnte, weil das so ein bisschen abstrakt einfach war."
("This was actually a case where I could use few of my own templates because it was just a bit abstract.")

> "Hier war das schon so ein Fall, wenn jetzt hier jemandem Betrug unterstellt wird, Unterschlagung und wer weiß was, es hat einfach dann mehr Zeit gekostet."
("Here this was already such a case that when someone is accused of fraud, embezzlement and who knows what, it just costs more time.")

> "Grundsätzlich bei jeder Replik... würde ich jetzt schon pauschal sagen, dass jede Replik seine Zeit beansprucht."
("In principle with every Replik... I would say broadly that every Replik takes its time.")

**Why This Matters**:
Lawyer time is the primary cost driver for Legalhero's margin per case. Complex and appellate cases are the long tail that most erodes profitability. Templates help in the standard case; AI-assisted drafting (like the ChatGPT workflow discovered in the NL team) could be the lever for complex cases. This is a strategic opportunity to apply AI where the ROI is highest.

**Root Cause**:
CaseForce templates are designed for common case patterns. Atypical factual situations (criminal allegations, complex corporate disputes) require deep legal reasoning that templates cannot pre-structure. No AI drafting assistance exists within CaseForce for these document types.

**Recommended Action**:
- [ ] Investigate AI-assisted drafting for Replik / Berufungserwiderung documents as a high-value AI feature
- [ ] Explore whether the ChatGPT workflow used by the NL team (see Wiecher interview synthesis) can be adapted for German appellate/Replik cases
- [ ] Follow up with Andrés specifically about which parts of the Replik drafting are most time-consuming (research, structure, or writing)

**Impact if Addressed**: Even a 30% time reduction on Replik/appellate filings would save multiple hours per case; significant margin impact at scale.
**Effort Estimate**: High
**Priority Score**: 17/25

---

#### 6. Case List Sort Logic Needs Refinement — Appointments Should Follow Deadlines — Priority: 🟢 Medium

**What We Learned**:
Andrés sorts by Frist (deadline) as the primary priority, which is correct. But he expressed a preference for Termine (court appointments) to appear directly below deadline-sorted cases, rather than being mixed or deprioritized. Cases without any appointment should appear last.

**Evidence from Interview**:
> "Sortierung nach Fristen hat höchste Priorität, aber Termine sollten direkt darunter folgen."
("Sorting by deadlines has highest priority, but appointments should follow directly below.")

> "Dann einfach alle Termine nach oben verlegen und alle terminlosen Fälle... am Ende stehen."
("Then simply move all appointments up and all cases without appointments... stand at the end.")

**Why This Matters**:
The case list is the primary daily working view for lawyers. A well-structured sort order directly maps to how lawyers plan their workday. The current sort mixing cases with upcoming appointments in among deadline-sorted cases reduces clarity.

**Recommended Action**:
- [ ] Design a sort hierarchy: (1) Cases with active deadlines, (2) Cases with upcoming Termine, (3) New cases without deadline/appointment, (4) All other cases, (5) Cases in waiting state
- [ ] Consider a "smart sort" mode that implements this automatically vs. requiring manual configuration
- [ ] Validate this sort preference with additional lawyers to confirm it generalizes

**Effort Estimate**: Low-Medium
**Priority Score**: 15/25

---

## Improvement Areas by Category

### 🔴 Critical Issues (Must Address)

**New Cases Buried at Bottom of Case List**
- **Problem**: In deadline-sort mode, newly assigned cases with no deadline appear at the very bottom, requiring lawyers to scroll to discover them
- **User Impact**: New case discovery relies on an implicit convention ("bottom = new") that is fragile and unintuitive; creates SLA risk
- **Quote**: > "Ich finde es grundsätzlich irgendwie etwas unübersichtlich."
- **Recommendation**: Surface new cases prominently — dedicated section at top, "New" badge, or explicit new-case sort option
- **Timeline**: Next Sprint
- **Owner**: Engineering (Frontend)

---

### 🟡 High-Value Opportunities

**Document Upload → Client Notification Integration**
- **Opportunity**: Add a "Send to client?" prompt after document upload, pre-populating a standard template email with the document attached
- **Business Impact**: Saves 5-10 minutes per document-share event; reduces risk of client notification omissions; improves perceived service quality
- **User Benefit**: One flow instead of two; reduces cognitive overhead of remembering to follow up
- **Quote**: > "Wenn ich ein Dokument hochlade und vom System gefragt werde, soll das Dokument an den Mandanten versandt werden. Das fände ich eine tolle Optimierung."
- **Recommendation**: Post-upload modal with "Send to client?" option + pre-populated template message
- **Timeline**: Next Sprint / This Month
- **Effort vs. Impact**: Low effort / High impact

**AI-Assisted Replik / Appellate Brief Drafting**
- **Opportunity**: Apply AI drafting capabilities to the most time-intensive document type in the German lawyer workflow
- **Business Impact**: Replik/Berufungserwiderung cases take 6-12 hours; even 30% reduction saves hours per case at scale
- **User Benefit**: Dramatically reduces time on the most cognitively demanding document type
- **Quote**: > "Trotzdem würde ich jetzt schon pauschal sagen, dass jede Replik seine Zeit beansprucht."
- **Recommendation**: Investigate as part of the broader AI Case Assist feature (aligned with NL ChatGPT workflow discovery)
- **Timeline**: This Quarter (discovery/design)
- **Effort vs. Impact**: High effort / Very high impact

---

### 🟢 Quick Wins

**AI Case Summary — Bullet Points Instead of Sentences**
- **What**: Change the AI prompt to output structured bullet points rather than full prose paragraphs
- **Why**: Lawyers want to skim, not read; bullets match mental model for case re-orientation
- **Effort**: Very Low (prompt update)
- **Impact**: Medium (improves utility of already-used feature)
- **Timeline**: This Sprint
- **Implementation Notes**: Update system prompt; test with 2-3 lawyers before rollout

**Case List Sort Hierarchy**
- **What**: Refine sort order to: deadlines → appointments → new cases → waiting cases
- **Why**: Current sort mixes appointments and deadlines without clear hierarchy
- **Effort**: Low-Medium
- **Impact**: Medium
- **Timeline**: Next Sprint

---

### 🔵 Long-term Enhancements

**Contextual Client Contact Status ("Waiting" State)**
- **Vision**: Replace the raw "days since contact" metric with a context-aware case health indicator that understands when silence is appropriate (waiting on court, expert, counterparty)
- **Strategic Value**: Makes the contact indicator genuinely useful and actionable rather than noisy; supports better case health monitoring at scale
- **User Need**: Lawyers need to distinguish between "deliberately waiting" and "neglected" cases
- **Timeline**: 3-6 months
- **Dependencies**: Requires case stage/status model that captures "waiting on X" states; alignment with case management workflow design

**AI-Powered Replik Drafting (CaseForce Native)**
- **Vision**: An AI drafting tool within CaseForce that can analyze the opposing brief (Klageerwiderung), identify the key arguments, and produce a structured draft counter-argument (Replik) for the lawyer to refine
- **Strategic Value**: Addresses the highest-cost case activity for German lawyers; significant margin impact if adopted
- **Timeline**: 6-12 months
- **Dependencies**: Broader AI Case Assist infrastructure; legal document parsing capability; validation with lawyers on quality bar

---

### ❓ Research Questions

**How generalizable is the "new cases at top" preference?**
- **What We Don't Know**: Whether all lawyers share this preference or whether lawyers who use deadlines/follow-ups extensively have different needs
- **Why It Matters**: A sort change that solves the problem for one segment might create friction for another
- **How to Answer**: Quick survey or follow-up interviews with 3-5 additional DE lawyers
- **Next Step**: Add to next lawyer interview agenda

**What specifically makes Replik drafting so time-intensive?**
- **What We Don't Know**: Whether the bottleneck is research, legal argumentation, writing, or structure — matters for AI tool design
- **Why It Matters**: Determines whether AI can help at all and at which stage
- **How to Answer**: Follow-up session with Andrés specifically focused on a Replik case walkthrough
- **Next Step**: Schedule Replik-specific session

**When do lawyers expect to contact clients vs. let cases wait?**
- **What We Don't Know**: A systematic understanding of case stages where proactive client contact is expected vs. not
- **Why It Matters**: Needed to build the "waiting state" feature correctly
- **How to Answer**: Map client communication norms across case types with a small group of DE lawyers
- **Next Step**: Add to next research sprint

---

## Themes & Patterns

### Theme 1: Sorting and Navigation Are the Primary Daily Workflow Friction
**Frequency**: Discussed ~8 times throughout the session
**Sentiment**: Mildly frustrated, constructive
**Key Points**:
- New cases appear at the bottom — counterintuitive and fragile
- Deadline sort is correct as primary, but appointments need to be subordinated clearly
- Legacy system behavior was better for surfacing new cases
- The list is described as "unübersichtlich" (unclear/disorganized) overall

**Representative Quotes**:
> "Ich finde es grundsätzlich irgendwie etwas unübersichtlich."
> "Das ist so ein bisschen anders als früher im Legacy. Da waren die, glaube ich, sehr weit oben."

**Analysis**: Navigation and sort order are the foundational UX layer that every other feature rests on. If lawyers struggle to find cases or understand the list structure, everything else is harder. The mismatch with legacy behavior also creates an onboarding/relearning burden.

---

### Theme 2: Document Upload Is an Integration Dead-End
**Frequency**: Mentioned explicitly as a feature request once, but surfaces as a structural gap in the case walkthrough
**Sentiment**: Pragmatic; clear request, not emotionally charged
**Key Points**:
- Document upload doesn't connect to client communication
- Requires a separate email workflow every time a document needs to be shared
- Lawyer self-diagnosed the fix: a "send to client?" prompt similar to existing appointment prompts

**Representative Quotes**:
> "Wenn ich ein Dokument hochlade und vom System gefragt werde, soll das Dokument an den Mandanten versandt werden."
> "Einfach würde wieder 10 Minuten Zeit wegnehmen."

**Analysis**: This is a classic workflow integration gap — two actions that are almost always sequential are treated as independent in the system. The lawyer's proposed solution is well-designed and directly implementable.

---

### Theme 3: AI Features Are Seen as Useful But Need Refinement
**Frequency**: AI summary discussed 3-4 times; proposed approach discussed once
**Sentiment**: Positive (uses it, wants to keep it) with format critique
**Key Points**:
- AI case summary is actively read, which is strong adoption signal
- Format (full sentences) doesn't match how lawyers consume the information
- AI proposed approach is well-received

**Representative Quotes**:
> "Ich schaue sie mir regelmäßig an, ich würde sie aber eben verkürzen auf Stichpunkte."
> "Das finde ich gut mit dem vorgeschlagenen Vorgehen."

**Analysis**: The fact that the AI summary is read regularly is significant — it means the feature has achieved adoption. The format change is a quick win to deepen the value. The positive reception of the proposed approach section is worth highlighting as product validation.

---

### Theme 4: Complex Cases Are a Margin and Time Problem Without a Tooling Solution
**Frequency**: Discussed extensively at the start of the interview (~10 minutes)
**Sentiment**: Matter-of-fact (accepted as reality) rather than frustrated
**Key Points**:
- Atypical cases (fraud, embezzlement, complex appeals) can take 12+ hours
- Templates and copy-paste are the current tool — but don't help when cases are structurally novel
- Lawyer doesn't explicitly ask for AI help here, but it is the obvious gap

**Analysis**: This insight was the opening topic of the interview, suggesting it is top-of-mind. The lawyer doesn't frame it as a product problem — it's framed as case reality. But from a product perspective, this is exactly where AI drafting assistance would have the highest ROI.

---

## User Journey & Pain Points

### Current Case Workflow (Andrés' Day)
```
1. Open case list → Sorted by deadline → Pain: New cases are at the bottom, easy to miss
2. Identify which cases need attention → Scroll through list → Pain: Disorganized; appointments not clearly tiered
3. Open case → Review AI summary → Pain: Full sentences slow down scanning
4. Work on case documents → Draft Replik or Berufungserwiderung → Pain: Complex cases take 6-12 hours; no AI drafting assistance
5. Upload court document / expert report → Pain: Must separately compose email to notify client (5-10 min extra)
6. Check "days since contact" hourglass → Pain: Shows 200 days for a case in "waiting" phase — creates noise
7. Set follow-up / deadline for next action → Works reasonably well (used actively)
8. New case assigned → Lands at bottom of list → Pain: Must scroll down to find it
```

### Pain Point Analysis

**Most Severe Pain Points** (Ranked):
1. **New Cases Not Discoverable at Top** - Severity: High
   - **Where It Happens**: Start of day / case list navigation
   - **Frequency**: Every time a new case is assigned
   - **Workaround**: Scroll to bottom of case list
   - **Cost**: Risk of missing new cases; cognitive friction
   - **Quote**: > "Da weiß ich, dass so die aktuelleren Fälle liegen hier unten."

2. **Document Upload ≠ Client Notification** - Severity: Medium-High
   - **Where It Happens**: After every significant case event requiring document sharing
   - **Frequency**: Multiple times per week per lawyer
   - **Workaround**: Compose separate email with Textbaustein
   - **Cost**: 5-10 minutes per occurrence

3. **Complex Case Drafting (Replik / Berufung)** - Severity: High (time cost)
   - **Where It Happens**: Legal writing / document drafting phase
   - **Frequency**: Every Replik; periodic for appellate cases
   - **Workaround**: Templates + heavy manual customization
   - **Cost**: 6-12 hours for complex appeals; 2-4 hours per Replik

4. **AI Summary Format (Full Sentences)** - Severity: Low-Medium
   - **Where It Happens**: Case overview / re-orientation
   - **Frequency**: Daily (reads regularly)
   - **Workaround**: Reads it anyway, slower than it could be
   - **Cost**: Minor time; reduced utility

5. **"Days Since Contact" Metric Is Noisy** - Severity: Medium
   - **Where It Happens**: Case list overview
   - **Frequency**: Ongoing for cases in "waiting" states
   - **Workaround**: Lawyer mentally filters it for appropriate cases
   - **Cost**: Alert fatigue; risk that real neglect cases are dismissed along with valid wait states

---

## Opportunity Space (Teresa Torres – Continuous Discovery Habits)

> Opportunities are unmet needs, pain points, and desires from the customer's perspective. They describe the customer's world — not solutions.

### Problems
*Things going wrong, frustrations, obstacles*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | New cases can't be found at a glance — must scroll to the bottom of the case list every time | > "Da weiß ich, dass so die aktuelleren Fälle liegen hier unten." | Opening the case list at the start of the day | Explicit | High |
| 2 | Uploading a document and notifying the client are two completely separate, disconnected manual steps | > "Einfach würde wieder 10 Minuten Zeit wegnehmen." | After uploading a court document or expert report | Explicit | Medium |
| 3 | The AI case summary is written in full prose sentences, which makes it slow to scan | > "Ich würde sie eben verkürzen auf Stichpunkte, also nicht als zusammenfassende Sätze." | Reviewing a case after not touching it for a while | Explicit | Low-Medium |
| 4 | The "days since contact" indicator fires for cases deliberately in a waiting phase — it creates noise, not signal | > "Grundsätzlich ist jetzt von Seiten des Mandanten nicht mehr das große Interesse da." | Scanning the case list for cases needing action | Implicit | Low-Medium |
| 5 | The case list sort doesn't reflect daily priority — appointments and deadline cases are mixed without a clear hierarchy | > "Ich finde es grundsätzlich irgendwie etwas unübersichtlich." | Daily case list navigation | Explicit | Medium |
| 6 | Complex and atypical cases (fraud allegations, appellate briefs, Replik) consume 6–12 hours with no tooling to help | > "Das war jetzt tatsächlich mal so ein Fall, wo ich jetzt wenig mit eigenen Vorlagen arbeiten konnte." | Legal drafting phase for complex or atypical cases | Implicit | High (time cost) |

### Needs
*Requirements and missing capabilities*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | Need to see newly assigned cases immediately without knowing to scroll to the bottom | > "Das ist so ein bisschen anders als früher im Legacy. Da waren die, glaube ich, sehr weit oben." | Start of day / case list review | Explicit | High |
| 2 | Need to send a document to the client directly after uploading it — one flow, not two | > "Wenn ich ein Dokument hochlade und vom System gefragt werde, soll das Dokument an den Mandanten versandt werden. Das fände ich eine tolle Optimierung." | Post-upload document sharing | Explicit | Medium |
| 3 | Need a way to signal that a case is "waiting" so the contact metric stops creating false alerts | No direct quote — inferred from the explanation of the 200-day no-contact case | Reviewing case health on the case list | Implicit | Medium |

### Desires
*Aspirational wants and unarticulated wishes*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | Wishes there was something to help draft the difficult parts of Replik and Berufungserwiderung — the abstract, novel cases that templates can't cover | > "Das war jetzt tatsächlich mal so ein Fall, wo ich jetzt wenig mit eigenen Vorlagen arbeiten konnte, weil das so ein bisschen abstrakt einfach war." | Complex legal document drafting | Implicit | High |
| 2 | Wants a case list view that automatically shows what actually matters that day — deadlines first, then appointments, then new, then waiting | > "Sortierung nach Fristen hat höchste Priorität, aber Termine sollten direkt darunter folgen." | Daily case planning | Explicit | Medium |

### Opportunity Hierarchy

**Navigating and understanding the case list takes unnecessary effort**
- **Type**: Problem / Need
- **Description**: The case list is the primary daily working view; its current structure forces lawyers to work against it
- **Child Opportunities**:
  - New cases are not visible at the top after assignment — (Problem)
  - Sort order doesn't reflect the lawyer's daily priority model — (Problem)
    - Appointments aren't clearly subordinated to deadlines — (Problem)
    - Cases without appointments aren't separated to the bottom — (Need)

**Document-related workflows are disconnected islands**
- **Type**: Problem / Need / Desire
- **Description**: Every document action exists in isolation — no downstream workflow connects upload to communication or drafting to AI assistance
- **Child Opportunities**:
  - Uploading a document doesn't offer to notify the client — (Problem / Need)
  - Complex legal document drafting (Replik, appellate briefs) has no tooling support — (Desire)

**Case health indicators create noise rather than signal**
- **Type**: Problem / Need
- **Description**: Metrics intended to flag neglected cases fire indiscriminately, eroding trust in the indicators
- **Child Opportunities**:
  - "Days since contact" fires for cases intentionally in a waiting phase — (Problem)
  - No way to mark a case as "Waiting on court / expert / counterparty" — (Need)

**AI tools are useful but not optimized for how lawyers consume them**
- **Type**: Problem / Desire
- **Description**: AI features exist and are actively used, but format and scope don't fully match the lawyer's workflow
- **Child Opportunities**:
  - Case summary format (full sentences) is slower to scan than bullet points — (Problem)
  - No AI drafting assistance for complex, template-resistant document types — (Desire)

---

## Jobs-to-be-Done Analysis

### Main Job(s)
**Primary Job**: Handle a portfolio of legal cases efficiently — prioritize correctly, produce high-quality legal work, keep clients informed, close cases at good margins
- **Functional Job**: Find the right cases to work on at the right time; produce legal documents accurately; communicate with clients and counterparties efficiently
- **Emotional Job**: Feel in control of the caseload; feel confident that nothing is falling through the cracks
- **Social Job**: Be seen as a competent, responsive lawyer by clients and the LH organization

**Supporting Quote**: > "Ja, und diese Replik, auch wenn ich jetzt mit Vorlagen arbeiten kann... Trotzdem würde ich jetzt schon pauschal sagen, dass jede Replik seine Zeit beansprucht."

### Job Performance
**Current Performance**: CaseForce handles tracking and communication adequately for standard cases. Navigation for complex caseloads (40+ cases) and the document→communication workflow are sub-optimal.
**Gaps**: New case discovery, document-communication integration, AI drafting for complex legal documents, contextual case health indicators
**Opportunities**: Make the AI summary the fastest possible case re-orientation tool; integrate document and email workflows; surface new cases prominently; eventually support complex document drafting with AI

---

## Feature Requests & Suggestions

### Explicit Requests
| Feature Request | Urgency | User Benefit | Effort | Priority |
|----------------|---------|--------------|--------|----------|
| New cases at top of case list | High | Eliminates scroll-to-bottom workaround; reduces case miss risk | Low-Medium | P0 |
| Document upload → "Send to client?" prompt | Medium | Saves 5-10 min per occurrence; reduces omission risk | Low | P1 |
| AI summary in bullet points | Medium | Faster scanning; higher daily utility | Very Low | P1 |
| Appointments directly below deadlines in sort | Low-Medium | Better case list structure for daily planning | Low-Medium | P1 |
| Cases without appointments at bottom | Low | Cleaner sort hierarchy | Low | P2 |

### Implicit Needs
**AI-Assisted Complex Document Drafting**
- **What They Said**: > "Das war jetzt tatsächlich mal so ein Fall, wo ich jetzt wenig mit eigenen Vorlagen arbeiten konnte."
- **What They Really Need**: Drafting assistance for atypical cases where templates don't apply — the job of understanding the other side's arguments and constructing a structured counter-response
- **Why**: These cases consume 3-5x the time of standard cases and represent the largest single time cost in the lawyer's workweek
- **Solution Ideas**: AI-powered Replik assistant that parses the Klageerwiderung and generates a draft response structure; integration with the NL team's ChatGPT workflow model

**Contextual Case Status / "Waiting" Flag**
- **What They Said**: Explained why 200 days no contact was appropriate for a specific case — but the system has no way to capture this
- **What They Really Need**: A way to mark a case as "awaiting [X]" so the contact-days indicator doesn't fire false alarms
- **Why**: Prevents alert fatigue; allows the metric to be meaningful when it matters
- **Solution Ideas**: "Waiting on court / counterparty / expert" status tag; or "Next expected event" date field that suppresses alerts

---

## Satisfaction & Sentiment Analysis

### Overall Sentiment
**Satisfaction Level**: Satisfied (constructive feedback, no major frustration)

**What's Working Well** ✅:
- Deadline-based sorting as primary sort: actively used and appreciated
- Follow-up and deadline features: mentioned as used daily to track case actions
- AI case summary: read regularly (strong adoption signal)
- AI proposed approach: > "Das finde ich gut mit dem vorgeschlagenen Vorgehen."
- Templates (Vorlagen) for standard cases: work well for typical employment law patterns

**What's Not Working** ❌:
- New case discoverability: > "Ich finde es grundsätzlich irgendwie etwas unübersichtlich."
- Document-to-client notification workflow: > "Einfach würde wieder 10 Minuten Zeit wegnehmen."
- AI summary format: > "Ich würde sie eben verkürzen auf Stichpunkte."
- Contact-days metric for waiting cases: creates noise without context

**Emotional Indicators**:
- **Frustration**: Low overall — Andrés is pragmatic and accepting of current limitations. The biggest frustration markers are around the case list structure and the document workflow.
- **Delight**: Positive about AI summary (reads it regularly) and the AI proposed approach section. The fact that a court expert report came back quickly was mentioned with genuine relief ("sogar überraschend schnell" — "even surprisingly quickly").
- **Confusion**: No significant confusion markers — Andrés is an experienced CaseForce user who knows the system's quirks.

---

## Competitive Insights

### Mentioned Competitors/Alternatives
**Legacy System (LH's previous tool)**
- **Usage**: Previous system before migration to CaseForce
- **Strengths**: New cases were surfaced at the top of the case list — behavior that was intuitive and preferred
- **Weaknesses**: Not mentioned (presumably less feature-rich overall)
- **Opportunity**: Restore new-case visibility behavior from the legacy system as a quick win that addresses a known regression

*(No external competitors or alternative tools were mentioned. Notably, unlike the NL team, no ChatGPT or external AI tool usage was mentioned.)*

---

## Prioritization Matrix

| Insight/Improvement | Impact | Frequency | Urgency | Feasibility | Alignment | Total Score | Priority |
|---------------------|--------|-----------|---------|-------------|-----------|-------------|----------|
| New cases at top of list | 4 | 5 | 4 | 4 | 4 | 21 | P0 |
| Document upload → send to client | 4 | 4 | 3 | 4 | 5 | 20 | P0 |
| AI drafting for Replik/Berufung | 5 | 3 | 3 | 2 | 5 | 18 | P1 |
| AI summary → bullet points | 3 | 5 | 2 | 5 | 4 | 19 | P1 |
| Case list sort hierarchy (Termine after Fristen) | 3 | 4 | 3 | 4 | 4 | 18 | P1 |
| Contextual "waiting" state (contact metric) | 3 | 3 | 2 | 3 | 4 | 15 | P1 |
| Cases without appointments at bottom | 2 | 3 | 2 | 4 | 3 | 14 | P2 |

---

## Recommended Actions

### Immediate (This Week)
1. **Update AI case summary prompt to output bullet points**
   - **Why**: High adoption already; format change makes it significantly more useful
   - **Owner**: Product / AI team
   - **Output**: Bullet-point format AI summary deployed and tested with 2-3 lawyers

### Short-term (Next 2-4 Weeks)
1. **Add new case surfacing to case list**
   - **Why**: New case discovery via "scroll to bottom" is a regression from legacy and creates SLA risk
   - **Owner**: Engineering (Frontend)
   - **Output**: New cases appear prominently — either as a dedicated top section, a "New" badge, or a sort option

2. **Implement "Send to client?" prompt after document upload**
   - **Why**: Saves 5-10 min per occurrence; reduces notification omissions
   - **Owner**: Engineering (Frontend)
   - **Output**: Post-upload modal with pre-populated email template and document attached

3. **Refine case list sort hierarchy**
   - **Why**: Appointments should be subordinated to deadlines but clearly follow them; terminal cases should sort last
   - **Owner**: Engineering (Frontend + Product design)
   - **Output**: Updated sort logic; validate with Andrés and 2 other lawyers before shipping

### Medium-term (This Quarter)
1. **Design "waiting state" for case health indicator**
   - **Why**: "Days since contact" metric creates noise for cases appropriately in waiting phases
   - **Owner**: Product
   - **Output**: Feature spec for contextual case status; validated with lawyer group

2. **Investigate AI-assisted Replik drafting**
   - **Why**: Highest time-cost document type in the German workflow; significant margin impact at scale
   - **Owner**: Product + AI team
   - **Output**: Feasibility assessment; scoping for AI Case Assist feature (aligned with NL ChatGPT workflow initiative)

---

## Follow-up & Next Steps

### Additional Research Needed
- [ ] Interview 2-3 additional DE lawyers to validate "new cases at top" sort preference
- [ ] Schedule a Replik-focused case walkthrough with Andrés to understand where exactly the time is spent
- [ ] Map client communication norms across case types and stages (when is "no contact" appropriate?)

### Validation Required
- [ ] Confirm that new-case-at-top behavior matches what other DE lawyers expect (not just Andrés)
- [ ] Test bullet-point AI summary format with lawyers before full rollout
- [ ] Validate document upload → notify workflow design with Andrés and one other lawyer

### Stakeholder Communication
- [ ] Share findings with: Engineering team, Product team
- [ ] Connect findings to Wiecher interview (NL) — several themes overlap: AI adoption, case list navigation, document workflow
- [ ] Create user stories for: new case surfacing, document upload prompt, AI summary format, sort hierarchy

---

## Raw Insights & Notable Quotes

### Memorable Quotes
> "Das war jetzt tatsächlich mal so ein Fall, wo ich jetzt wenig mit eigenen Vorlagen arbeiten konnte, weil das so ein bisschen abstrakt einfach war."
— Andrés, on why a complex fraud/embezzlement appeal took 12 hours

> "Wenn ich ein Dokument hochlade und vom System gefragt werde, soll das Dokument an den Mandanten versandt werden. Das fände ich eine tolle Optimierung."
— Andrés, proposing the document-upload integration feature himself

> "Ich schaue sie mir regelmäßig an, ich würde sie aber eben verkürzen auf Stichpunkte."
— Andrés, on the AI summary — active user, wants format improvement

> "Da weiß ich, dass so die aktuelleren Fälle liegen hier unten."
— Andrés, explaining how he finds new cases by scrolling to the bottom

### Additional Notes
- The interview was conducted in German. The lawyer is on the German team (Wiesbaden area), distinct from the Netherlands team (Wiecher interview, 2026-02-18). The two interviews together reveal overlapping themes: case list navigation issues, AI feature usage and format, and the universal desire for more integrated workflows.
- Unlike the NL team, Andrés did not mention any external AI tool usage (no ChatGPT workflow). This may mean the German lawyers haven't adopted it, are using it but it wasn't surfaced, or have different workflows. Worth validating.
- The 200-day no-contact case was an interesting test of the product team's assumption that all long gaps indicate neglect. The lawyer's explanation was clear and reasonable — the client had low interest and the case was in a well-defined waiting phase. The product team should be cautious about over-indexing the contact metric as a quality signal.
- The interview ran slightly over time, which is consistent with the previous Wiecher interview — lawyers have more to say once in a product conversation and are genuinely engaged. Consider scheduling 75-minute slots going forward.

---

## Appendix

### Interview Methodology
**Interview Type**: Semi-structured (case walkthrough + targeted questions)
**Duration**: ~45-50 minutes (over scheduled time)
**Format**: Remote video call with screen sharing
**Recording**: Yes (AI transcript generated)
**Language**: German (transcript in German)
**Attendees**: Andrés Jansen (lawyer), Kaan (Product), Manuel, Katharina (Product team)

### Related Documents
- [Interview Notion Page](https://www.notion.so/Feedback-LH-Jansen-30a5e8cace39804da4dfeaa9078c8f7e)
- [Previous Interview: Wiecher van Lingen (NL)](./2026-02-18-wiecher-van-lingen-nl-lawyer.md)

---

**Document Owner**: Product (Kaan)
**Last Updated**: 2026-02-24
**Next Review**: After Replik-focused follow-up session with Andrés
