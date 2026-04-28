# Problem Statement Examples

Paired before/after examples for the **Problem** section of a user story or bug ticket. Use these as a calibration reference when drafting or reviewing tickets.

The pattern is always the same: the bad version describes the *ticket* or the *solution*, the good version describes the *user* and their *pain*.

---

## Example 1 — Performance promise on a paid tier

### ❌ Weak

> The 100ms search latency cap is the core performance promise of the Premium tier. The cap was finalised at 100ms on 2026-04-15 (superseding an earlier 250ms target from 2026-03-22). This ticket exists to lock in and verify the 100ms target is enforced in the search service.

**Why it fails:** leads with a specific number, recounts decision history, frames the ticket as verification work. A reader still doesn't know why anyone cares.

### ✅ Strong

> Premium-tier users pay for a faster product, but search currently returns results in 300–500ms — slow enough to feel laggy on every keystroke. Search latency is the top-cited friction point in Premium NPS surveys this quarter, putting renewal at risk among power users who run dozens of searches per day.

**Why it works:** names the persona (Premium users), describes observable pain (laggy search), grounds the business consequence (renewal risk). The actual latency target lives in AC, not here.

---

## Example 2 — Surfacing high-priority records

### ❌ Weak

> Add a `priorityFlag: boolean` field to the records API and surface it as a star icon in the list view. The flag should be set when a record's value exceeds €10,000 or its expiry date is within 7 days. Approximately every 5th–10th record should qualify.

**Why it fails:** prescribes the API field, the UI treatment, the threshold values, and the expected hit rate. None of those are PM decisions and none belong in the Problem.

### ✅ Strong

> Account managers triage hundreds of records per day and currently have no way to spot the high-stakes ones at a glance. Time-sensitive opportunities get missed because important records look identical to routine ones in the list view. We need a visual signal that lets account managers prioritise without scanning every row.

**Why it works:** names the persona (account managers), describes the failure mode (missed opportunities), motivates the change without prescribing the mechanism. Field names, thresholds, and UI treatment go in Scope and AC.

---

## Example 3 — Bug ticket framed as a code change

### ❌ Weak

> This ticket exists to fix the off-by-one error in the pagination component identified in Sentry issue #4521.

**Why it fails:** describes the code change, not the user impact. A dev reading this doesn't know whether to prioritise it over five other bugs.

### ✅ Strong

> Users navigating to page 2 of search results see the same items they saw on page 1 — duplicate results across pagination. This makes the product feel broken and forces users to scroll endlessly to find what they need. Reported by 3 customers in the last week; affects all paginated lists across the product.

**Why it works:** describes what the user actually experiences, the felt impact, and the blast radius. The Sentry link belongs in Evidence, not Problem.

---

## Example 4 — Internal infrastructure work with no visible "why"

### ❌ Weak

> Move the customer export job from the legacy worker into the new Temporal pipeline so we can decommission the old infrastructure by Q3.

**Why it fails:** this is a dev work-item description. There's no user or business problem visible — only an internal milestone. If priorities shift, no one can argue for this ticket because no one knows what's at stake.

### ✅ Strong

> Customer exports currently fail silently 5–10% of the time, leaving the success team without the data they need for QBRs and account reviews. The success team has logged this as their top weekly tooling complaint for the past two quarters, and the failures correlate with churn signals being missed during renewal cycles.

**Why it works:** translates an infra migration into a user-facing problem (success team), gives the consequence (missed churn signals), and provides evidence of severity (two quarters of complaints). The "move to Temporal" decision belongs in Scope.

---

## Self-review checklist

Before submitting, run the Problem section through this checklist:

- [ ] Does it name a real human persona (user, customer, operator, internal team)?
- [ ] Does it describe observable pain — something a reader could go and witness?
- [ ] Does it state the business consequence of not fixing it?
- [ ] Is it free of specific values, thresholds, field names, endpoints, or UI mechanics?
- [ ] Is it free of decision history and meeting dates?
- [ ] Does it avoid the phrase "this ticket exists to…"?
- [ ] If a dev read only this section, would they understand who hurts and why?

If any answer is "no", rewrite before creating the ticket.
