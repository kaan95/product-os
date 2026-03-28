# Interview Synthesis - Wiecher van Lingen (NL Lawyer)

**Interview Date**: 2026-02-18
**Interview Type**: Internal User (Lawyer using CaseForce)
**Synthesized**: 2026-02-23
**Synthesized By**: Claude (Product Interview Synthesis)

---

## Executive Summary

Wiecher van Lingen is a lawyer on the Legalhero Netherlands team who handles termination cases (and starting the following week, VSO/sick leave cases) exclusively with ARAG as the insurance partner. The interview was a screen-sharing session where Wiecher walked the product and engineering team through daily frustrations and feature gaps in CaseForce.

The session surfaced two major categories of findings: **tactical blockers** (file format support, email feature gaps, case organization) that create daily friction and compliance risks; and a **strategic discovery** — the team has independently built a sophisticated ChatGPT Enterprise workflow that cuts case handling time nearly in half (from 4 hours to ~2 hours). The product team was previously unaware of the depth of this AI usage.

The top three critical findings are: (1) inability to open .doc/.docx/.eml/.msg files forces lawyers to use external tools, creating compliance risks; (2) the Netherlands team shares a single email address, which is already painful and becomes a GDPR violation risk with the imminent start of sensitive VSO cases; and (3) lawyers have self-built an AI-assisted workflow that CaseForce should absorb natively to unlock team-wide productivity gains. Immediate action is required on items 1 and 2 before VSO cases begin next week.

---

## Interview Context

**Interviewee**: Wiecher van Lingen
**Company/Segment**: Legalhero Netherlands team
**Use Case**: Daily case management — reviewing documents, drafting emails, client communication, legal analysis
**Current Solution**: CaseForce + ChatGPT Enterprise (self-built parallel workflow)
**Interview Focus**: Product feedback session — bugs, wishes, workflow walkthrough

---

## Key Insights

### 🎯 Top Insights (Prioritized)

#### 1. Unsupported File Formats Block Core Document Workflows — Priority: 🔴 Critical

**What We Learned**:
CaseForce cannot open .doc, .docx, .eml, and .msg files inline. Since ARAG (the sole NL insurance partner) frequently sends .eml and .msg files, lawyers must download files, open them in a free online MSG reader or convert via Google Drive, then re-upload as PDFs. This happens on every case, every day.

**Evidence from Interview**:
> "So what I have to do in order to read it, I have to go on the internet, use this free MSG reader. Download the file here. And then I can finally see the email. As you can imagine, that's very cumbersome."

> "I have to download it and then open it in Google Drive. Then convert it into a PDF, upload it again here, and then I can finally view it in CaseForce, which is also very time consuming."

> "From a compliance perspective, it's also important that this is addressed so that we do not miss any important documents."

**Why This Matters**:
Every case is affected. The workaround adds minutes per file, and uploading case documents to a free public online tool creates real compliance and data security exposure. ARAG files frequently contain sensitive personal and legal data.

**Root Cause**:
CaseForce's document viewer only supports a limited set of file types (likely PDF and images). No embeddable .doc/.eml viewer has been integrated. ARAG uses Outlook-native formats (.msg, .eml) that are not common in the German market but are standard in the NL workflow.

**Recommended Action**:
- [ ] Investigate embeddable document viewer libraries that support .doc/.docx (e.g., Microsoft Office Online embed, LibreOffice Online, or similar)
- [ ] Investigate .eml and .msg rendering (e.g., `msgreader` JS library or backend parsing to HTML)
- [ ] Also explore requesting ARAG NL to switch to PDF attachments as a parallel track

**Impact if Addressed**: Eliminates a daily compliance risk and saves multiple minutes per case across all NL lawyers.
**Effort Estimate**: Medium
**Priority Score**: 23/25

---

#### 2. Shared Email Account Creates Compliance Risk and Imminent GDPR Violation — Priority: 🔴 Critical

**What We Learned**:
All NL lawyers share a single inbox (`service-nl@legalhero.io`). Lawyers must manually scan the shared inbox to identify which emails belong to them. Starting next week, the team will handle VSO (sick leave/sickness) cases, where Dutch law explicitly requires minimizing colleague access to each other's case data. The shared inbox directly violates this requirement.

**Evidence from Interview**:
> "We strongly need a personal email account for each individual. At the moment we all use service.nlaccount.io. And this means that you always have to check this general email box to see whether emails are addressed to you."

> "Under Dutch law it must be prevented that colleagues have access — excessive access to each other's cases, especially because next week we will start working with sickness cases and there are strong GDPR privacy rules for those cases."

> "And especially once we have more team members, this will become unworkable."

**Why This Matters**:
VSO cases start next week. Operating with a shared inbox for sick leave cases is a potential GDPR/Dutch law violation. This is a hard compliance deadline, not a UX preference.

**Root Cause**:
Individual email provisioning was not set up when the NL team was established. The shared inbox was a shortcut that is now a blocker for legal compliance.

**Recommended Action**:
- [ ] Immediately provision individual email addresses for each NL lawyer (e.g., `firstname.lastname@legalhero.io`)
- [ ] Configure CaseForce to associate incoming emails with individual lawyer accounts
- [ ] Keep `service-nl@legalhero.io` active during transition to avoid missing emails in flight
- [ ] Ensure case-level email isolation so lawyers cannot see each other's case emails

**Impact if Addressed**: Unblocks VSO case handling, eliminates GDPR risk, reduces daily inbox-checking overhead.
**Effort Estimate**: Medium (email provisioning + routing config)
**Priority Score**: 24/25

