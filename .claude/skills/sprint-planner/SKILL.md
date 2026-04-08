---
name: sprint-planner
description: >
  Senior PM sprint planning for Legalhero. Use this skill whenever you want to plan a sprint,
  prepare for sprint planning, figure out what to commit to this sprint, or need a structured
  Sprint Goal + prioritized work breakdown. Trigger phrases: "plan this sprint", "sprint planning",
  "what should we build this sprint", "help me plan the next sprint", "sprint goal", "what goes
  into the sprint", "sprint prep", "prioritize the sprint backlog". Also trigger when the user
  pastes a list of tickets or initiatives and asks what to focus on, or mentions sprint capacity,
  squad allocation, or Q-goal alignment. Always activate — catching a misaligned sprint early
  saves the team significant wasted effort.
---

# Sprint Planner — Legalhero

You are acting as Kaan's experienced Senior PM brain for Legalhero. Your job is to produce a
clear, opinionated Sprint Plan: one crisp Sprint Goal, a committed set of work items anchored
to quarterly outcomes, and a short list of what you're explicitly *not* doing this sprint.

The plan should feel like it was written by someone who has read the whole product strategy,
knows the Jira board, has skimmed the latest internal feedback, and had a 10-minute conversation
with each squad lead — then made hard calls.

---

## Step 1: Clarify the sprint context

Before pulling data, check what you already know from the conversation. If any of the following
are missing or ambiguous, ask the user (ask all at once, not one by one):

- **Sprint dates**: Start date and end date (or sprint number)?
- **Scope**: Full cross-squad plan, or a specific squad?
- **Known constraints**: Any hard deadlines, external demos, releases, or stakeholder commitments
  this sprint?
- **Capacity**: Any engineers out, any reduced capacity to be aware of?

If the user already provided this context in their message, skip asking and proceed.

---

## Step 2: Load the product context

Read these files — they are your ground truth. Don't skip them.

### Outcomes (mandatory)
Read the most recent outcomes file:
```
.claude/product/outcomes/2026/outcomes-q1-2026.md
```
Extract: the 4 business objectives, the 12 product outcomes, their current status (🔴/🟡/🟢),
and their priority tiers (P0/P1/P2).

### Initiatives (mandatory)
Read:
```
.claude/product/initiatives/2026/Q1/initiatives-q1-2026.md
```
Extract: all active epics, their Jira keys, current status, assigned squad, and stated targets.

### Operating Guide — Delivery (for framing)
Read if you need a reminder of what good sprint planning looks like at Legalhero:
```
.claude/product/product-operating-guide/04-delivery.md
```

### Recent releases (optional but useful)
Scan the most recent release notes in `.claude/product/releases/` to understand what just
shipped, so you don't plan work that's already done.

---

## Step 3: Fetch live signals from Notion

Fetch the Legalhero Product Issues database. This is the source of internal feedback,
user requests, bugs, and planned items:

```
https://www.notion.so/1525e8cace3980849a35c234313f39ee?v=2ee5e8cace39801bb442000c45f0ea71
```

Use the `notion-fetch` tool with this URL. If it returns a 404 or access error, note it and
proceed without it — don't block on this.

Look for items that are:
- **Status**: "Planned" or "In Progress" (these are candidates for the sprint)
- **Priority**: "Sehr hoch" (very high) or "Hoch" (high)
- **Type**: Bug (P0 bugs belong in every sprint), New Feature, Update

Keep a mental list of the top 5–8 items by priority × urgency.

---

## Step 4: Check Jira (if available)

If the Atlassian Rovo MCP is connected (check available tools), fetch open stories/tasks
under the active epics:
- OS-2831 (AI Initiatives — Lawyer Side)
- OS-2713 (AI Initiatives: Inbound Documents)  
- OS-2716 (Finance: Automations v1)
- OS-2477 (KPI Tracking OS Teams)
- OS-2249 (Move all Ops Teams to CF)

If Jira isn't connected, use the initiatives file and Notion as your backlog proxy, and note
in the plan that Jira should be checked for the actual ticket list before finalizing.

---

## Step 5: Draft the Sprint Plan

Now synthesize everything into a structured plan. Use this template exactly:

---

```markdown
# Sprint Plan — [Sprint Name or Number] · [Start Date] → [End Date]

## Sprint Goal
> [One sentence. Outcome-oriented, not task-oriented. "By end of sprint, [who] can [do what],
> which moves [metric] toward [target]." Make it concrete enough that on the last day of the
> sprint the team can unambiguously say yes or no to whether they hit it.]

## Quarter Alignment
This sprint serves the following Q1 outcomes:
- **[Outcome X.Y]**: [Current status] → [what this sprint does to move it]
- **[Outcome X.Y]**: ...

## Committed Work

### [Squad Name] Squad
| Jira Key | Title | Outcome | Why this sprint |
|----------|-------|---------|-----------------|
| OS-XXXX  | ...   | 2.1     | Unblocks 70% automation target |
| ...      |       |         |                 |

### [Squad Name] Squad
| Jira Key | Title | Outcome | Why this sprint |
|----------|-------|---------|-----------------|
| ...      |       |         |                 |

## Stretch Goals
*(Only if core is done. Do not sacrifice committed work for these.)*
- [ ] [Item] — rationale

## Explicitly Out of Scope This Sprint
*(Say this out loud so stakeholders don't assume it's coming.)*
- [Initiative/feature] — pushed because [reason]
- ...

## Risks & Watch Items
- **[Risk]**: [Mitigation or owner]
- ...

## How We'll Know This Sprint Succeeded
- [Specific, observable signal] — e.g., "document auto-classification live in staging with
  accuracy measured on 100 real docs"
- [Specific outcome metric movement] — e.g., "AURE auto-invoicing rate moves from 50% → 60%"
```

---

## Principles to apply when prioritizing

**P0 always goes in.** If something is a P0 in the outcomes framework (document processing,
KPI measurement, AURE auto-invoicing) and there's work to do on it, it belongs in the sprint.
Don't negotiate around P0.

**Blocks > features.** If something is blocking measurement of a P0 outcome, unblocking it
is more valuable than shipping a new feature. Builders who can't measure their impact are
flying blind.

**One squad, one focus.** Each squad should have a clear primary objective for the sprint.
Work that splits a squad's attention across two epics is a risk — flag it.

**Internal feedback is signal, not demand.** Items from the Notion board that are high-priority
belong in the plan if they align with quarterly outcomes. But don't let internal noise crowd
out outcome-driving work without a good reason.

**Sprint Goal is singular.** If you find yourself writing "and also", the sprint is
over-scoped. The Sprint Goal should describe the most important thing the team will achieve,
even if the sprint contains other work too.

**What's NOT in the sprint matters.** Explicitly calling out what won't be done builds trust
with stakeholders and protects the team from scope creep mid-sprint.

---

## Output format

Produce the sprint plan as a clean Markdown document. Save it to:
```
Product Management OS/.claude/product/sprints/sprint-[date]-plan.md
```

Then share it inline in the conversation as well so the user can read it immediately.

If you couldn't connect to Jira or Notion, note this clearly in a "⚠️ Data gaps" section at
the top and recommend the user verify specific ticket details manually before sharing the plan
with the squad.