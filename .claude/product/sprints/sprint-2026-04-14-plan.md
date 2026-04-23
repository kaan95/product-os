# Sprint Plan — Sprint 2 · Q2 2026 · April 14 → April 25, 2026

## Sprint Goal
> By end of sprint, the ARAG new case endpoint is integrated in CaseForce, all Premium Package v2 features are shipped and ready for May 1 pilot launch, and all remaining Ops team migration blockers are resolved so every team operates exclusively in CaseForce.

## Why This Sprint Is Non-Negotiable
- **May 1**: Premium Package pilot launches with 10 law firms. CX-4 must be complete this sprint — there is no Sprint 3 buffer.
- **ARAG API**: CX-31 (BE) is In Progress. CX-219 (FE) and CX-194 (FE) are unstarted. Finishing the API unlocks automatic case routing (CX-228) and closes the last insurance integration gap.
- **Ops Migration**: CX-139 and CX-70 are in progress at Highest priority. CX-177 (Yessmine) is Highest and open. The migration cannot be called complete until these land.

## Quarter Alignment

| Objective | Current State | What This Sprint Moves |
|-----------|--------------|----------------------|
| Revenue: Take rate 46% → 48.72% | Premium Package pilot planned May 1 | Ships v2 features required for pilot go-live |
| Insurance SLA compliance | ARAG API BE in progress, FE unstarted | Closes ARAG API integration end-to-end |
| Platform: All Ops teams on CaseForce | 3/8 migration tickets in progress | Resolves all remaining CX-180 blockers |

---

## Committed Work

### Customer Excellence Squad — ARAG API (CX-2)

| Jira Key | Title | Priority | Status | Owner | Why this sprint |
|----------|-------|----------|--------|-------|-----------------|
| CX-31 | BE - ARAG new endpoint for cases | High | In Progress | Houcem Kacem | Finish & merge — this is the core API contract |
| CX-219 | FE - Add missing fields to case creation form for ARAG (Arbeitsrecht) | High | Open | Assign FE dev | Unstarted blocker — FE cannot ship without it |
| CX-194 | FE - ARAG new endpoint implementation | Medium | TBD | Assign FE dev | Completes the FE integration layer |
| CX-228 | BE - Route ARAG Inbound Cases from Legacy to CaseForce | High | Open | Houcem Kacem | Ops migration dependency + ARAG routing completion |

**Definition of done:** A case initiated via ARAG API creates correctly in CaseForce, is visible in the inbound list, and can be processed without legacy system fallback.

---

### Customer Excellence Squad — Premium Package v2 (CX-4)

| Jira Key | Title | Priority | Status | Owner | Why this sprint |
|----------|-------|----------|--------|-------|-----------------|
| CX-11 | FE - CTL filtering for Kündigung cases Premium agencies | Medium | QA (Feature) | Kaan Özgiray | In QA — close and ship. Core CTL feature for pilot. |
| CX-187 | BE - Check if summaries correct for premium lawyers | Medium | Blocked | Kaan Özgiray | **Unblock Day 1.** Payout accuracy depends on this. |
| CX-233 | BE - Expose Premium Flag on Billing Queue | Medium | Open | Assign BE dev | Required for priority sorting — 3 BE flags ship together |
| CX-234 | BE - Expose Premium Flag on Deckungsanfragen Endpoint | Medium | Open | Assign BE dev | Required for priority sorting |
| CX-235 | BE - Expose Premium Flag on Inbound Emails & Attachments | Medium | Open | Assign BE dev | Required for priority sorting |
| CX-236 | FE - Premium First Filter Toggle on Billing Queue | Medium | Open | Assign FE dev | Depends on CX-233 |
| CX-237 | FE - Premium First Filter Toggle on Deckungsanfragen | Medium | Open | Assign FE dev | Depends on CX-234 |
| CX-238 | FE - Premium First Filter Toggle on Inbound Emails & Attachments | Medium | Open | Assign FE dev | Depends on CX-235 |

**Definition of done:** CTL Kündigung filter live for pilot agencies; Premium flag exposed on all three queues; billing summaries validated. System is ready for May 1 pilot onboarding.

---

