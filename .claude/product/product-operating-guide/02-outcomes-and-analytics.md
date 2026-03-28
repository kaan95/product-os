# 📊 Outcomes & Analytics

> *"The best product teams are not measured by features shipped — they are measured by the impact those features have on the business and the customer."*
> — Marty Cagan

**Time allocation: ~20% (~8h/week)**

Outcomes are what change in the world as a result of what we build. Analytics is how we know whether that change happened. Without this, we are flying blind.

---

## Why It Matters (Cagan)

Cagan distinguishes sharply between **outputs** (features shipped) and **outcomes** (change in customer behaviour or business metrics). Feature factories optimise for outputs. Empowered teams optimise for outcomes.

This matters because a team can ship constantly and still fail — if the shipped work doesn't move any meaningful metric. The discipline of outcomes forces the question: *did what we built actually work?*

---

## Outcome vs. Output

| Output (avoid leading with this) | Outcome (lead with this) |
|---|---|
| "We shipped the notification feature" | "Lawyer response rate improved by 18%" |
| "We released the new onboarding flow" | "Time-to-first-value dropped from 3 days to 6 hours" |
| "We added 5 new filters to the search" | "Search-to-hire conversion increased by 12%" |

Epics and roadmap items should be framed as outcomes wherever possible.

---

## Goal Hierarchy

```
Business Goals (revenue, retention, growth)
    ↓
Product Goals (what Product can directly influence ✅)
    ↓
Product Outcomes / KPIs (measurable signals of progress)
    ↓
Epics / Initiatives (the work we do to move those outcomes)
```

**Key distinction:**
- **Business Goals** — can only be partially influenced by Product (e.g., "Increase ARR by 30%"). These are inputs.
- **Product Goals** — can be fully influenced by Product decisions (e.g., "Reduce churn rate by improving lawyer onboarding"). These are our targets.

---

## OKR Framework (Cagan + Google)

OKRs translate quarterly strategy into measurable commitments.

### Structure

**Objective** — Qualitative, inspiring, directional. The north star for the quarter.
*Example: "Make LegalHero the platform lawyers actually want to use every day."*

**Key Results** — Quantitative, measurable, time-bound. 2-4 per objective.
*Example: "Increase weekly active lawyers from 40% to 60% of registered users by Q2 end."*

### Rules for Good OKRs

1. **Baseline first** — You need a status quo number before you can set a target. Never set OKRs without knowing where you currently stand.
2. **Ambitious but honest** — A good OKR has roughly 70% confidence. If you're 100% sure you'll hit it, it's not ambitious enough.
3. **Product Goals, not Business Goals** — You own what you can influence. Don't set OKRs on revenue if you can't directly control the sales process.
4. **Bi-weekly check-ins** — Don't wait for quarter-end to discover you're off track. Review with the squad every two weeks.
5. **Kill what's not working** — If an initiative isn't moving the metric after a reasonable test, stop it. Don't sunk-cost your way to the end of a quarter.

---

## Monitoring & Dashboards

Good monitoring means you know your numbers before someone asks you.

**What to maintain:**
- A living dashboard tied to current OKR outcomes (PostHog or equivalent)
- Experiment tracking — results visible to the whole squad
- A weekly 5-minute data check as part of daily habit

**Key questions when looking at metrics:**
- Did the number move?
- *Why* did it move (or not)?
- Is the change statistically meaningful or just noise?
- What should we do differently as a result?

---

## Quarterly OKR Planning Rhythm

1. **4 weeks before quarter end** — Draft next quarter's objectives based on strategy direction
2. **2 weeks before quarter end** — Align with leadership and squad on objectives and key results
3. **Week 1 of new quarter** — Baseline all metrics, confirm OKRs, add to tracking
4. **Every 2 weeks** — Squad OKR check-in: progress, blockers, adjustments
5. **Final week of quarter** — Retrospective: what moved? What didn't? What do we carry forward?

---

## Weekly Outcomes Checklist

- [ ] Reviewed current OKR metrics — are we on track?
- [ ] Checked experiment results for any outcome signals
- [ ] Updated squad on outcomes in weekly sync
- [ ] Identified any metric that needs investigation (spike, drop, stall)
- [ ] Noted any initiatives to stop, scale, or pivot based on data

---

*← [Discovery](./01-discovery.md) | [Back to Index](./00-index.md) | Next: [Strategy & Vision →](./03-strategy-and-vision.md)*
