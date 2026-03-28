# Solution Brainstorm: Lawyer Case Neglect -- AI-Native Round

**Date**: 2026-03-16 | **Constraints**: AI-native preferred. Quick to implement. Must complement the AI-prioritized to-do list initiative. Focus on outcomes: increase lawyer efficiency + reduce client complaints.

**Opportunity**: Lawyers managing high caseloads forget to take the next step on cases, leaving clients waiting without updates.
**Type**: Problem
**Evidence**:
- "Keine Rückmeldung" = 39 complaints in Q1 2026, #1 complaint driver
- Root cause: RSV compensation doesn't justify the time spent on routine communication
- Lawyers have no alerting, no context-switching support, and no way to batch routine actions

**Competitive Inspiration**: This brainstorm is informed by what's working at scale elsewhere in legal tech:
- **Lawhive** (7x revenue growth): AI paralegal "Lawrence" handles drafting, case management, intake end-to-end
- **Ironclad** ($3.2B): AI agents that autonomously execute multi-step workflows (Intake Agent, Review Agent, Drafting Agent)
- **Luminance**: "Institutional memory" -- platform retains decision-making history and learns from every interaction
- **EvenUp** ($2B, 10K cases/week): Data-driven case analysis at scale, comparable case matching
- **Darrow**: AI-powered pattern detection to find cases before humans do
- **Harvey** ($8-11B): Custom LLMs fine-tuned on firm-specific data; "AI as colleague, not tool"

**Key Insight from Competitors**: The market is moving from "AI as assistant" to "AI as autonomous agent." The winners aren't building better dashboards -- they're building AI that **does the work**. Legalhero's opportunity: don't just tell the lawyer which case needs attention (the to-do list). Have the AI **do the routine work** so the lawyer only handles what requires legal judgment.

---

## Solutions

| # | Title | Angle | Effort | Test Speed | AI-Native? |
|---|-------|-------|--------|------------|------------|
| 1 | AI Draft-and-Queue | Technology / AI | S-M | Fast | Yes |
| 2 | AI Case Narrator | Technology / AI | S | Fast | Yes |
| 3 | Smart Action Batching | Technology / AI | S | Fast | Yes |
| 4 | Predictive Complaint Risk Score | Data / AI | M | Fast | Yes |
| 5 | Voice-to-Update | Technology / AI | S-M | Fast | Yes |
| 6 | AI Auto-Responder for Clients | Technology / Process | S-M | Fast | Yes |

---

### 1. AI Draft-and-Queue

**Angle**: Technology / AI
**Inspired by**: Ironclad's AI Agents, Lawhive's "Lawrence," Harvey's "AI as colleague"

Every morning, the AI reviews all cases in a lawyer's portfolio, identifies cases that need a communication, and **pre-drafts the message** -- personalized with case-specific details (client name, case stage, last event, next expected step). These drafts queue up in an "Outbox" view. The lawyer's workflow becomes: open Outbox, scan 10 drafts, approve/edit/reject each one, done. 10 client updates in 5 minutes instead of 2 hours.

**Why it works**: The competitor insight is clear -- Lawhive's AI paralegal does exactly this and it drove 7x revenue growth. The bottleneck isn't knowing which case needs action (the to-do list solves that). The bottleneck is **producing the action**. Writing a personalized email to a client takes 10-15 minutes per case. If the AI drafts it and the lawyer just reviews, we cut that to 30 seconds per case. At 80 cases, that's the difference between "impossible" and "done before lunch."

This is fundamentally different from one-click templates (Solution 1 in the prior brainstorm): templates are generic ("Your case is being reviewed"). AI drafts are **case-specific** ("Dear Herr Meier, we received the response from your employer's legal team on March 10th. We are currently reviewing their position regarding your Kundigungsschutzklage and will prepare our response this week.").

**Riskiest assumption**: We believe that AI can generate case-specific client updates that are accurate enough for lawyers to approve with minimal editing. We'll know when >70% of AI drafts are sent with fewer than 2 edits.

**Cheapest test**: Use Claude API to generate draft updates for 30 real cases (feed it the case summary, timeline, and last 3 communications from CaseForce). Have the assigned lawyer review each draft: accurate? Would you send this? What would you change? -- 1 week -- Success: >60% of drafts rated "I'd send this as-is or with minor edits." Failure: lawyers say the drafts are too inaccurate, too generic, or miss critical legal nuance.

