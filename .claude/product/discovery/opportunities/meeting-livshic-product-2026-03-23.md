# Opportunities: Meeting with Partner Lawyer Daniel Livshic

**Source**: 1:1 product discovery session with Daniel Livshic (partner lawyer, high performer on platform)
**Source Date**: 2026-03-23
**Source Author**: Livshic x Product (Kaan)
**Stakeholder Perspective**: lawyer
**Extracted**: 2026-03-23
**Total Opportunities**: 13

---

## Opportunity Summary

| # | Opportunity | Type | Pain | Reach | Frequency | Score | Parent |
|---|------------|------|------|-------|-----------|-------|--------|
| 1 | Lawyers can't maintain awareness of case context while working in the document editor | Problem | High | Broad | Constant | 27 | — |
| 1.1 | Deadline (Fristen) view is blocked when a document is open — 4-step context switch required | Problem | Medium | Broad | Constant | 18 | 1 |
| 1.2 | Favorites navigation bar disappears when PDFs are open | Problem | Low | Broad | Constant | 9 | 1 |
| 1.3 | Call notes cannot be taken in parallel while a document is open | Problem | Medium | Significant | Regular | 8 | 1 |
| 2 | Case takeover workflow doesn't ensure timely first client contact | Problem | High | Broad | Constant | 27 | — |
| 2.1 | No automated first-contact message is triggered when a lawyer takes a new case | Need | High | Broad | Constant | 27 | 2 |
| 2.2 | Cases without deadlines sink to the bottom of the list and are consistently forgotten | Problem | High | Broad | Regular | 18 | 2 |
| 3 | Mixed and conflicting data at case intake causes lawyer confusion and rework | Problem | Medium | Broad | Regular | 12 | — |
| 3.1 | Internal phone team notes are visually indistinguishable from client-provided information in the Fallgarten | Problem | Medium | Broad | Regular | 12 | 3 |
| 3.2 | Case intake fields and documents frequently contain conflicting data requiring manual reconciliation | Problem | Medium | Significant | Regular | 8 | 3 |
| 4 | Lawsuit (Klageschrift) creation involves preventable manual steps | Problem | Medium | Broad | Regular | 12 | — |
| 4.1 | Court addresses must be manually looked up in an external Justice Portal before filing | Problem | Low | Broad | Regular | 6 | 4 |
| 4.2 | File names must be manually renamed (spaces → underscores) before uploading to BEA | Problem | Low | Broad | Constant | 9 | 4 |
| 5 | AI-generated first letters are more detailed than lawyers' preferred efficient first-contact style | Problem | Medium | Significant | Regular | 8 | — |
| 6 | Tasks tab (Aufgaben) is systematically deprioritized — lawyers only review it after all case work is done | Problem | Low | Significant | Regular | 4 | — |
| 7 | Clients with non-German backgrounds need phone-first communication but the platform is email-optimized | Need | Medium | Significant | Regular | 8 | — |
| 8 | PDF document viewer rotation is unpredictable for multi-page documents | Problem | Low | Significant | Regular | 4 | — |

---

## Opportunity Tree

```
Lawyers can't maintain context awareness while editing documents [Score: 27]
  ├── Deadline view is blocked when a document is open (4-step context switch) [Score: 18]
  ├── Favorites bar disappears behind open PDFs [Score: 9]
  └── Call notes can't be created in parallel with open documents [Score: 8]

Case takeover workflow doesn't ensure timely first client contact [Score: 27]
  ├── No automated first-contact message is triggered at case takeover [Score: 27]
  └── Cases without deadlines sink to the bottom of the list and are forgotten [Score: 18]

Mixed and conflicting data at case intake causes confusion and rework [Score: 12]
  ├── Phone team notes are indistinguishable from client notes in Fallgarten [Score: 12]
  └── Intake fields and documents contain conflicting data requiring manual reconciliation [Score: 8]

Lawsuit creation involves preventable manual steps [Score: 12]
  ├── Court addresses must be manually looked up in external Justice Portal [Score: 6]
  └── File names must be manually renamed for BEA upload [Score: 9]

AI-generated first letters are too detailed for lawyers' efficient first-contact style [Score: 8]

Tasks tab is systematically deprioritized by lawyers [Score: 4]

Clients with non-German backgrounds need phone-first communication [Score: 8]

PDF rotation is unpredictable for multi-page documents [Score: 4]
```

