# Sprint Plan — Sprint CX 3 · Q2 2026 · April 30 → May 14, 2026

## Sprint Goal

> **By end of Sprint CX 3, the Pro Package v2 pilot is live and stable for 10 partner law firms, the ARAG API is fully integrated end-to-end in CaseForce, and the Ops Migration (CX-180) is officially complete with every Ops team operating exclusively in CaseForce.**

Three goals, one sentence, zero "and also". Everything else this sprint exists to support these three.

---

## The Three Goals

### Goal 1 — Pro Package v2: Ship for May 1 Pilot
Pilot for 10 partner law firms goes live on Day 2. Every v2 ticket must be in production by then or the pilot ships broken.

### Goal 2 — ARAG API: End-to-End in CaseForce
A real case from ARAG creates correctly in CaseForce inbound, with all Arbeitsrecht fields, no legacy fallback. Closes the last insurance integration gap.

### Goal 3 — Ops Migration (CX-180): Closed
Every Ops team (Post, Phone, Finance, RSV, TV) confirms at sprint review that they operate exclusively in CaseForce. CX-180 moved to Done.

---

## Quarter Alignment

| Q1 Objective (still active) | Current State | What This Sprint Moves |
|-----------------------------|---------------|------------------------|
| **Revenue / take rate**: 46% → 48.72% | v2 features in late review; pilot Day 2 | Ships v2 to production, lands May 1 pilot |
| **Insurance SLA compliance** (ARAG) | BE Prod Review, FE Blocked + Staging | Closes ARAG end-to-end |
| **Platform**: All Ops teams on CaseForce | 1 Open, 5 in late stages, 3 In Progress | Closes CX-180 |

> No `outcomes-q2-2026.md` exists yet. Q1 outcomes remain the operational reference. Drafting Q2 outcomes is a separate task, recommended before Sprint CX 4.

---

## Committed Work

### Goal 1 — Pro Package v2 (Epic CX-4)

**Definition of done:** All v2 tickets in production by end of Day 3 (May 4). Pilot for 10 firms running on production v2 by May 1, monitored daily for first 5 days.

| Jira Key | Title | Priority | Status (now) | Owner | Why this sprint |
|----------|-------|----------|--------------|-------|-----------------|
| CX-187 | BE - v2: Check premium summaries are correct | Medium | **Blocked** | Kaan Özgiray | **Unblock Day 1.** Payout accuracy depends on it. Same risk as S2. |
| CX-11 | FE - CTL filtering for Kündigung Premium agencies | Medium | QA (Feature) | Kaan Özgiray | Close QA, ship. |
| CX-233 | BE - Premium Flag on Billing Queue | High | Prod Review | Ester Daci | Deploy. |
| CX-234 | BE - Premium Flag on Deckungsanfragen | High | Prod Review | Ester Daci | Deploy. |
| CX-235 | BE - Premium Flag on Inbound Emails & Attachments | High | In Progress | Ester Daci | Finish (last v2 BE flag). |
| CX-236 | FE - Premium First Filter (Billing Queue) | High | Ready → Staging | Kaan Özgiray | Promote to Prod. |
| CX-237 | FE - Premium First Filter (Deckungsanfragen) | High | Ready → Staging | Kaan Özgiray | Promote to Prod. |
| CX-238 | FE - Premium First Filter (Inbound Emails) | High | Ready → Staging | Kaan Özgiray | Promote to Prod. |
| CX-257 | BE - Premium Flag on INBOUND-DOCUMENTS Endpoint | Medium | Prod Review | Ester Daci | Deploy. Fourth queue priority sort. |

---

### Goal 2 — ARAG API Close-out (Epic CX-2)

**Definition of done:** A real ARAG case created via the API lands in CaseForce inbound, fully visible with all required Arbeitsrecht fields. No legacy fallback.

| Jira Key | Title | Priority | Status | Owner | Why this sprint |
|----------|-------|----------|--------|-------|-----------------|
| CX-31 | BE - ARAG new endpoint for cases | High | Prod Review | Houcem Kacem | Deploy — this is the API contract. |
| CX-228 | BE - Route API/Webakte Inbound from Legacy → CaseForce | High | Staging | Houcem Kacem | Promote to Prod. |
| CX-219 | FE - Missing fields for ARAG (Arbeitsrecht) | High | **Blocked** | Kashan | **Unblock Day 1.** If unresolvable by Day 2, escalate or descope. |

---

### Goal 3 — Ops Migration (Epic CX-180)

**Definition of done:** All Ops teams (Post, Phone, Finance, RSV, TV) operate exclusively in CaseForce. CX-180 closed at sprint review with sign-off from each team lead.

| Jira Key | Title | Priority | Status | Owner | Why this sprint |
|----------|-------|----------|--------|-------|-----------------|
| CX-177 | FE - Add missing CCC fields to CaseForce case overview | Highest | **Open** | Kaan Özgiray | Last open Highest. Single biggest blocker to "migration complete". |
| CX-139 | BE - Notification + highlight new inbound case | Highest | Prod Review | Houcem Kacem | Deploy. |
| CX-70 | BE - Improve working on documents in CaseForce | Highest | Prod Review | Ester Daci | Deploy. |
| CX-261 | FE - Notification + highlight (FE counterpart of CX-139) | High | Prod Review | Kashan | Deploy alongside CX-139. |
| CX-227 | BE - Route Website Integration Cases from Legacy → CF | High | Code Review | Houcem Kacem | Merge + deploy. |
| CX-264 | BE - Empty flow link | Highest | In Progress | Yessmine Chabchoub | Finish. |
| CX-229 | FE - Website Integration Cases view in CF Inbound list | Medium | In Progress | Kashan | Finish — pairs with CX-227. |
| CX-262 | FE - Document rotation from merge tool | High | In Progress | Brisilda Bushi | Finish. |
| CX-249 | BE - List of all unassigned website cases | High | TBD | Assign Day 1 | Completes inbound visibility. |

