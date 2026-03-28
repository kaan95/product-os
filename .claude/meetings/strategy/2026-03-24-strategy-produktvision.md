# Meeting: Blocker, Strategy & Produktvision
**Date:** 24 March 2026 | **Duration:** ~3 hours
**Notion Source:** https://www.notion.so/Blocker-Strategy-Produktvision-32d5e8cace39801480e8ffeb5f82cf7b

---

## Strategic Core: From CRM to Autopilot

The central thesis: **LegalHero must transition from a manual CRM to a "Service-as-a-Software" Autopilot**.

- **Today:** LegalHero is essentially a CRM. Lawyers handle 100% of case work; LegalHero contributes 0% to actual case processing.
- **Target (18–24 months):** LegalHero handles 100% of case processing in autopilot mode. Lawyers retain a legal compliance "confirm" click (required by law) but no active work.
- **Why Autopilot > Co-Pilot:** Co-Pilot products get disrupted every time foundation models improve. Autopilots *benefit* — the service gets better automatically. This is the durable moat.

---

## The Pincer Threat

**Threat 1 — AI-native legal tech players (e.g., DeepLore/UQ):**
Already functionally ahead (catastrophic UI, but higher efficiency). If LegalHero stays at CRM level, it gets disrupted on price, speed, and quality.

**Threat 2 — Insurers building in-house:**
DEVK already has Klugo. Allianz could white-label something cheaply. Deep process integration ("End-to-End damage management") is the lock-in mechanism.

**The window: 12–18 months are decisive.**

---

## Three Focus Areas / Team Structure (from 2 April)

| Team | Focus | Room |
|---|---|---|
| **1 — Lawyer Autopilot** | AI-assisted case processing for lawyers | Basti's room |
| **2 — Operations Autopilot** | Automation for internal ops (mail, RSV, invoicing, telephone) | Amir's room |
| **3 — Running Business** | Customer requests, insurance integrations, APIs | Open area |

**Root problem today:** All resources are in Running Business. Strategic initiatives have near-zero dedicated capacity. The team split is the structural fix.

---

## Key Insights

1. **The clock is ticking.** Competitors are moving. The 12–18 month window to build an insurmountable advantage is real.
2. **AI value lands with lawyers, not LegalHero.** Efficiency gains currently go to partner lawyers. The Basis-Premium model is urgent to fix this.
3. **MCP tooling is a strategic lever.** Making ops teams self-sufficient drops inbound Product requests dramatically — freeing Product to build strategically.
4. **The organizational transformation is the hardest part.** Moving from ~30 Sachbearbeiter → ~10–11 experts/process owners is a cultural and structural shift requiring careful management.
5. **Insurers are already dependent on LegalHero.** Roland and Allianz/AWAC would suffer measurable damage if LegalHero stopped. Leverage not yet fully used.
6. **Rising complaints are the #1 short-term risk.** One insurer stopping case flow would be catastrophic. Q2 priority.
7. **"LegalHero Connect" (End-to-End) is a separate, high-potential business unit.** Quasi-independent, not to be communicated broadly yet. Requires one insurer to commit.
8. **Teams must be measured on outcomes, not feature shipping.** Adoption rates, automation rates, complaint reductions — not delivery velocity.
9. **Co-Pilot products are inherently fragile; Autopilots are durable.** Every foundation model improvement threatens a Co-Pilot (shrinks the moat); it benefits an Autopilot (improves the service).
10. **Legal compliance (Fremdbesitzverbot, lawyer-must-confirm) is a moat, not just a constraint.** New entrants cannot simply launch an autopilot — they lack the lawyer network and regulatory compliance infrastructure.
11. **DeepLore/UQ is functionally ahead.** The UI is catastrophic, but functional efficiency is reportedly already higher. This competitor benchmarks the urgency level.
12. **Hiring quality is "erschreckend" (alarming).** Current applicant pool quality across all roles needs to be diagnosed and addressed.
13. **B2C is deprioritized.** Would be a "declaration of war" on insurance partners. Only makes sense after the autopilot is built.

---

## Action Items for Product

### Immediate (this week)