---

## Detailed Opportunities

### Parent 1: Lawyers Can't Maintain Context Awareness While Editing Documents

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: When a lawyer opens a document to write (e.g., a Vollmacht or Forderungsschreiben), the case context — deadlines, notes, case history — becomes inaccessible. The lawyer must close the document, look up the information, memorize it, and re-open the document. This creates a multi-step context switch that breaks focus and risks errors.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High | Causes errors (wrong dates), breaks concentration, and creates a disjointed workflow. Livshic described up to 4 steps just to check a single deadline while writing. |
| Reach | Broad | Every lawyer who writes documents on the platform is affected. Document editing is a core daily workflow for all partner lawyers. |
| Frequency | Constant | Happens every time a lawyer writes a document and needs to reference case data. |
| **Score** | **27** | |

**Supporting Evidence**:
> "Ich schreibe jetzt hier irgendein Dokument [...] dann muss ich es zumachen, dann suche ich die Frist raus, dann muss ich mir das merken. Wenn man unkonzentriert ist, dann habe ich die Uhrzeit vergessen. Ja, dann gehe ich wieder zurück ins Dokument..."
> — Daniel Livshic, transcript

> "Also du bist quasi bei vier Schritten."
> — Daniel Livshic summarizing the context-switch friction

**Where it occurs**: Document editor, whenever writing Vollmachten, Forderungsschreiben, or any document that requires referencing case dates/facts
**Current workaround**: Memorizing information before opening the document; switching back and forth manually
**Strategic relevance**: Directly undermines Pillar 2 (AI-Powered Automation) and Pillar 3 (Process Standardization). Lawyer efficiency is a core platform quality metric.

---

#### Child 1.1: Deadline (Fristen) View Is Blocked When a Document Is Open

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: When a lawyer opens the document editor to write or edit a document, the Fristen (deadlines) view in the sidebar is blocked or covered. The lawyer must close the document to see the deadline, memorize it, and return to the document — a process that takes 4 navigation steps and is error-prone.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Risk of using wrong dates in legal documents; interrupts deep work; forces repeated context switching |
| Reach | Broad | Affects all lawyers writing documents that reference dates (Vollmachten, Forderungsschreiben, Klagen, etc.) |
| Frequency | Constant | Occurs every time a date or deadline needs to be referenced while writing |
| **Score** | **18** | |

**Supporting Evidence**:
> "Wenn ich jetzt hier irgendein Dokument schreibe [...] Ich habe keine Möglichkeit quasi aus dem Dokument irgendwie nochmal diese Frist hier zu sehen."
> — Daniel Livshic, transcript

**Proposed solution (from user)**: A collapsible right-side panel showing Fristen while in the document editor
**Where it occurs**: Document editor, throughout the document writing workflow

---

#### Child 1.2: Favorites Navigation Bar Disappears When PDFs Are Open

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: The pinned favorites bar at the top of the interface disappears when PDFs are viewed, forcing lawyers to navigate differently depending on whether a PDF is open or not.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Low | Minor inconvenience, but adds navigation friction during a workflow that's already interrupted by PDF viewing |
| Reach | Broad | Affects all lawyers who view PDFs while navigating (standard workflow) |
| Frequency | Constant | Happens every time a PDF is opened |
| **Score** | **9** | |

**Supporting Evidence**:
> "Diese Leiste hier oben mit diesen Favoriten — ob man die nicht vielleicht wie diese Startleiste bei Windows oben fixieren könnte, dass sie immer da ist. Das heißt, egal was ich für PDFs aufhabe, dass ich quasi das hier oben noch hätte."
> — Daniel Livshic, transcript

---