---

#### 3. Lawyers Have Independently Built a Powerful AI Workflow — CaseForce Should Absorb It — Priority: 🟡 High

**What We Learned**:
One NL lawyer has built a comprehensive ChatGPT Enterprise workflow that the whole team uses. At case start, they upload all CaseForce documents to a ChatGPT project with custom per-case-type prompts. The AI then generates: full case summary, employer/employee details, contract analysis, social plan review, transition payment calculations, a client advice email, and a draft email to the employer. Follow-up prompts are made via voice recording. This can reduce a typical 4-hour case to 2 hours.

**Evidence from Interview**:
> "For every type of case, we have our own folder project. So I have for every different project, I have a different prompt... And this is all GDPR-proof, right? So this is the enterprise version."

> "When the case has been started, I upload all the files from CaseForce into ChatGPT. And then what we do is we ask — it gives automatically all the information we need about the case. A summary, information about the employer and employee, name, everything. It goes into the agreement, sums up all the important things."

> "Sometimes this whole process only takes me 10 minutes. Which leads to sometimes us dealing the whole case in like two hours."

> "I think it will be interesting to do this in a very synchronous way, because you already thought of this workflow... our idea is that we integrate this into CaseForce so that every lawyer can benefit from this and you don't need to move around."

**Why This Matters**:
This is the most significant strategic discovery of the session. The team has validated an AI case-handling model in production that cuts time-on-case by up to 50%. They've done the prompt engineering and UX design work themselves. Integrating this natively in CaseForce would: (a) bring the productivity gain to all lawyers, not just the NL team; (b) eliminate the GDPR risk of uploading sensitive case files to ChatGPT; (c) unlock CaseForce's strategic positioning as an AI-augmented legal operating system.

**Root Cause**:
CaseForce's existing AI features (case summary) are visible but shallow. The lawyers' job-to-be-done (process case efficiently from intake to resolution) isn't fully served, so they built external tooling.

**Recommended Action**:
- [ ] Schedule a dedicated follow-up session in early March (already agreed with Wiecher) to deep-dive the workflow and prompt structure
- [ ] Map the full ChatGPT workflow to CaseForce feature equivalents
- [ ] Design an integrated "AI Case Assist" feature that pulls case files natively and runs structured analysis per case type
- [ ] Identify which case types and sub-tasks to target first (restructuring / termination as the validated starting point)

**Impact if Addressed**: Potentially 2x lawyer throughput across the platform; major competitive differentiator; eliminates shadow AI tool usage and its associated compliance risks.
**Effort Estimate**: High
**Priority Score**: 20/25

---

#### 4. Email Drafts Are Not Accessible Within Case View — Priority: 🟡 High

**What We Learned**:
Drafts exist in the system (under "Concepten" in the general inbox) but are shared across all team members and disconnected from case context. Lawyers cannot save a draft mid-email and return to it within a case. The workaround is opening CaseForce in multiple tabs simultaneously.

**Evidence from Interview**:
> "If you have written an email and want to continue working on it later, you cannot save it. As a result, it regularly happens that you accidentally close the screen and you lose your entire email."

> "What I do now is that I often open CaseForce in a second tab. So I open one here and then I can draft an email in this one, open another one here, which enables me to work in CaseForce while simultaneously drafting an email."

**Why This Matters**:
Case-contextual drafts are table stakes for an email tool embedded in a case management system. Shared drafts are a UX failure that creates confusion and shows gaps in case isolation.

**Root Cause**:
The draft feature was implemented at the mailbox level rather than the case level, resulting in shared state.

**Recommended Action**:
- [ ] Implement per-case email drafts (not mailbox-level)
- [ ] Ensure drafts are scoped to the individual lawyer, not shared
- [ ] Auto-save draft on navigation away from compose view

**Impact if Addressed**: Eliminates lost-email risk; reduces multi-tab workaround; improves email composing experience.
**Effort Estimate**: Low-Medium
**Priority Score**: 18/25

---

#### 5. Multiple Email Feature Gaps Accumulate Friction — Priority: 🟡 High

**What We Learned**:
Several standard email client features are missing: Reply to All, forwarding a single email without the entire thread, marking emails as unread, and scheduled sending.

**Evidence from Interview**:
> "Alles beantwoorden — reply to all. So here I have two email addresses I would like to reply to them both. It doesn't work."

> "Sometimes I receive an email from the employer or the lawyer and I want to forward it to my client without including the underlying email thread. That is currently not possible. So what I have to do now is copy and paste the text and put it into a new email. It happens two, three times a week."

> "If I want to check [an email] and I see, oh, this is not mine, this belongs to Maartje's case. But then I cannot change the status into unread."

> "Sometimes in my practice I'm drafting an email in the evening or in the weekend and then I want to send it on Monday morning first thing. And then there's no possibility to use the button."

**Why This Matters**:
Each of these is a small but daily friction point. Collectively they signal that the email component of CaseForce has not been built to production-grade standards for a legal professional's workflow. "Reply to all" and "forward single email" are the highest-frequency pain points.

**Recommended Action**:
- [ ] Implement "Reply to all" (straightforward email feature)
- [ ] Enable forwarding a single email within a thread (not the whole chain)
- [ ] Add "Mark as unread" on email items
- [ ] Add scheduled email sending (send later functionality)

**Impact if Addressed**: Removes several daily workflow friction points; signals product maturity to legal professionals.
**Effort Estimate**: Low-Medium per feature
**Priority Score**: 17/25

---

#### 6. Case List Cannot Be Sorted or Filtered by Case Type — Priority: 🟡 High