- [ ] **Developer presentation erstellen** — Max 5 slides, strategy + team restructure. Present Thursday 26 March or early next week.
- [ ] **Hiring-Ziele an Nadine übergeben** — 5 hires: 4 Backend Engineers + 1 PM. Both PMs prepare shortlists immediately. Budget: €262k (covered by Forschungszulage).
- [ ] **Roadmapping Session** (25 March) — Rough roadmap per focus area ready.
- [ ] **Strategie-Dokument finalisieren** — Gaps to close, especially team sections. Send to Jörg and Mario as onboarding briefing.

### Before Sprint Start (2 April)

- [ ] **Team-Split implementieren** — Three teams in place with assigned seating/rooms.
- [ ] **Kaano übernimmt interim Team 1 (Lawyer Autopilot)** — Until dedicated PM hired (~3 months).
- [ ] **Mario's Rolle klären** — Team assignment once he joins.

### Strategic Product Work

- [ ] **Autopilot-Infrastruktur bauen** (three prerequisites):
  1. Full Markdown/text extraction of all case PDFs (Young Jin)
  2. Document classification system (Basti + Emre)
  3. Case-flow mapping per case type (Young Jin's graph system)
- [ ] **MCP Frontend für Ops-Teams** — Secure interface so ops teams can configure and use MCP automations without direct Codex access.
- [ ] **Beschwerdemanagement-Feature** — Surface at-risk cases (untouched 30/60 days) prominently for Partner Management. Q2 priority.
- [ ] **Basis-Premium-Modell entwickeln und implementieren** — Monetize autopilot efficiency via lawyer tier model (naming TBD: Basis/Premium or Lite/Pro).
- [ ] **Partner-CRM in CaseForce konsolidieren** — Fragmented across Intercom, Notion, CaseForce, Tableau today.
- [ ] **To-Do-Liste für Anwälte iterieren** — Define proper success metrics (long-term, ~1–2 year scope). Focus on adoption and accuracy improvement.
- [ ] **Anlage A (AI Use Case Roadmap) überarbeiten** — Shift focus from End-to-End to Lawyer Autopilot.

### Metrics & Accountability

- [ ] **Headline-Metriken je Team definieren:**
  - Team 1: "Avg. AI actions per lawyer" + "% AI emails sent without correction"
  - Team 2: "% tasks completed without human intervention"
  - Team 3: Complaint rate, customer satisfaction
- [ ] **Quartals-Roadmaps** with committed milestones, built collaboratively with the full team.
- [ ] **Epic-Template standardisieren** — Must include: customer impact, strategic alignment (→ autopilot), expected automation stages, success metric + timeframe.

### Hiring (by mid-May 2026)

- [ ] **4 Backend Engineers + 1 PM einstellen** — Only "Rockstars." If right PM not found by July, keep searching rather than compromise on quality.
- [ ] **Hiring-Qualität diagnostizieren** — Current applicant pool quality described as "erschreckend." Root cause to be identified.

### End-to-End / LegalHero Connect (longer horizon, confidential)

- [ ] **Ersten Kunden gewinnen** — Jörg and Niki in active talks (OERA already pitched). Requires one insurer "go" before building starts.
- [ ] **Anlage B (End-to-End Modules)** — Develop once customer confirms.
- [ ] **End-to-End Team/Business Unit strukturieren** — Define team composition (BizDev, PM, Developers, Key Account Manager for insurers).

---

## Additional Context

### Monetization: Basis-Premium Model
- **Problem:** AI efficiency gains currently land with partner lawyers, not LegalHero.
- **Solution:** Premium partners get higher revenue shares (e.g., 60% vs. 50% in Arbeitsrecht) in exchange for prioritized case allocation, AI features, fastlane document processing.

### LegalHero Connect (End-to-End Damage Management)
A separate business unit analogous to Control-Expert (automotive) and Property-Expert (construction). Products include: digital damage intake, AI-powered coverage assessment (Deckungsprüfung), case routing, legal case processing, invoice validation, and regress.
- **Pricing model:** Base fee (~€15k/month per insurer) + transactional (€0.95/case routed, €30/invoice check, €50/coverage check).
- OERA already pitched with positive initial reaction. Not to be communicated broadly internally yet.

### Hiring Budget
- €262,000 fully covered by Forschungszulage (research tax incentive)
- Average salary ~€75k, employer costs ~€90k
- Start target: May 2026
- Two backend candidates already in conversation; one very positive