#### Child 1.3: Call Notes Cannot Be Created in Parallel With Open Documents

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: When a lawyer is actively working in a document and receives or makes a call (via R-Call), they cannot simultaneously write a call note. The document must be closed first, then the call note is created, then the document must be re-opened. This breaks the flow of parallel phone + document work.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Forces a context break during a call where the lawyer is simultaneously reviewing a document. Risks losing the call context or the document progress. |
| Reach | Significant | Affects lawyers who receive calls from clients while working in documents — a common pattern for active lawyers handling complex cases |
| Frequency | Regular | Multiple times per week for active lawyers |
| **Score** | **8** | |

**Supporting Evidence**:
> "Ich schreibe was, mich ruft mein Band an und wir besprechen den Text zusammen und ich arbeite direkt im Text, während wir telefonieren, will aber gleichzeitig eine Anrufnotiz machen. Kann ich nicht, weil ich dann die Datei zumachen muss."
> — Daniel Livshic, transcript

---

### Parent 2: Case Takeover Workflow Doesn't Ensure Timely First Client Contact

**Type**: Problem
**Stakeholder**: Partner lawyer + Client
**Description**: When a lawyer pulls a new case (Pfeil ziehen), no systematic process ensures the client is contacted promptly. Lawyers who don't immediately set a deadline on the case risk losing it at the bottom of their list. This results in an average first contact time of 125 hours — with some cases going weeks without any contact.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High | Livshic's own average first contact is 125h. Clients feel ignored, satisfaction drops, and lawyers' performance metrics worsen. One case was not touched since January. |
| Reach | Broad | Affects all lawyers and all cases taken. Livshic himself identified this and built a manual workaround (always setting a deadline to "tomorrow" immediately after pulling a case). |
| Frequency | Constant | Happens at every case takeover. |
| **Score** | **27** | |

**Supporting Evidence**:
> "Die sind da unten dann hängen geblieben und dann, ich komm hier hin und manchmal ist es halt echt viel und dann arbeitest du die Liste runter und dann ist es 19 Uhr und dann guckst du einfach nicht mehr nach ganz unten."
> — Daniel Livshic, transcript

> "Ich habe jetzt angefangen, direkt wenn ich einen Fall übernehme, seit letztem Monat mache ich das, dem eine Frist zu geben, morgen, damit es in dieser Fristenliste auftaucht."
> — Daniel Livshic describing his workaround

**Data point**: Avg. first contact time: 125 hours. Distribution: 91 cases <1h, 177 cases same day, but multiple outliers >3 days.
**Strategic relevance**: Directly maps to Pillar 3 (Process Standardization) — SLA enforcement for first contact <24h. Critical for client satisfaction and lawyer performance metrics.

---

#### Child 2.1: No Automated First-Contact Message Is Triggered at Case Takeover

**Need**: Need
**Stakeholder**: Partner lawyer + Client
**Description**: When a lawyer pulls a case, the platform does not automatically send a first-contact email to the client or set a reminder for the lawyer. The lawyer must manually compose the first email and set a deadline. This creates friction and inconsistency — some lawyers do it immediately, others delay, and some forget.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High | No first contact = clients waiting days without acknowledgment. Livshic explicitly validated a product idea to auto-send a first-contact email with auto-reminder on case takeover. |
| Reach | Broad | All lawyers on all cases. Currently the only systematic workaround is the one Livshic invented himself (manual deadline on "tomorrow"). |
| Frequency | Constant | Every case takeover |
| **Score** | **27** | |

**Supporting Evidence**:
> "Wir hatten jetzt die Idee, dass wir sagen, wir generieren schon mal eine E-Mail vor, wo einfach nur drinsteht, 'hallo, ich bin der und der, ich übernehme jetzt Ihren Fall'. Siehst du da dann irgendwelche Probleme? [...] Ich glaube, die E-Mail schadet überhaupt nicht."
> — Livshic validating the product idea, transcript

> "Und dann könnten wir dir immer eine Option geben, dir eine Wiedervorlage oder eine Frist [...] zu setzen. Dann vergisst du das auch nicht."
> — Product team explaining the planned feature, transcript

**Current workaround**: Livshic manually sets every new case deadline to "tomorrow" immediately after pulling it — since ~1 month ago
**Proposed solution**: Auto-generate first contact email at case takeover + auto-set follow-up in 2-3 days

