# Step 3: The OKR Structure

Every section of the roadmap is anchored to an **Objective** — a qualitative, memorable direction the team wants to move toward. Under each Objective are **Key Results** — measurable signals that tell you the Objective was achieved. Under each Key Result are **Initiatives/Bets** — the work the team believes will move the needle.

```
Objective (O)           — qualitative direction, inspiring but grounded
├── Key Result 1 (KR)   — specific, measurable outcome signal
│   ├── Initiative A    — a bet we're making to move this KR
│   └── Initiative B    — another angle on the same KR
└── Key Result 2 (KR)
    └── Initiative C
```

---

## What Makes a Good Objective

- Qualitative and directional ("Make new users wildly successful in their first week")
- Memorable — a team member should be able to say it without looking at the doc
- Specific enough to be meaningful, broad enough to allow multiple approaches
- *Not* a feature ("Launch redesigned onboarding" is an initiative, not an objective)

## What Makes a Good Key Result

- Measurable and time-bound (e.g., "7-day retention increases from 38% to 52% by end of Q2")
- Outcome-oriented — it measures a *change in behaviour or performance*, not activity
- Ambitious but achievable — if you're certain you'll hit it, it's not a KR; if it's a fantasy, it destroys motivation
- Avoid: "Complete X", "Launch Y", "Ship Z" — these are all outputs, not KRs

---

## Output vs. Outcome — The Key Distinction to Coach On

| Output (avoid as KR) | Outcome (what the KR should say) |
|---|---|
| "Launch redesigned onboarding" | "% of new users completing onboarding rises from 45% to 70%" |
| "Ship push notifications" | "Weekly active users grow 15% as users return to finish tasks" |
| "Migrate to new infra" | "P95 API latency drops below 200ms" (if user-facing) or classified as a constraint |
| "Build admin dashboard" | "Support tickets about account settings drop 40%" |

---

## Initiatives / Bets

These are the work the team is planning *in service of* the KRs. They're held lightly — if evidence emerges that a different initiative would move the KR better, the team should feel free to swap it out. List initiatives under the KR they serve, not as standalone line items.

**Committed vs. Exploratory:**
Some initiatives are non-negotiable (compliance, existing contracts, critical tech debt). Mark these as **Committed**. Others are bets — mark them as **Bet**. This distinction helps the reader understand where the team has agency.