---

### Carryover Deploys — Ship With the Sprint, Not a Goal

These are already in late-stage deploy queue and would be wasteful to hold back, but they don't earn sprint-goal status.

| Jira Key | Title | Priority | Status | Owner |
|----------|-------|----------|--------|-------|
| CX-239 | FE - HUK Follow up with validation | Highest | Ready → Prod | Kaan Özgiray |
| CX-182 | FE - Display HUK Coverage Result in Case Creation | Highest | Ready → Prod | Kaan Özgiray |

---

### Critical Bugs — Ship Regardless

Not a sprint goal, but Highest/High bugs ship with the sprint.

| Jira Key | Title | Priority | Status | Owner |
|----------|-------|----------|--------|-------|
| CX-288 | BE - Issues in delivering Emails | Highest | In Progress | Houcem Kacem |
| CX-220 | BE - legacy NullPointerException | Highest | Prod Review | Houcem Kacem |
| CX-277 | BE - Emails parsing Issue | High | Staging | Houcem Kacem |
| CX-240 | BE - DOCX files no longer previewable | High | Staging | Ester Daci |
| CX-271 | BE - NPE on null LegalCase from Action | Medium | Prod Review | Houcem Kacem |
| CX-280 | BE - Error assigning case 147790 to PA 613 | Medium | In Progress | Houcem Kacem |

---

## Stretch Goals
*(Only if the three core goals are done. Do not sacrifice committed work for these.)*

- [ ] **CX-216** — BE: Bootstrap Test entities in Review envs (Code Review — close out tech debt)
- [ ] **CX-13** — FE: Fix search behavior on all views (Code Review — close out tech debt)
- [ ] **CX-198 / CX-202** — User Requests Q2 (already in Prod Review — promote if review bandwidth allows)
- [ ] **CX-242** — FE: Internal Users see enhanced Case Transfer List (Blocked — investigate Day 1, park if unresolvable)

---

## Explicitly Out of Scope This Sprint

- **Pro Package v3 (CX-5)**: All v3 tickets — CX-289 (high-value classification), CX-293 (star indicator), CX-294 (Pro head-start), CX-295 (cohort randomization), CX-296 (trial payout cut-over), CX-188 (feature toggles BE), CX-189 (AI tokens), CX-184 (push notifications), CX-185/186 (contract versioning). v3 starts Sprint CX 4 once v2 is stable in production.
- **E2E test pipeline (CX-269)**: continues in parallel under Hamza, not part of sprint goal.
- **Reduce Complaints (CX-14, CX-191 in Prod Review)**: promote opportunistically, not committed.
- **Finance department work** (Notion product board high-priority items: CSV export, HUK Glatt-ziehen, Vorsteuer download, Rechnungen by date): all Finance department, not CX squad.
- **Q2 outcomes doc**: needed but separate from sprint planning — flag to do this week.

---

## Risks & Watch Items

| Risk | Severity | Mitigation |
|------|----------|------------|
| **CX-187 still blocked** (Premium summaries — same as Sprint 2) | **Critical** | Kaan unblocks Day 1. If unresolved by Day 2, descope from pilot scope and brief stakeholders **before** May 1 comms go out. |
| **CX-219 (ARAG FE) blocked** | High | Kashan investigates Day 1. If blocker is upstream/external, reassign or escalate same day. |
| **CX-177 still Open at Highest** | High | Kaan finishes Week 1; if at risk, drop all stretch immediately. |
| **Pilot Day 2 (May 1)** | **Critical** | Pre-launch checklist by Apr 30 EOD. Daily standup explicitly checks pilot health for first 5 days. Rollback plan documented. |
| **Houcem load**: CX-31, CX-227, CX-228, CX-220, CX-277, CX-271, CX-280, CX-288, CX-249 | High | Houcem owns deploy/finish work only — no net-new BE this sprint. CX-249 reassigned if Houcem at capacity. |
| **No v3 progress** | Medium (accepted) | v3 deferred to CX 4 by design. Communicate to Pro Package stakeholders before May 1 so v3 expectations are calibrated. |

---

## How We'll Know This Sprint Succeeded

1. **Goal 1 — Pilot live and stable**: 10 partner firms onboarded to v2 by May 1; zero P0/P1 incidents in first 5 days; Premium First filter and CTL Kündigung filter working in production.
2. **Goal 2 — ARAG closed**: A real ARAG case creates end-to-end in CaseForce; legacy fallback fully removed.
3. **Goal 3 — CX-180 closed**: Each Ops team lead confirms in sprint review they operate exclusively in CaseForce. Epic moved to Done.
4. **Bonus**: HUK deployed; no Highest-priority bugs open at sprint end.

---

## Verification

- **Pilot health**: Monitor partner-firm logins, CTL filter usage, billing queue priority sort behavior in production daily for first 5 days post-May-1.
- **ARAG end-to-end**: Trigger a real ARAG test case via API; confirm it lands in CaseForce inbound with all Arbeitsrecht fields populated; confirm no Legacy entry.
- **Ops migration sign-off**: Walk each Ops team lead through their CaseForce-only workflow at sprint review; capture sign-off in retro doc.
- **HUK (bonus)**: Run a real HUK case-creation flow; confirm coverage check result rendered with validation states.