---

#### Child 2.2: Cases Without Deadlines Sink to the Bottom of the List and Are Systematically Forgotten

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: The case list is sorted by deadline/Frist. Cases without a deadline appear at the bottom and are not surfaced unless the lawyer explicitly scrolls down. In high-volume periods, these cases are consistently overlooked — a pattern Livshic confirmed with a concrete example of a case taken in January that had no activity since.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High | Concrete case: a case pulled in January sat untouched until discovered in this session. Client dissatisfaction, performance metric degradation, and operational risk. |
| Reach | Broad | Affects all lawyers. The issue is structural — deadline-less cases are invisible by design. |
| Frequency | Regular | Happens whenever a lawyer takes a case and doesn't immediately set a deadline (common under high workload). |
| **Score** | **18** | |

**Supporting Evidence**:
> "Genau der zum Beispiel — den hattest du übernommen im Januar und da ist quasi nichts passiert."
> — Product team showing Livshic a forgotten case, transcript

> "Die sind da unten dann hängen geblieben [...] und dann ist es 19 Uhr und dann guckst du einfach nicht mehr nach ganz unten."
> — Livshic describing the pattern, transcript

---

### Parent 3: Mixed and Conflicting Data at Case Intake Causes Lawyer Confusion and Rework

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: When a lawyer reviews a newly taken case, they encounter two data quality issues: (1) internal phone team notes appear alongside client-provided information without visual distinction, and (2) key data fields (e.g., vacation days) differ between the intake form and attached documents. Both force lawyers to stop, investigate, and verify before proceeding.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Causes rework (contacting clients for clarification), risk of acting on wrong data, and slows the case takeover workflow |
| Reach | Broad | Affects all lawyers reviewing newly taken cases — standard part of the case takeover workflow |
| Frequency | Regular | Observed in the live session with a specific case (10 vs. 22 Urlaubstage); Livshic indicated this is a recurring pattern |
| **Score** | **12** | |

**Supporting Evidence**:
> "Schon das Erste Problem in Anführungsstrichen — sie sagt Anzahl der offenen Urlaubstage: 10, die KI sagt 22."
> — Livshic during case walkthrough, transcript

**Strategic relevance**: Connects to Pillar 1 (Platform Orchestration) — structured intake is a core requirement for the platform model. Bad data = delayed case handling = worse outcomes.

---

#### Child 3.1: Phone Team Notes Are Visually Indistinguishable From Client-Provided Information in the Fallgarten

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: In the Fallgarten (case summary/intake view), notes written by the internal phone team appear in the same visual style and location as information provided by the client. Lawyers cannot quickly distinguish between the two, leading to confusion about the source and reliability of the data.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Lawyers act on incorrect assumptions about data origin. In the live session, Livshic initially treated a phone team note as a client statement. |
| Reach | Broad | All lawyers reviewing the Fallgarten on intake — which is every lawyer on every case |
| Frequency | Regular | Happens whenever the phone team adds notes alongside client information |
| **Score** | **12** | |

**Supporting Evidence**:
> "Ich glaube tatsächlich, diese Notizen da unten sind vom Telefonteam, nicht von der Mandantin. Das ist ein bisschen irreführend, das müssten wir mal abändern."
> — Product team realizing the confusion in real-time, transcript

---

#### Child 3.2: Intake Fields and Uploaded Documents Frequently Contain Conflicting Data

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: The case intake form and attached documents (e.g., Gehaltsabrechnungen, Schriftsätze) often contain different values for key facts like the number of outstanding vacation days. Lawyers must manually cross-check multiple sources before acting, adding time and risk of error.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Forces rework (contacting client for clarification, cross-checking documents) before any legal work can begin |
| Reach | Significant | Observed with employment law cases specifically; may be broader. Exact frequency across case types unclear. |
| Frequency | Regular | Livshic encountered this during the live session with a specific case; described it as a recognized pattern |
| **Score** | **8** | |

**Supporting Evidence**:
> "Aus den Angaben wäre ich jetzt nicht auf 22 gekommen. Die Falldaten sagen mir 10."
> — Livshic on the specific case reviewed in session, transcript