**What We Learned**:
With 40+ cases, the inability to sort cases alphabetically by client name makes navigation cumbersome. More urgently, as the NL team expands to VSO/sickness cases alongside termination cases, there is no visible way to separate them. (A legal field filter may exist but is not discoverable or well-understood.)

**Evidence from Interview**:
> "It would be very helpful if we could sort and organize by client name. When I have 40 cases, I have to search."

> "Starting next week, we will also work with sickness cases. It will be very inconvenient if this is all being mixed up. I would just like to have the option to separate them or to look for them."

**Why This Matters**:
Case discoverability scales poorly without sort/filter. The case type separation is time-sensitive given the VSO expansion next week.

**Recommended Action**:
- [ ] Add column sorting to the case list (client name alphabetically, at minimum)
- [ ] Verify and validate the legal field filter works for NL case types (VSO vs. termination)
- [ ] Communicate to the NL team that the search functionality and legal field filter already exist
- [ ] Consider making sort/filter controls more visually prominent

**Impact if Addressed**: Reduces navigation time as caseload scales; enables case type separation ahead of VSO launch.
**Effort Estimate**: Low (if filter exists; mostly discoverability and validation)
**Priority Score**: 17/25

---

#### 7. AI Case Summary UX — Should Be Collapsed by Default — Priority: 🟢 Medium

**What We Learned**:
The AI case summary is expanded by default every time a case is opened. Lawyers collapse it as the first action every time, as it takes up significant screen space and is not always needed.

**Evidence from Interview**:
> "Every time I'm opening a case, what I'm doing is this [collapses it]. I know. And it would be more logical if it's defaulted — like this [collapsed]."