**Effort**: S-M (LLM integration, case context retrieval, outbox UI, approve/edit/send workflow)

---

### 2. AI Case Narrator

**Angle**: Technology / AI
**Inspired by**: Luminance's "Institutional Memory," Harvey's firm-specific learning

For every case, the AI maintains a living, plain-language **case narrative** -- a 3-5 sentence "story so far" that updates automatically as events happen. When a lawyer opens a case they haven't looked at in 2 weeks, instead of reading through 40 messages and 12 documents, they see:

> "Herr Schmidt filed a Kundigungsschutzklage on Jan 15. Coverage was confirmed by ARAG on Jan 22. You sent the claim letter to the employer on Feb 3. The employer's lawyer responded on Feb 28 rejecting the claim. **No action has been taken since. The client messaged on March 8 asking for an update.** Suggested next step: Review employer's response and advise client on options (Gutetermin is scheduled for April 2)."

**Why it works**: Context-switching is the invisible killer of lawyer productivity. A lawyer with 80 cases can't hold the state of each one in their head. Every time they switch to a case, they spend 5-10 minutes re-reading to remember where things stand. The AI Narrator eliminates this ramp-up time entirely. Combined with the to-do list ("act on this case") and Draft-and-Queue ("here's the message to send"), the Narrator completes the loop: "here's why this case needs attention, here's the context, here's the draft action."

Luminance proved this with contracts -- their platform retains negotiation history so lawyers never lose context. We're applying the same principle to cases.

**Riskiest assumption**: We believe that AI can generate accurate, useful case summaries from CaseForce data (messages, documents, status changes). We'll know when lawyers rate AI-generated narratives as 80%+ accurate in a blind review.

**Cheapest test**: Generate AI narratives for 20 cases using Claude (feed it the full case timeline from CaseForce). Show the narrative to the assigned lawyer alongside the actual case file. Ask: "Is this accurate? Is anything missing? Would this save you time?" -- 1 week -- Success: >80% accuracy rating; lawyers say "this would save me 5-10 minutes per case." Failure: narratives miss critical facts or misrepresent the case status.

**Effort**: S (LLM call with case data as context, display in case view -- no complex UI needed, just a text block)

---

### 3. Smart Action Batching

**Angle**: Technology / AI
**Inspired by**: Clio's workflow optimization, EvenUp's 10K cases/week throughput

The AI analyzes a lawyer's pending actions across all cases and groups them into **batching sessions** by action type:

> "You have 6 cases that need a client status update. Handle all 6 now? Estimated time: 8 minutes."
> "You have 3 cases where you need to review opposing party responses. Handle all 3 now? Estimated time: 25 minutes."
> "You have 2 cases that need document requests sent to clients. Handle both now? Estimated time: 4 minutes."

Each batch pre-loads the relevant cases in sequence with the AI draft ready for each one. The lawyer enters a focused "flow state" -- same type of action, repeated across cases, with AI pre-work done.

**Why it works**: EvenUp processes 10,000 cases per week not because each case gets individual attention, but because similar actions are **standardized and batched**. A lawyer who context-switches between "review a document," "write a client email," "check a court date," and "draft a claim letter" across 4 different cases burns enormous cognitive energy. Batching same-type actions eliminates this. Combined with AI Draft-and-Queue, this becomes: "Here are your 6 status update drafts -- review, approve, next, approve, next..." Assembly line efficiency for routine case work.

**Riskiest assumption**: We believe that lawyers will adopt a batching workflow (processing cases by action type) rather than their current habit of working case-by-case. We'll know when lawyers who use batching complete 2x more actions per hour than those who don't.

**Cheapest test**: For 5 lawyers, manually prepare a "batching sheet" each morning: group their pending actions by type, with case links. Send via Slack: "You have 5 status updates to send today -- here are the cases in order." Track whether they complete the batch and how long it takes vs. their normal pace. -- 2 weeks -- Success: lawyers complete batches faster than ad-hoc work; they ask for the list to continue. Failure: lawyers ignore the grouping and work case-by-case anyway.

**Effort**: S (action classification + grouping logic on top of the AI to-do list; the to-do list already knows which cases need action, this just groups them)