**Gaps**: Limited to employment law observation in this session. Reach and frequency across other case types (housing, traffic) needs validation.

---

### Parent 4: Lawsuit (Klageschrift) Creation Involves Preventable Manual Steps

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: Despite Livshic being highly efficient (creates a Kündigungsschutzklage in ~6 minutes), two specific manual steps remain: (1) looking up the responsible court's address in an external Justice Portal, and (2) manually renaming file names to replace spaces with underscores before BEA upload. Both are automatable and add friction to an otherwise streamlined workflow.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Each step takes 1-3 minutes but is repetitive and interruptive. Not a major blocker, but clearly recognized as unnecessarily manual. |
| Reach | Broad | All lawyers filing lawsuits use both the court lookup and BEA. Filing lawsuits (Klagen) is a regular workflow for all employment and civil lawyers. |
| Frequency | Regular | Multiple times per week for active litigating lawyers |
| **Score** | **12** | |

**Supporting Evidence**:
> "Wenn ich eine Klage schreibe, das denke ich mir jedes Mal wieder — das Justizportal des Bundes und der Länder [...] die Idee wäre, dass man eine Datenbank hinterlegt mit den Adressen der Gerichte."
> — Livshic, transcript

**Strategic relevance**: Connects to Pillar 2 (AI-Powered Automation) — automating routine data lookup is exactly the type of efficiency gain the strategy targets.

---

#### Child 4.1: Court Addresses Must Be Manually Looked Up in an External Justice Portal Before Filing

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: When creating a lawsuit (Klageschrift), the responsible court's address is not pre-populated in the system. The lawyer must navigate to the external "Justizportal des Bundes und der Länder," enter the postal code, find the responsible court, and manually enter the address into the document. The address only appears in CaseForce once a court summons (Ladung) is received — too late for the initial filing.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Low | Adds ~1-2 minutes per lawsuit filing; interruptive but manageable with habit |
| Reach | Broad | All lawyers filing lawsuits — standard for Kündigungsschutz, housing, and employment cases |
| Frequency | Regular | Every new lawsuit filing |
| **Score** | **6** | |

**Supporting Evidence**:
> "Das Gericht raussuchen muss, das ist dann quasi eine Internetseite [...] dass man die Postleitzahl eingibt und dann schaut, welches Gericht zuständig ist. Die Idee dahinter wäre, dass man eine Datenbank hinterlegt mit den Adressen."
> — Livshic, transcript

> "Die Adressen stehen ja erst drin, nachdem ich die Ladung gekriegt habe [...] Wenn ich die Klage schreibe, habe ich ja noch gar keinen Kontakt zum Gericht."
> — Livshic explaining why the existing data isn't useful, transcript

---

#### Child 4.2: File Names Must Be Manually Renamed Before BEA Upload (Spaces → Underscores)

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: The German legal electronic communication system (beA) does not accept file names with spaces. When lawyers download files from CaseForce to upload to beA, they must manually rename every file — replacing all spaces with underscores — before the upload works.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Low | Small but annoying step that must be done for every beA upload. Confirmed as a known annoyance. |
| Reach | Broad | Every lawyer submitting documents to court via beA — which is all lawyers handling litigation |
| Frequency | Constant | Every beA submission |
| **Score** | **9** | |

**Supporting Evidence**:
> "Dann heißt die Datei 'Kündigungsschutzklage ordentliche Kündigung'. Wenn man das mit Unterstrichen machen könnte, weil der lässt keine Leerzeichen zu [...] Das heißt ich muss jedes Leerzeichen egal in welcher Datei immer zumindest zu einem Unterstrich machen."
> — Livshic, transcript

---