### Customer Excellence Squad — Ops Migration (CX-180)

| Jira Key | Title | Priority | Status | Owner | Why this sprint |
|----------|-------|----------|--------|-------|-----------------|
| CX-139 | BE - Add notification + highlight new inbound case | Highest | In Progress | Ester Daci | Finish — inbound visibility blocker for Ops teams |
| CX-70 | BE - Improve working on documents in CaseForce | Highest | In Progress | Ester Daci | Finish — document workflow prerequisite for migration |
| CX-177 | FE - Add missing CCC fields to CaseForce case overview | Highest | Open | Yessmine Chabchoub | Highest and open — teams cannot fully migrate without this |
| CX-227 | BE - Route Website Integration Cases from Legacy to CaseForce | High | Open | Assign BE dev | Closes legacy routing gap alongside CX-228 |
| CX-213 | BE - Incorrect CCC Assignment in Nebenkosten cases | Medium | Open | Assign BE dev | Data quality blocker for RSV team migration |

**Definition of done:** All Ops teams (Post, Phone, Finance, RSV, TV) can process their full caseload in CaseForce without any legacy system dependency. CCC fields complete, inbound notifications live, document workflows functional.

---

### Critical Bugs — Ship Regardless of Epic

| Jira Key | Title | Priority | Status | Owner |
|----------|-------|----------|--------|-------|
| CX-225 | BE - Kündigung cases still not working | Highest | Open | Mohammad Amir |
| CX-220 | BE - NullPointerException in legacy system | Highest | Prod Review | Houcem Kacem |

---

## Stretch Goals
*(Only if core is done. Do not sacrifice committed work for these.)*

- [ ] CX-46 — BE: Fixes to case creation with follow-up channel (Medium, Houcem) — edge case migration fix
- [ ] CX-229 — FE: Website Integration Cases view in CaseForce inbound list (Blocked — investigate blocker first)
- [ ] CX-231 — BE: Migration | Legacy Cases missing on CF (Medium, Houcem) — data completeness

---

## Explicitly Out of Scope This Sprint

- **Premium Package v3 (CX-5)** — AI token system (CX-189), feature toggles (CX-188), push notifications (CX-184), contract versioning (CX-185/186). All blocked or deprioritized. May 1 pilot runs on v2 only.
- **Case Intelligence System** — Not in scope until Premium Package is stable.
- **Finance automation (OS-3394)** — Invoice download work (OS-3395–3398) runs in parallel under Finance squad; separate sprint goal.
- **KPI Tracking (OS-2477)** — Separate squad, not part of this sprint's goal.

---

## Risks & Watch Items

| Risk | Severity | Mitigation |
|------|----------|------------|
| **Houcem overloaded** — carries CX-31, CX-228, CX-220 + stretch items | High | Assign CX-227 and CX-219 to another dev immediately. Houcem finishes CX-31 first. |
| **CX-187 blocked (Premium payout summaries)** | High | Kaan investigates and unblocks Day 1. If not resolvable in 2 days, descope and flag to stakeholders before pilot comms go out. |
| **May 1 pilot deadline** | Critical | 8 CX-4 tickets must ship in 10 days. No buffer. Daily status check on Premium work from Day 5. |
| **Unassigned FE tickets (CX-219, 236, 237, 238, 194)** | Medium | Assign in sprint planning Day 1 — cannot sit unowned given the deadline. |
| **CX-229 blocked** | Medium | Investigate blocker Day 1. If unresolvable, park for Sprint 3 and remove from stretch. |

---

## How We'll Know This Sprint Succeeded

1. **ARAG API closed** — A new case initiated via ARAG API creates correctly in CaseForce inbound list, tested end-to-end in staging with a real ARAG test case.
2. **Premium Package v2 ship-ready** — CTL Kündigung filter live for pilot agencies; Premium flags on all 3 queues; payout summaries validated. Pilot onboarding confirmed for May 1.
3. **Ops migration complete** — CCC fields visible, inbound notifications working, document workflows unblocked — confirmed by each Ops team lead at sprint review.
4. **Zero Highest-priority bugs open** — CX-225 and CX-220 resolved by end of sprint.