**Recommended Action**:
- [ ] Change the AI case summary to collapsed by default (or remember user's last state)

**Impact if Addressed**: Small but consistent UX improvement for every case opened.
**Effort Estimate**: Low
**Priority Score**: 14/25

---

#### 8. Feature Announcements Are Not Reaching the NL Team — Priority: 🟢 Medium

**What We Learned**:
New features appear in CaseForce without any communication, introduction, or training for the Netherlands team. This means lawyers are missing functionality that already exists (e.g., email delivery tracking indicators, search, legal field filter).

**Evidence from Interview**:
> "For us in the Netherlands, there is no introduction from you. Like, hey, this is what we did, please let us know. It's just there from one day to another."

> "I have to be honest, lucky for us we have Lucas, who — when you guys have made some adjustments — there is no introduction."

**Why This Matters**:
This session revealed that Wiecher was unaware of multiple existing features (email status indicators, search, draft location). This is a communication/enablement gap, not a product gap. Fixing it costs little and recovers value from already-shipped work.

**Recommended Action**:
- [ ] Establish a lightweight product update communication channel for the NL team (Slack, in-app, or email digest)
- [ ] Provide feature walkthroughs when releasing new capabilities to NL (short Loom or written summary)
- [ ] Consider an in-app "What's new" notification

**Impact if Addressed**: Increases adoption of existing features; reduces support overhead; builds team trust.
**Effort Estimate**: Low
**Priority Score**: 13/25

---

## Improvement Areas by Category

### 🔴 Critical Issues (Must Address)

**Unsupported File Formats (.doc, .docx, .eml, .msg)**
- **Problem**: Files sent by ARAG (primary NL insurer) cannot be viewed inline in CaseForce
- **User Impact**: Lawyers must leave the platform, use external tools, and re-upload files — daily friction with compliance risk
- **Quote**: > "From a compliance perspective, it's also important that this is addressed so that we do not miss any important documents."
- **Recommendation**: Integrate embeddable document/email viewer; explore server-side conversion to HTML/PDF
- **Timeline**: Next 2 Weeks
- **Owner**: Engineering (Frontend + Backend)

**Shared Email Address vs. GDPR Requirement for VSO Cases**
- **Problem**: All NL lawyers share one inbox; VSO (sick leave) cases require individual email isolation by Dutch law
- **User Impact**: Lawyers manually triage shared inbox daily; GDPR violation risk starting next week
- **Quote**: > "Under Dutch law it must be prevented that colleagues have access — excessive access to each other's cases, especially because next week we will start working with sickness cases."
- **Recommendation**: Provision personal email accounts per lawyer immediately; configure routing accordingly
- **Timeline**: Immediate (before VSO cases begin)
- **Owner**: Ops / Engineering

---

### 🟡 High-Value Opportunities

**Native AI Case Assist (CaseForce-Integrated ChatGPT Workflow)**
- **Opportunity**: Absorb the externally-built ChatGPT workflow into CaseForce natively
- **Business Impact**: Up to 2x lawyer throughput; eliminates shadow tool compliance risk; key strategic differentiator
- **User Benefit**: Lawyers get AI-powered case analysis, draft emails, and calculations without leaving CaseForce
- **Quote**: > "Our idea is that we integrate this into CaseForce so that every lawyer can benefit from this and you don't need to move around."
- **Recommendation**: Deep-dive session in March to map the workflow; design integrated "AI Case Assist" feature per case type
- **Timeline**: This Quarter (design) → Next Quarter (build)
- **Effort vs. Impact**: High effort / Very high impact

**Case-Level Email Drafts**
- **Opportunity**: Move drafts from shared mailbox to case-contextual, per-lawyer drafts
- **Business Impact**: Eliminates lost emails; reduces multi-tab workaround
- **User Benefit**: Lawyers can draft and return to emails safely within case context
- **Timeline**: Next Sprint
- **Effort vs. Impact**: Medium effort / High impact

---

### 🟢 Quick Wins

**Reply to All**
- **What**: Implement Reply to All in the email compose view
- **Why**: Currently requires manual CC addition — adds friction to every multi-party email
- **Effort**: Low
- **Impact**: Medium
- **Timeline**: Next Sprint

**Mark Email as Unread**
- **What**: Add "mark as unread" action to email items
- **Why**: Accidentally opening an email removes unread state; lawyers currently text colleagues to notify them
- **Effort**: Low
- **Impact**: Medium
- **Timeline**: Next Sprint

**AI Case Summary: Collapsed by Default**
- **What**: Change AI summary display to collapsed on case open
- **Why**: Lawyers collapse it as their first action every time
- **Effort**: Very Low
- **Impact**: Low-Medium (daily UX improvement)
- **Timeline**: This Sprint

**Forward Single Email Without Thread**
- **What**: Allow forwarding a single email from within a thread, excluding previous messages
- **Why**: Happens 2-3 times per week; current workaround is copy-paste into new email
- **Effort**: Low-Medium
- **Impact**: Medium
- **Timeline**: Next Sprint

**Case List Sorting by Client Name**
- **What**: Add sortable columns to case list (at minimum: client name A-Z)
- **Why**: With 40+ cases, manual scanning is impractical
- **Effort**: Low
- **Impact**: Medium
- **Timeline**: Next Sprint

---

### 🔵 Long-term Enhancements

**Document Section Organization**
- **Vision**: Structured, filterable document section with clear naming, categorization, and context
- **Strategic Value**: As case complexity grows and document volume increases, navigation degrades rapidly
- **User Need**: > "Documents are messy. Too many." Uses favorites as a workaround.
- **Timeline**: 3-6 months
- **Dependencies**: Define document taxonomy; potentially different per case type

**In-App Feature Announcement System**
- **Vision**: In-app "What's New" or changelog visible to users on login or via notification
- **Strategic Value**: Ensures feature adoption; reduces communication debt with remote teams
- **Timeline**: 3-6 months
- **Dependencies**: Feature release process, content authorship workflow

---

### ❓ Research Questions

**How universal is the ChatGPT workflow across the NL team?**
- **What We Don't Know**: Is it used by all NL lawyers or only the one who built it? What is the prompt quality and consistency?
- **Why It Matters**: Determines the baseline to design against when integrating into CaseForce
- **How to Answer**: Follow-up session in March; ask to see the prompts and workflow directly
- **Next Step**: Schedule deep-dive with Wiecher in early March

**Does ARAG NL have flexibility on file formats?**
- **What We Don't Know**: Whether ARAG can be asked to switch to PDF instead of .eml/.msg
- **Why It Matters**: A format change from ARAG would eliminate the rendering problem entirely
- **How to Answer**: Ask Lucas or the NL team lead to raise with the ARAG account contact
- **Next Step**: Assign to NL team to check with ARAG

**What is the full case type taxonomy for the NL market?**
- **What We Don't Know**: Full range of case types the NL team will handle; how they map to German taxonomy
- **Why It Matters**: Needed to design AI case type prompts, filters, and routing
- **How to Answer**: Interview Lucas and the NL team; review ARAG contract scope
- **Next Step**: Product to document NL case types in a brief

---

## Themes & Patterns

### Theme 1: Platform as a Bottleneck to Efficiency
**Frequency**: Referenced throughout (~15 distinct examples)
**Sentiment**: Frustrated but constructive
**Key Points**:
- Multiple daily workarounds (external tools, multiple tabs, copy-paste)
- Workarounds are consistent and repeatable, meaning the pain is structural
- Despite workarounds, Wiecher is productive and engaged with CaseForce
**Representative Quotes**:
> "That's very cumbersome."
> "That's a pain in the ass that we constantly have to go through all these emails."
**Analysis**: Wiecher is a power user who has adapted well, but the cumulative weight of workarounds signals that CaseForce is being used despite its email and document handling, not because of it. The email module in particular has significant gaps relative to standard professional email tools.

---

### Theme 2: AI Adoption Is Already Happening Outside CaseForce
**Frequency**: Mentioned in depth for ~10 minutes of the interview
**Sentiment**: Very positive (about ChatGPT), constructive (wants it in CaseForce)
**Key Points**:
- Team built a self-service AI workflow independently
- It is genuinely reducing case handling time
- The team is asking for it to be integrated natively
- Voice prompting is already part of the workflow
**Representative Quotes**:
> "Sometimes this whole process only takes me 10 minutes. Which leads to sometimes us dealing the whole case in like two hours."
> "Our idea is that we integrate this into CaseForce so that every lawyer can benefit from this."
**Analysis**: This is the most strategically significant discovery of the session. Lawyers are not waiting for the product team to deliver AI — they are building it themselves. The product team's opportunity is to absorb this validated workflow before external shadow tool usage becomes entrenched.

---

### Theme 3: Feature Blindness Due to Lack of Communication
**Frequency**: 3 explicit examples in the session
**Sentiment**: Mildly frustrated
**Key Points**:
- Email delivery status indicators (delivered, opened) exist but Wiecher wasn't aware
- Search functionality exists but not widely used
- Legal field filter exists but not discoverable/understood
- Features shipped without NL-team communication
**Representative Quotes**:
> "For us in the Netherlands, there is no introduction from you. It's just there from one day to another."
**Analysis**: There is a non-trivial gap between what CaseForce can do and what the NL team knows it can do. This is a communication and onboarding problem that is eroding the perceived value of shipped work.

---

### Theme 4: Compliance Pressures Are Accelerating Infrastructure Needs
**Frequency**: Referenced ~5 times
**Sentiment**: Serious / urgent
**Key Points**:
- VSO cases require strict GDPR compliance starting immediately
- Shared email inbox is a direct compliance risk
- Using external tools (free MSG reader, Google Drive) for case files is also a compliance risk
- Dutch law specifically governs colleague access to case data
**Analysis**: Compliance is not a future concern — it is a live constraint with a deadline. The product team needs to treat the personal email provisioning and file handling gaps as compliance blockers, not just UX improvements.

---

## User Journey & Pain Points

### Current Case Workflow (Wiecher's Day)
```
1. Start of day: Check shared inbox (service-nl@legalhero.io) → Pain: Manual triage, risk of missing emails
2. Open case → AI summary is expanded → Pain: Manually collapse every time
3. Review case documents → Some files are .doc/.eml/.msg → Pain: Download, use external tool, re-upload
4. Gather context for email draft → Search through previous emails manually → Pain: Time-consuming
5. Draft email → No case-level draft feature → Pain: Multi-tab workaround; risk of losing draft
6. Send email to multiple parties → No Reply to All → Pain: Manual CC/BCC
7. Need to forward single email → Must copy-paste into new compose → Pain: Happens 2-3x/week
8. Email accidentally opened → Cannot mark unread → Pain: Text colleague to notify
9. Parallel workflow in ChatGPT → Upload all case files → Run structured prompts → Pain: Outside CaseForce, GDPR risk
10. End of case: Write advice email → Use ChatGPT-generated draft as base → Refine and send
```

### Pain Point Analysis

**Most Severe Pain Points** (Ranked):
1. **Unsupported File Formats** - Severity: High
   - **Where It Happens**: Document review in every case
   - **Frequency**: Daily, multiple times
   - **Workaround**: Free online MSG reader / Google Drive conversion
   - **Cost**: 5-15 min per file; compliance exposure
   - **Quote**: > "On a daily basis, it takes a lot of time."

2. **Shared Email Inbox** - Severity: High (Compliance Critical)
   - **Where It Happens**: Start of day / email monitoring
   - **Frequency**: Continuously throughout the day
   - **Workaround**: Manual scanning of shared inbox
   - **Cost**: Ongoing overhead; GDPR risk for VSO cases
   - **Quote**: > "You always have to check this general email box to see whether emails are addressed to you."

3. **No Case-Level Email Drafts** - Severity: Medium-High
   - **Where It Happens**: Email composition
   - **Frequency**: Every email that takes more than one sitting
   - **Workaround**: Multiple CaseForce tabs open simultaneously
   - **Cost**: Cognitive overhead; risk of draft loss

4. **Forward Single Email Without Thread** - Severity: Medium
   - **Where It Happens**: Email thread management
   - **Frequency**: 2-3 times per week
   - **Workaround**: Copy-paste text into new email
   - **Cost**: ~5 min per occurrence

5. **No Reply to All** - Severity: Medium
   - **Where It Happens**: Multi-party email replies
   - **Frequency**: Regularly
   - **Workaround**: Reply to one, manually add CC
   - **Cost**: Time; risk of missing a recipient

---

## Opportunity Space (Teresa Torres – Continuous Discovery Habits)

> Opportunities are unmet needs, pain points, and desires from the customer's perspective. They describe the customer's world — not solutions.

### Problems
*Things going wrong, frustrations, obstacles*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | .doc, .docx, .eml, and .msg files can't be viewed in CaseForce — lawyers must use external tools and re-upload | > "I have to go on the internet, use this free MSG reader... As you can imagine, that's very cumbersome." | Document review in every case, every day | Explicit | High |
| 2 | All NL lawyers share a single inbox — manually scanning for emails addressed to you is daily overhead and a GDPR risk | > "You always have to check this general email box to see whether emails are addressed to you." | Start of day and ongoing email monitoring | Explicit | High (Compliance) |
| 3 | Email drafts are shared across all team members and disconnected from case context — closing the screen loses the draft | > "You accidentally close the screen and you lose your entire email." | Drafting complex client communications | Explicit | High |
| 4 | Reply to All doesn't work — must add recipients manually every time | > "Alles beantwoorden — reply to all. Here I have two email addresses I would like to reply to them both. It doesn't work." | Multi-party email communication | Explicit | Medium |
| 5 | Forwarding a single email without the full thread history is not possible | > "I want to forward it to my client without including the underlying email thread. That is currently not possible." | Email thread management | Explicit | Medium |
| 6 | An email accidentally opened cannot be marked as unread | > "Then I cannot change the status into unread." | Inbox triage in shared inbox | Explicit | Medium |
| 7 | The AI case summary is expanded by default — collapsing it is the first action every single time a case is opened | > "Every time I'm opening a case, what I'm doing is this [collapses it]. I know." | Opening any case | Explicit | Low |
| 8 | New features appear in CaseForce without any communication or introduction for the NL team | > "For us in the Netherlands, there is no introduction from you. It's just there from one day to another." | Discovering new functionality | Explicit | Low-Medium |
| 9 | The document section becomes disorganized and hard to navigate as case complexity and document count grow | > "Documents are messy. Too many." | Reviewing documents in a complex case | Explicit | Medium |
| 10 | The AI workflow that cuts case time in half runs outside CaseForce — requires manual file upload and creates GDPR risk | > "I upload all the files from CaseForce into ChatGPT." | Case intake and analysis at case start | Explicit | High |

### Needs
*Requirements and missing capabilities*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | Need to view .eml and .msg files from ARAG inline, without leaving CaseForce | > "From a compliance perspective, it's also important that this is addressed so that we do not miss any important documents." | Daily document review | Explicit | High |
| 2 | Need personal email addresses per lawyer to isolate case communications and comply with Dutch GDPR law for VSO cases | > "Under Dutch law it must be prevented that colleagues have access — excessive access to each other's cases, especially because next week we will start working with sickness cases." | All email workflows; critical for VSO cases starting next week | Explicit | Critical |
| 3 | Need to save email drafts at the case level and come back to them safely | > "If you have written an email and want to continue working on it later, you cannot save it." | Drafting emails across multiple sittings | Explicit | High |
| 4 | Need standard email client features that are currently absent: Reply to All, single-email forwarding, mark as unread, scheduled sending | Multiple quotes above | Daily email workflows | Explicit | Medium |
| 5 | Need to sort and filter cases by case type so termination and VSO cases don't mix in the same list | > "Starting next week, we will also work with sickness cases. It will be very inconvenient if this is all being mixed up." | Managing a 40+ case portfolio across types | Explicit | High |
| 6 | Need to know when new features are released — currently discovering them by accident, or not at all | > "For us in the Netherlands, there is no introduction from you." | Using the product day-to-day | Explicit | Medium |

### Desires
*Aspirational wants and unarticulated wishes*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | Wants the ChatGPT AI case analysis workflow absorbed natively into CaseForce — same power, no file upload, no platform switching | > "Our idea is that we integrate this into CaseForce so that every lawyer can benefit from this and you don't need to move around." | Case intake, analysis, and drafting across all case types | Explicit | Very High |
| 2 | Wants to interact with the AI by voice within CaseForce — currently does this via ChatGPT for follow-up prompts | Implicit — inferred from description of the ChatGPT voice recording workflow | AI-assisted case analysis during active work | Implicit | Medium |
| 3 | Wishes the document section were clean, organized, and filterable so it stays navigable as cases grow | > "Documents are messy. Too many. All these icons." | Document review and navigation | Explicit | Medium |
| 4 | Wishes emails could be scheduled to send at a chosen time | > "Sometimes I'm drafting an email in the evening or in the weekend and then I want to send it on Monday morning first thing. And then there's no possibility." | Client and employer communication outside business hours | Explicit | Low-Medium |

### Opportunity Hierarchy

**CaseForce email doesn't meet professional legal workflow standards**
- **Type**: Problem / Need
- **Description**: The email module was built at a basic level; it lacks table-stakes features that lawyers expect from any professional email tool
- **Child Opportunities**:
  - Missing standard email client features — (Problem / Need)
    - No Reply to All — (Problem)
    - Cannot forward a single email without the full thread — (Problem)
    - Cannot mark an email as unread — (Problem)
    - No scheduled sending — (Desire)
  - Drafts are shared mailbox-level, not case-level or per-lawyer — (Problem / Need)
  - All lawyers share a single inbox — (Problem / Need)
    - GDPR violation risk for VSO cases starting next week — (Problem — Compliance)
    - Daily manual inbox triage overhead — (Problem)

**Core case documents cannot be opened inside the platform**
- **Type**: Problem / Need
- **Description**: A significant portion of ARAG's case materials arrive in formats CaseForce can't render, breaking the platform as the single source of truth
- **Child Opportunities**:
  - .eml and .msg files from ARAG require an external tool to view — (Problem / Need)
  - .doc and .docx files require manual conversion before viewing — (Problem)
  - Document section becomes unnavigable as case complexity grows — (Problem / Desire)

**AI-powered case work is already happening — outside CaseForce**
- **Type**: Problem / Desire
- **Description**: The team independently built a workflow that cuts case handling time in half; CaseForce is being bypassed for the highest-value part of the lawyer's job
- **Child Opportunities**:
  - ChatGPT workflow reduces case time from 4h to 2h but requires leaving CaseForce — (Problem)
    - Manual file upload from CaseForce to ChatGPT adds friction and GDPR risk — (Problem)
  - Lawyers want the AI workflow integrated natively in CaseForce — (Desire)
    - Voice-prompted AI interactions — (Desire)

**The NL team doesn't know what CaseForce can already do**
- **Type**: Problem / Need
- **Description**: Shipped features are going undiscovered because there is no communication channel between the product team and the NL team
- **Child Opportunities**:
  - No feature release communication for the NL team — (Problem / Need)
  - Existing features (email tracking, search, legal field filter) are unknown to active users — (Problem)

---

## Jobs-to-be-Done Analysis

### Main Job(s)
**Primary Job**: Handle legal cases efficiently from intake to resolution — review documents, analyze legal situation, communicate with all parties, track progress
- **Functional Job**: Process a case (understand context, draft communications, track actions) with maximum accuracy and minimum time
- **Emotional Job**: Feel confident that nothing is missed; feel in control of a complex multi-party situation
- **Social Job**: Be seen as a reliable, professional lawyer by clients and counterparts

**Supporting Quote**: > "In general, my general time spent on cases is like four hours. So this is for me a long case."

### Job Performance
**Current Performance**: CaseForce handles case tracking and communication adequately, but document handling and email capabilities fall below the bar of professional email tools lawyers are used to.
**Gaps**: Document rendering, email feature parity, AI-assisted drafting, case discoverability at scale
**Opportunities**: Integrate AI workflow natively; achieve email feature parity; fix document rendering; improve case organization at scale (40+ cases)

---

## Feature Requests & Suggestions

### Explicit Requests
| Feature Request | Urgency | User Benefit | Effort | Priority |
|----------------|---------|--------------|--------|----------|
| .doc/.docx/.eml/.msg file viewer | High | Eliminates daily external tool workaround; compliance safety | Medium | P0 |
| Personal email per lawyer | High (compliance deadline) | GDPR compliance; reduces inbox noise | Medium | P0 |
| Case-level email drafts | High | Prevents draft loss; removes multi-tab workaround | Medium | P1 |
| Reply to All | Medium | Email feature parity | Low | P1 |
| Forward single email (no thread) | Medium | Saves 5 min, 2-3x/week | Low | P1 |
| Sort cases by client name | Medium | Faster navigation with 40+ cases | Low | P1 |
| Mark email as unread | Low-Medium | Avoid texting colleagues to re-flag emails | Low | P1 |
| Scheduled email sending | Low | Send in-progress drafts at the right time | Low | P2 |
| AI case summary collapsed by default | Low | Minor UX improvement, saves 1 click per case | Very Low | P2 |
| Native AI Case Assist (ChatGPT integration) | Strategic | 2x throughput potential | High | P1 (strategic) |

### Implicit Needs
**Document Organization at Scale**
- **What They Said**: > "This is also a bit of a pain in the ass. All these icons."
- **What They Really Need**: A document section that remains navigable as case complexity and document count grows
- **Why**: Currently relies on "Favorites" as a workaround; with .doc/.msg support added, the problem will grow
- **Solution Ideas**: Auto-categorize documents by type; surfacing recently added docs; document search within case

**Better AI Integration — Right Place, Right Time**
- **What They Said**: Built elaborate ChatGPT workflow with custom prompts
- **What They Really Need**: AI that understands case context and can generate drafts within CaseForce without file upload overhead
- **Why**: The current flow requires leaving CaseForce and manually uploading files — friction that grows every time a new document arrives
- **Solution Ideas**: CaseForce-native "AI Draft" that reads case files directly; contextual prompts per case type

---

## Satisfaction & Sentiment Analysis

### Overall Sentiment
**Satisfaction Level**: Satisfied (with clear, specific frustrations)

**What's Working Well** ✅:
- Deadline and follow-up tracking: > "That's a good way to work with."
- Email delivery status (delivered / opened): > "This is nice to know." (once discovered)
- Favorites for documents: > "That really works."
- Notification highlighting for active cases: Core workflow tool used daily
- Async email sending fix (recently shipped): > "That actually by chance happened just 10 minutes ago." (positive)

**What's Not Working** ❌:
- File format support: > "That's very cumbersome."
- Shared inbox: > "It's time consuming, and there's also a risk in there."
- No case-level drafts: > "You accidentally close the screen and you lose your entire email."
- Missing email features (reply all, forward, mark unread): Multiple quotes above

**Emotional Indicators**:
- **Frustration**: File formats, shared inbox, email feature gaps
- **Delight**: AI case summary (conceptually); email delivery tracking once discovered; ChatGPT workflow
- **Curiosity**: Open to feedback on AI integration roadmap; engaged and collaborative in tone
- **Urgency**: Noticeably more serious when discussing GDPR/compliance implications

---

## Competitive Insights

### Mentioned Competitors/Alternatives
**ChatGPT Enterprise**
- **Usage**: Daily, for all case types — document analysis, email drafting, calculations, client advice
- **Strengths**: Custom prompts per case type; voice recording for follow-up prompts; handles full document sets; dramatically reduces case handling time
- **Weaknesses**: Requires manual file upload from CaseForce; operates outside CaseForce context; GDPR concerns for sensitive case data
- **Opportunity**: CaseForce should absorb this workflow natively, providing the AI capabilities with the security and context advantages that an integrated tool can offer

**Free Online MSG Viewer / Google Drive**
- **Usage**: Daily for opening .eml/.msg files and .doc/.docx files
- **Strengths**: Works
- **Weaknesses**: External, potentially non-GDPR-compliant; cumbersome
- **Opportunity**: Native support in CaseForce eliminates this entirely

---

## Prioritization Matrix

| Insight/Improvement | Impact | Frequency | Urgency | Feasibility | Alignment | Total Score | Priority |
|---------------------|--------|-----------|---------|-------------|-----------|-------------|----------|
| Personal email per lawyer (GDPR) | 5 | 5 | 5 | 4 | 5 | 24 | P0 |
| File format support (.doc/.eml/.msg) | 5 | 5 | 5 | 3 | 5 | 23 | P0 |
| Native AI Case Assist | 5 | 4 | 3 | 2 | 5 | 19 | P1 |
| Case-level email drafts | 4 | 4 | 4 | 4 | 4 | 20 | P1 |
| Reply to All | 3 | 4 | 3 | 5 | 4 | 19 | P1 |
| Forward single email | 3 | 3 | 3 | 4 | 4 | 17 | P1 |
| Case list sorting (client name) | 3 | 4 | 3 | 5 | 4 | 19 | P1 |
| Mark email as unread | 2 | 3 | 2 | 5 | 4 | 16 | P1 |
| Feature announcement process | 3 | 5 | 2 | 5 | 4 | 19 | P1 |
| AI summary collapsed by default | 2 | 5 | 2 | 5 | 4 | 18 | P1 |
| Scheduled email sending | 2 | 2 | 2 | 3 | 3 | 12 | P2 |
| Document section organization | 3 | 3 | 2 | 2 | 4 | 14 | P2 |

---

## Recommended Actions

### Immediate (This Week)
1. **Provision personal email addresses for NL lawyers**
   - **Why**: VSO cases start next week; shared inbox is a GDPR compliance risk
   - **Owner**: Ops + Engineering
   - **Output**: Each NL lawyer has firstname.lastname@legalhero.io routing into CaseForce

2. **Investigate file format rendering solution**
   - **Why**: Daily compliance and efficiency blocker; embeddable viewer likely exists
   - **Owner**: Engineering (Rizilda/Kashan per meeting)
   - **Output**: Technical spike with recommended library and implementation plan

3. **Communicate existing features to NL team**
   - **Why**: Email delivery tracking, search, and legal field filter are unknown to team
   - **Owner**: Product (Kaan)
   - **Output**: Short written summary or Loom video shared with NL team

### Short-term (Next 2-4 Weeks)
1. **Implement case-level email drafts**
   - **Why**: High-frequency pain; unblocks multi-tab workaround
   - **Owner**: Engineering (Frontend)
   - **Output**: Drafts scoped to case and individual lawyer in CaseForce

2. **Implement Reply to All + Forward Single Email**
   - **Why**: Email feature parity; straightforward to implement
   - **Owner**: Engineering (Frontend)
   - **Output**: Reply-all button; option to forward without thread history

3. **Implement Mark as Unread + AI Summary collapsed by default**
   - **Why**: Quick wins; minimal effort; improve daily UX
   - **Owner**: Engineering (Frontend)
   - **Output**: Mark as unread action; AI summary defaults to collapsed state

4. **Validate and communicate legal field filter for NL case types**
   - **Why**: VSO/termination separation is needed; filter may already exist
   - **Owner**: Product + Engineering
   - **Output**: Confirmed working filter for NL; communicated to Wiecher and Lucas

### Medium-term (This Quarter)
1. **Schedule AI workflow deep-dive with Wiecher (early March)**
   - **Why**: Foundation for native AI Case Assist feature design
   - **Owner**: Kaan (agreed in meeting)
   - **Output**: Documented prompt structure, workflow map, and feature spec draft

2. **Design Native AI Case Assist feature**
   - **Why**: Biggest long-term opportunity for lawyer throughput
   - **Owner**: Product
   - **Output**: Feature spec for AI Case Assist integrated with CaseForce case context

3. **Establish feature announcement process for NL team**
   - **Why**: Feature blindness is eroding perceived value of shipped work
   - **Owner**: Product (Kaan)
   - **Output**: Lightweight release communication channel (Slack/email) + process

---

## Follow-up & Next Steps

### Additional Research Needed
- [ ] Deep-dive session with Wiecher in early March on ChatGPT workflow and prompt engineering
- [ ] Ask Lucas / NL team lead whether ARAG can switch to PDF format for file attachments
- [ ] Document full NL case type taxonomy (termination, VSO, sickness, other) for AI prompt design

### Validation Required
- [ ] Confirm legal field filter works correctly for VSO vs. termination (test with NL team)
- [ ] Confirm that case-level email drafts can be scoped without touching shared mailbox state
- [ ] Validate that individual email routing can be set up before next week's VSO case start

### Stakeholder Communication
- [ ] Share findings with: Engineering (Rizilda, Kashan), Product team, NL team lead (Lucas)
- [ ] Schedule follow-up discussion: AI integration approach (early March, agreed with Wiecher)
- [ ] Create user stories for: File format support, personal email accounts, case-level drafts, email feature parity

---

## Raw Insights & Notable Quotes

### Memorable Quotes
> "In general, my general time spent on cases is like four hours. So this is for me a long case."
— Wiecher, contextualizing case complexity

> "Sometimes this whole process only takes me 10 minutes. Which leads to sometimes us dealing the whole case in like two hours."
— Wiecher, on the ChatGPT workflow impact

> "Under Dutch law it must be prevented that colleagues have access — excessive access to each other's cases, especially because next week we will start working with sickness cases and there are strong GDPR privacy rules for those cases."
— Wiecher, on compliance urgency

> "Lucky for us we have Lucas, who — when you guys have made some adjustments — there is no introduction from you. It's just there from one day to another."
— Wiecher, on feature communication gap

> "Our idea is that we integrate this into CaseForce so that every lawyer can benefit from this and you don't need to move around."
— Wiecher, explicitly requesting native AI integration

### Additional Notes
- The NL team works exclusively with ARAG — unlike Germany where multiple insurers are present. This creates unique file format dependencies (ARAG sends .eml/.msg) that may not exist in DE.
- Wiecher uses the ChatGPT voice recording feature for follow-up prompts — an interaction pattern worth noting for future CaseForce AI UX design.
- The session ran over time but Wiecher continued to contribute additional items even at the end — high engagement and motivation to improve the product.
- Lucas is mentioned several times as the person who manages case creation and is the NL team's informal product liaison. He should be included in follow-up communications.

---

## Appendix

### Interview Methodology
**Interview Type**: Semi-structured (screen-sharing walkthrough with Q&A)
**Duration**: ~60 minutes (over scheduled time)
**Format**: Remote video call
**Recording**: Yes (AI transcript generated)
**Attendees**: Wiecher van Lingen (NL lawyer), Kaan (Product), Rizilda (Frontend Engineer), Kashan (Backend/Fullstack Engineer), + others

### Related Documents
- [Interview Notion Page](https://www.notion.so/Wiecher-x-Product-30b5e8cace3980549a2bf1f4b7e7e017)

---

**Document Owner**: Product (Kaan)
**Last Updated**: 2026-02-23
**Next Review**: After early March follow-up session on AI integration