### 5: AI-Generated First Letters Are More Detailed Than Lawyers' Efficient First-Contact Style

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: The AI generates first letters (e.g., Urlaubsabgeltungsschreiben) that include full legal argumentation, statutory references, and detailed calculations. While technically correct, this doesn't match Livshic's preferred first-contact style — a short, direct demand letter that reserves full legal reasoning for cases where the employer contests the claim. This misalignment means lawyers need to significantly edit AI outputs, reducing the time-saving value.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Lawyers still need to edit the AI output extensively to match their style. Reduces adoption and trust in AI-generated documents. |
| Reach | Significant | Affects all lawyers using AI document generation. Different lawyers may have different preferences (not all will share Livshic's efficient approach). |
| Frequency | Regular | Every time AI document generation is used for first letters |
| **Score** | **8** | |

**Supporting Evidence**:
> "Ich hätte jetzt, wenn ich es freigeschrieben hätte, hätte ich einfach nur reingeschrieben: Das Arbeitsverhältnis wurde beendet, es sind 22 offene Urlaubstage, die Forderungen sind zur Urlaubsabgeltung gemacht. Also das wäre auf einer Seite."
> — Livshic describing his preferred brevity, transcript

> "Das ist jetzt detaillierter, als ich es gemacht hätte im Anschreiben, im ersten. [...] Wenn die Gegenseite dann sagt nein, dann kann man natürlich dieses ganze Zeug machen."
> — Livshic explaining his two-phase drafting approach, transcript

**Current workaround**: Lawyers either manually shorten AI output or don't use it for first letters
**Strategic relevance**: Directly relevant to Pillar 2 (AI-Powered Automation) — AI adoption depends on the output matching real workflows, not just being technically accurate.

---

### 6: Tasks Tab (Aufgaben) Is Systematically Deprioritized — Reviewed Only After All Case Work Is Done

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: The Aufgaben (tasks) tab in CaseForce is the lowest-priority view for lawyers. Livshic confirmed he only opens it "wenn ich mit meinen Fällen durch bin" — meaning tasks accumulate and are often delayed by days. This creates a structural gap where time-sensitive tasks (e.g., callback requests, follow-ups) sit unaddressed.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Low | Tasks do eventually get done, but the delay can cause client dissatisfaction. Livshic noted tasks from January were still open. |
| Reach | Significant | Likely affects many lawyers — the nature of the case-first workflow means tasks are always secondary |
| Frequency | Regular | Ongoing structural pattern, not just situational |
| **Score** | **4** | |

**Supporting Evidence**:
> "Also das ist was, das mache ich, wenn ich mit meinen Fällen durch bin. Also wenn ich quasi damit jetzt durch bin und noch Zeit habe."
> — Livshic on tasks, transcript

> "Ich gucke da immer mal wieder rein, alle drei, vier, fünf Tage und denke mir, boah scheiße, da ist viel offen geblieben."
> — Livshic, transcript

---

### 7: Clients With Non-German Backgrounds Need Phone-First Communication, But the Platform Is Email-Optimized

**Need**: Need
**Stakeholder**: Partner lawyer + Client
**Description**: Livshic has observed a consistent pattern: clients with non-German backgrounds (e.g., with Russian, Turkish, or other immigrant backgrounds) respond much more effectively to phone calls than to written emails. However, the platform's communication tools (CaseForce, AI suggestions) are optimized for email-first workflows. This creates inefficiency when dealing with this segment of clients — it takes significantly more email exchanges to achieve what one phone call resolves.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Without phone-first options, these cases take significantly longer and create more frustration for both the lawyer and the client. |
| Reach | Significant | Livshic specifically flagged this as a recurring pattern based on his case portfolio. Exact % of cases unclear. |
| Frequency | Regular | Multiple cases per month across the lawyer pool |
| **Score** | **8** | |

**Supporting Evidence**:
> "Bei ausländischen Mandanten telefoniere ich eher mal an und sage, ich verstehe euch, dass ihr damit Probleme habt [...] Das problem ist manchmal man hört sich aus aus den E-Mails."
> — Livshic, transcript

> "Manche schreiben dann nur 'Entschuldigung, ich habe vergessen mich zu melden' und so."
> — Livshic on email non-response from clients, transcript

**Gaps**: Hard to quantify reach without platform data on client demographics. Recommended to analyze response rates by communication channel.

---

### 8: PDF Document Viewer Rotation Is Unpredictable for Multi-Page Documents

**Type**: Problem
**Stakeholder**: Partner lawyer
**Description**: When rotating pages in the PDF viewer within CaseForce, lawyers are unsure which page will be rotated (the currently visible page or the entire document). This causes errors when reviewing multi-page scanned documents.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Low | Small UX bug; causes confusion but is not critical to case outcomes |
| Reach | Significant | All lawyers reviewing multi-page PDFs, which is standard |
| Frequency | Regular | Happens whenever lawyers need to rotate scanned documents |
| **Score** | **4** | |

**Supporting Evidence**:
> "Wenn ich nicht weit genug runter gescrollt hab oder zu weit runter, manchmal dreht er dann die untere. Da weiß ich nicht genau, welche Seite von beiden er dreht."
> — Livshic, transcript

---

## Cross-References

### Overlaps With Existing Opportunities

| New Opportunity | Existing Opportunity | File | Notes |
|---|---|---|---|
| 1.1 – Deadline view blocked in document editor | #13 CaseForce text editor and document creation are poor quality | `survey-partner-lawyers-2026-03-03.md` | Survey captured general document editing quality. This is a specific, high-priority UX issue within it. |
| 1.3 – Can't take call notes in parallel | #13 CaseForce text editor poor quality | `survey-partner-lawyers-2026-03-03.md` | Related but distinct — this is specifically about parallel window management, not editor quality |
| 3.1 / 3.2 – Conflicting/mixed intake data | #8 Case intake quality inconsistent, #9 Contact/address data often incomplete | `survey-partner-lawyers-2026-03-03.md` | Strong overlap. Survey captured the general problem; this adds specific evidence and sub-types (phone team notes vs. client data) |
| 5 – AI too detailed for first letters | #18 KI features have performance issues and inconsistent value | `survey-partner-lawyers-2026-03-03.md` | Partial overlap. Survey captured general AI quality issues; this is a specific style/format mismatch |
| 2.1 – No automated first-contact at case takeover | (none — new) | — | New theme not previously captured |
| 2.2 – Cases without deadlines get forgotten | (none — new) | — | New theme not previously captured |
| 4.1 – Court address manual lookup | (none — new) | — | New theme not previously captured |
| 4.2 – BEA file name renaming | (none — new) | — | New theme not previously captured |

### New Themes Identified

1. **Case takeover automation** — The critical moment when a lawyer pulls a case is completely unorchestrated. No system support exists to ensure first contact happens. This is a major gap.
2. **Context continuity in the document editor** — The editing experience is siloed from case data (deadlines, notes). A right-panel or overlay for case context during document editing is a high-value addition.
3. **Court infrastructure integration** — Integrating German court databases (Justizportal) and beA submission formatting into the platform would reduce friction for the most time-sensitive legal workflow (filing lawsuits).

### Gaps & Uncertainties

- **Reach of AI mismatch (Opp. 5)**: Only one lawyer's perspective. Other lawyers may prefer detailed first letters. Needs validation across lawyer segments.
- **Scale of client language issue (Opp. 7)**: No platform data on how many cases involve non-German speaking clients. Worth analyzing.
- **Generalizability of Livshic's workflow**: Livshic is a high performer with specific, efficient habits. Some observations may not apply to lower-performing lawyers who may have more systematic problems.
- **Tasks tab usage (Opp. 6)**: Platform-side data on task completion rates and delay times would validate the severity of this issue.

---

## Source Notes

**Source quality**: High — live screen-share session with a high-performing partner lawyer walking through real cases in real time. Observations are grounded in actual workflows, not hypothetical.
**Limitations**: Single lawyer perspective. Livshic is unusually efficient and process-oriented; less organized lawyers may have more severe versions of the same problems (or different ones entirely).
**Recommended follow-up**:
1. Validate case takeover automation (Opp. 2.1) with 3-5 additional lawyers — is the manual deadline-setting workaround common?
2. Run platform data pull: what % of newly taken cases have no activity in the first 48h?
3. Set up the Focus Group that Livshic suggested (Livshic + Emre + one more lawyer) specifically to test AI features and document generation style preferences.
4. Check beA file naming constraint — is this fixable on the CaseForce export side or requires beA-side change?