---

### 4. Predictive Complaint Risk Score

**Angle**: Data / AI
**Inspired by**: Darrow's AI pattern detection, EvenUp's settlement prediction models

Train a model on historical complaint data (228 Q1 complaints + historical data) to predict which active cases are most likely to generate a complaint in the next 7-14 days. The model uses signals: days since last lawyer activity, case type, client communication frequency, RSV partner, lawyer's historical complaint rate, case complexity, and whether the client has already reached out without response. Each case gets a **complaint risk score** (0-100). Cases above a threshold get flagged to both the lawyer and the PM.

This is fundamentally different from simple aging indicators (the prior brainstorm's Sol 6). Aging treats all cases the same: 10 days inactive = orange. Predictive scoring understands that a complex employment case from HUK with an unresponsive lawyer who already has 3 complaints is at 95% risk, while a simple traffic case with a responsive lawyer at 10 days is at 15% risk. The model learns which combinations predict complaints.

**Why it works**: Darrow proved that AI pattern detection can find legal issues before humans do (they're at $120M projected revenue from this approach). We're applying the same principle internally: find the complaints before they happen. The Q1 data (228 complaints with detailed attributes) is a strong training set. If the model can identify the top 20 highest-risk cases each week with >70% accuracy, PMs can intervene proactively instead of reactively.

**Riskiest assumption**: We believe that complaint risk can be predicted from case activity data with sufficient accuracy to be actionable. We'll know when the model correctly flags >70% of cases that actually generate complaints (recall) with a false positive rate below 3:1.

**Cheapest test**: Retrospective validation -- take the 228 Q1 complaints and the full universe of active cases during the same period. Build a simple logistic regression on: days inactive, case type, RSV partner, lawyer ID. Does it correctly identify the complaint cases? What's the precision/recall? -- 3-5 days (data analysis only, no engineering) -- Success: model achieves >70% recall with manageable false positive rate. Failure: complaint cases look statistically identical to non-complaint cases (no predictive signal).

**Effort**: M (model training, real-time scoring, integration with case views, PM alerting)

---

### 5. Voice-to-Update

**Angle**: Technology / AI
**Inspired by**: Harvey's "AI as colleague" philosophy, mobile-first legal workflows

Let lawyers record a 30-60 second voice note about a case, and AI converts it into a properly formatted, professional client update email. The lawyer dictates while commuting, between meetings, or walking to court: "Hey, I reviewed the employer's response on the Schmidt case. Their position is weak on the Kundigungsschutzklage -- they're claiming Betriebsbedingte Kundigung but haven't provided social selection criteria. I'll draft our Klageschrift response this week. Let the client know we're confident and will have next steps by Friday."

AI output (ready to send):

> "Sehr geehrter Herr Schmidt, wir haben die Stellungnahme Ihres Arbeitgebers eingehend geprüft. Wir sehen gute Ansatzpunkte fur Ihre Kundigungsschutzklage und werden in dieser Woche unsere Erwiderung vorbereiten. Sie konnen bis Freitag mit einer ausfuhrlichen Ruckmeldung zu den nachsten Schritten rechnen. Mit freundlichen Grüßen..."

**Why it works**: The insight from Harvey's positioning is that AI should feel like a colleague you talk to, not a form you fill out. Voice is the most natural communication medium -- lawyers spend all day talking (to clients, in court, on calls). Writing emails is the unnatural part. Voice-to-Update removes the "sit down and type" barrier entirely. A lawyer who wouldn't spend 10 minutes writing an email WILL spend 30 seconds dictating one between meetings. This is especially powerful for mobile -- lawyers are often not at their desk.

**Riskiest assumption**: We believe that lawyers will actually use voice input for case updates (it's not too awkward or inconvenient). We'll know when >40% of lawyers who have access to voice input use it at least once per week.

**Cheapest test**: Set up a simple WhatsApp or Telegram workflow: lawyer sends a voice note to a dedicated number, an ops team member (or Claude API) transcribes and reformats it into a professional email, sends it back for approval. Test with 5 lawyers for 2 weeks. -- 2 weeks -- Success: lawyers use it regularly; say it's faster than typing; clients receive well-formatted updates. Failure: lawyers feel awkward recording voice notes, or the transcription quality is too low for legal context.

**Effort**: S-M (speech-to-text API + LLM reformatting + simple approval flow; can start with WhatsApp integration)

---

### 6. AI Auto-Responder for Client Inquiries

**Angle**: Technology / Process
**Inspired by**: Lawhive's end-to-end AI, Anthropic's Claude Cowork for legal workflows

When a client sends a message asking for a status update (the most common client inquiry), the AI generates and sends an immediate, case-specific response -- without waiting for the lawyer. The AI reads the case file, constructs an accurate status update, and sends it within minutes. The lawyer is notified ("AI responded to Herr Schmidt's inquiry -- here's what was sent") and can follow up if needed.

**Scope is critical**: The AI only responds to **status inquiries** ("What's happening with my case?", "Any updates?", "When will I hear back?"). It does NOT respond to legal questions, strategy discussions, or anything requiring legal judgment. For those, it routes to the lawyer with a flag.

**Why it works**: Lawhive's entire model is built on AI handling routine client interactions at scale -- and it works (7x revenue growth, $35M+ ARR). The majority of client messages that trigger complaints aren't complex legal questions -- they're "hello, is anyone there?" Status inquiries are perfectly handleable by AI because the answer is factual (current case stage, last event, expected next step), not advisory.

This directly attacks the #1 complaint driver ("Keine Ruckmeldung"). The client gets an accurate, immediate response. The lawyer doesn't have to do anything. The complaint never happens.

**Riskiest assumption**: We believe that AI can correctly classify client messages as "status inquiry" vs. "requires lawyer attention" with >95% accuracy, and that clients will accept AI-generated responses positively. We'll know when clients who receive AI responses don't escalate to RSV at a higher rate than those who receive lawyer responses.

**Cheapest test**: Pull the last 50 client messages from cases that eventually generated complaints. Classify each: is this a status inquiry or a substantive question? For the status inquiries, generate an AI response using case data. Show the AI responses to 3 PMs: would this have satisfied the client? Would it have prevented the complaint? -- 3 days (classification) + 1 week (PM review) -- Success: >70% of messages are status inquiries; PM review confirms AI responses would have prevented escalation in most cases. Failure: most messages require substantive lawyer input; or AI responses are too inaccurate to trust.

**Effort**: S-M (message classification model, case context retrieval, auto-response generation, lawyer notification, client channel integration)

**Three-sided market note**: This is the highest-impact solution for clients (immediate response) and RSVs (complaint prevention). Lawyers benefit too (less routine communication burden). Risk: lawyers may feel the AI is "stepping on their toes" or worry about accuracy. Mitigation: always notify the lawyer what was sent; make it easy to correct or follow up; start with a very conservative scope (status inquiries only).

---

## Comparison

| Dimension | Sol 1: Draft-Queue | Sol 2: Narrator | Sol 3: Batching | Sol 4: Risk Score | Sol 5: Voice | Sol 6: Auto-Respond |
|-----------|-------------------|----------------|----------------|-------------------|-------------|-------------------|
| **Mechanism** | AI writes, lawyer approves | AI summarizes case context | AI groups similar actions | AI predicts complaints | AI converts voice to email | AI responds to clients directly |
| **Lawyer efficiency** | High | High | High | Medium | High | Very High |
| **Complaint reduction** | High | Medium | Medium | Very High | High | Very High |
| **AI depth** | Deep (generates text) | Medium (summarizes) | Light (classifies/groups) | Deep (ML prediction) | Deep (speech + generation) | Deep (classification + generation) |
| **Risk** | Low (lawyer reviews) | Low (read-only) | Low (suggestion only) | Medium (model accuracy) | Low (lawyer approves) | Medium (AI acts autonomously) |
| **Effort** | S-M | S | S | M | S-M | S-M |
| **Test speed** | 1 week | 1 week | 2 weeks | 3-5 days (data) | 2 weeks | 1-2 weeks |

---

## Recommended Stack

These solutions form a **layered AI system**, not alternatives. They should be built in sequence, each layer adding more AI autonomy:

**Layer 1 -- Context** (ship first, prerequisite for everything else):
- **Sol 2: AI Case Narrator** -- gives the lawyer instant case context. Simplest to build (one LLM call per case). Unlocks value for every other solution.

**Layer 2 -- Efficiency** (ship next, makes lawyer workflow 5x faster):
- **Sol 1: AI Draft-and-Queue** -- AI writes, lawyer reviews. The single highest-impact solution for both efficiency and complaint reduction.
- **Sol 3: Smart Batching** -- groups similar drafts for flow-state processing. Natural extension of Sol 1.

**Layer 3 -- Prevention** (ship in parallel, catches what Layers 1-2 miss):
- **Sol 4: Predictive Risk Score** -- identifies which cases will become complaints. Start with the retrospective data analysis (3-5 days) to validate feasibility.
- **Sol 6: AI Auto-Responder** -- handles the simplest client inquiries without lawyer involvement. Highest autonomy, highest impact, but needs the most careful scoping.

**Layer 4 -- Accessibility** (ship anytime, independent):
- **Sol 5: Voice-to-Update** -- alternative input channel for lawyers who are mobile or prefer dictating. Can be built and tested independently.

**First test to run**: Sol 2 (AI Narrator) -- generate narratives for 20 cases using Claude, show to lawyers, validate accuracy. This is a 1-week test that costs almost nothing and validates whether the AI can understand case context well enough to power all the other solutions.

---

## How This Connects to the Existing AI To-Do List Initiative

The AI to-do list answers: **"Which case needs attention?"**

This brainstorm's solutions answer:
- **Sol 2 (Narrator)**: "Here's what's happening in that case" (context)
- **Sol 1 (Draft-Queue)**: "Here's the message to send" (action)
- **Sol 3 (Batching)**: "Here are all similar actions to do at once" (efficiency)
- **Sol 4 (Risk Score)**: "This case is about to become a complaint" (urgency)
- **Sol 5 (Voice)**: "Dictate the update instead of typing" (accessibility)
- **Sol 6 (Auto-Responder)**: "The AI already handled it" (autonomy)

Together, they form a progression from **"AI tells lawyer what to do"** to **"AI does the routine work itself."** This mirrors the industry trend (Ironclad, Lawhive, Harvey) from AI assistants to AI agents.

---

## Overlaps with Previous Brainstorms

**`lawyer-case-neglect-solutions-2026-03-16.md`** (same-day, prior round):
- Sol 1 (One-Click Status Updates) -- **Superseded** by Sol 1 here (AI Draft-Queue). Templates are generic; AI drafts are case-specific. Draft-Queue is the AI-native evolution.
- Sol 4 (Automated Client Pings) -- **Related** to Sol 6 here (AI Auto-Responder). Pings are proactive and generic; Auto-Responder is reactive and case-specific. Complementary.
- Sol 5 (Quick-Reply Buttons) -- **Complementary** with Sol 1 here. Quick-Reply Buttons are manual triggers; Draft-Queue is proactive (AI drafts before the lawyer asks).
- Sol 6 (Aging Colors) -- **Superseded** by Sol 4 here (Predictive Risk Score). Colors are static rules; Risk Score is ML-powered prediction.

**`lawyer-case-neglect-solutions-2026-03-10.md`**:
- Sol A (Friction-Free Next Action) -- **Evolutionary overlap** with Sol 1 (Draft-Queue). Same philosophy (reduce friction), but Sol 1 uses AI to generate the message instead of templates.

**`complaint-reduction-brainstorm-2026-03-06.md`**:
- Stalled Case Detection Engine -- **Complementary** with Sol 4 (Risk Score). Detection Engine uses rules; Risk Score uses ML prediction. Risk Score is the AI-native evolution.

---

## References

- **Jira**: PD-46, PD-9, PD-25, PD-38, PD-90
- **Competitive Intelligence**: `.claude/product/competition/landscape-2026-02-27.md`
- **Prior brainstorms**: `lawyer-case-neglect-solutions-2026-03-10.md`, `lawyer-case-neglect-solutions-2026-03-16.md`, `complaint-reduction-brainstorm-2026-03-06.md`
- **Opportunity data**: `complaint-opportunities-q1-2026.md`
- **Strategy**: Pillar 2 (AI-Powered Automation), Pillar 3 (Process Standardization)

**Saved to**: `.claude/product/discovery/solutions/lawyer-case-neglect-ai-solutions-2026-03-16.md`
