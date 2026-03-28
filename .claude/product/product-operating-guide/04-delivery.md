# 🚢 Delivery

> *"The goal of delivery is not to implement the roadmap. It is to deliver working software that achieves the desired outcomes — quickly, with high quality, and without burning out the team."*
> — Marty Cagan

**Time allocation: ~25% (~10h/week)**

Delivery is how great ideas become real impact. The PM's role in delivery is not to manage the work — it is to ensure the team always knows what to work on, why it matters, and what done looks like.

---

## Why It Matters (Cagan)

Cagan is explicit: PMs do not manage projects. They manage outcomes. But delivery still requires the PM to be present, unblocking, and aligned. The biggest delivery failure is not slow shipping — it is shipping the wrong thing with high confidence.

Cagan's model: **Discovery de-risks. Delivery executes.** Both must run simultaneously. Delivery without discovery builds the wrong thing fast. Discovery without delivery learns but never ships.

---

## The PM's Role in Delivery

| Not the PM's job | The PM's job |
|---|---|
| Managing sprint ceremonies | Ensuring engineers know what to pick up next |
| Writing technical specs | Writing clear problem statements and acceptance criteria |
| Tracking burn-down charts | Keeping the backlog prioritised and the roadmap current |
| Deciding technical architecture | Giving engineers the context to make architecture decisions themselves |
| Moving tickets | Unblocking engineers when decisions are needed |

---

## User Stories — What Great Looks Like

Every ticket should have:

1. **A clear problem statement** — what user problem does this solve and why does it matter now?
2. **A link to an Epic** — which outcome is this ticket serving? (No orphan tickets)
3. **Acceptance criteria** — specific, testable conditions that define "done"
4. **Priority** — is this P0 (must have), P1 (should have), P2 (nice to have)?
5. **Context for engineers** — what do they need to know to make good decisions?

**Template:**

```
Problem: [The user currently cannot / struggles to ___]
Why now: [This matters because ___ and blocks ___ outcome]
Acceptance Criteria:
  - [ ] Given ___, when ___, then ___
  - [ ] Given ___, when ___, then ___
Notes for engineers: [Any relevant constraints, edge cases, or prior decisions]
Epic: [Link to Epic / Outcome]
```

---

## Backlog & Sprint Management

**Backlog health principles:**
- The backlog is always prioritised — engineers should never have to ask what to work on next
- Items without a clear outcome link get removed or parked
- Refine the backlog weekly, not just at sprint planning
- Plan no more than 1 quarter ahead in detail — beyond that, use themes not tickets

**Sprint rhythm:**
- Sprint planning: align the squad on what this sprint is for and what "success" looks like
- Mid-sprint: check in on blockers, adjust priorities if new information arrives
- Sprint review: demo, collect feedback, log learnings
- Retrospective: what can we improve in how we work?

---

## Release Notes

After every release, prepare release notes:

1. Export released items from Jira
2. Draft release notes (what changed, what it means for users, any known issues)
3. Communicate to relevant stakeholders — lawyers, internal OS users, leadership
4. Add to the release log

Release notes are not a formality — they build trust with stakeholders and create an audit trail of what shipped and why.

---

## Cagan on Empowered Delivery Teams

**Give context, not tasks.** The PM's job is to ensure the team understands the customer problem, the business context, and the outcome they're optimising for. With that context, engineers make better technical decisions independently.

**Protect the team's focus.** Unplanned interruptions are a tax on delivery speed. The PM should absorb requests from stakeholders and filter them — not let every stakeholder request land directly in the sprint.

**Celebrate outcomes, not outputs.** In sprint reviews and team communications, lead with what the work accomplished, not what was shipped.

---

## Daily Delivery Checklist

- [ ] Backlog is prioritised — engineers know what to pick up next
- [ ] Any blockers identified and actively being resolved
- [ ] Jira is up to date and reflects reality
- [ ] Release notes prepared for anything shipped today/this week

---

*← [Strategy & Vision](./03-strategy-and-vision.md) | [Back to Index](./00-index.md) | Next: [Communication & Stakeholders →](./05-communication-and-stakeholders.md)*
