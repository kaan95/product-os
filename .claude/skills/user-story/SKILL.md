---
name: user-story
description: Create a well-structured user story or bug ticket in Jira based on provided input.
---

# Create User Story or Bug

Generate a well-structured ticket based on the following input:

$ARGUMENTS

## Arguments

The user may provide the following optional arguments:

- **Sprint**: The sprint to assign the ticket to (e.g., "Sprint 30")
- **Project**: The Jira project key (e.g., "OS"). Default: OS
- **Priority**: The priority level. Options: highest, high, medium, low. Default: medium
- **Type**: `feature` (default) or `bug`. Infer from the input if not specified (e.g. "fix", "broken", "error" → bug).
- **URL** (`--url <url>`): A URL to screenshot for use as evidence (bug tickets only). If provided, a screenshot is captured before the ticket is written.

## Step 1 — Playwright evidence capture (if --url provided)

If the user passes `--url <url>`, capture a screenshot **before** writing the ticket:

1. Run via Bash:
   ```
   npx playwright screenshot --full-page "<url>" /tmp/evidence-$(date +%s).png 2>&1
   ```
2. **If Playwright is not installed** (`npx playwright` errors or is not found):
   - Run `npm install -g playwright` and retry once.
   - If it still fails, skip silently and note in the Evidence section: `Screenshot: could not be captured — Playwright not available.`
3. **If the screenshot succeeds**, display the image to the user using the Read tool so they can confirm it captured the right state.
4. Save the full path of the screenshot file — you will reference it in the `## Evidence` section of the ticket body as:
   `Screenshot: <path> — attach to this ticket manually.`
5. Do **not** block ticket creation on screenshot success or failure. Evidence capture is best-effort.

## Step 2 — Classify and gather context

Before writing anything, classify the ticket as **feature** or **bug** and check whether you have enough information to make it executable for a developer.

### For a bug, you must have:
- A reproducible trigger (endpoint, UI action, or event)
- At least one concrete example input (anonymized if sensitive)
- The observed error (status code, error message, Sentry/log link, or screenshot)
- Environment (prod / staging / local)
- Impact (who is affected, is there a workaround, is the flow fully blocked)

### For a feature, you must have:
- The user/persona (a human role — never "the backend", "the system")
- The concrete goal they're trying to achieve
- The benefit / outcome
- Enough scope clarity to write testable ACs

**If required information is missing, ASK the user for it. Do not speculate, and do not invent plausible-sounding root causes, behaviors, or payloads.** Phrases like "appears to be", "may be caused by", "likely" are a signal you are guessing — stop and ask instead.

## Step 3 — Structure the ticket

### Bug template

```
## Problem
[1–3 sentences: what is broken, who is affected, what is the business impact. State facts only.]

## Steps to Reproduce
1. [concrete step]
2. [concrete step]
3. ...

## Expected Behavior
[what should happen]

## Actual Behavior
[what happens instead, including error message / status code / stack trace excerpt]

## Evidence
- Sentry: [link]
- Logs / screenshots / example payload: [link or snippet]
- Environment: [prod / staging / local]

## Scope
- In scope: [what this ticket covers]
- Out of scope: [what this ticket does NOT cover, to prevent drift]

## Acceptance Criteria
[2–5 testable ACs — see rules below]
```

### Feature template

```
## Problem
[Why this matters — the user pain or business need. Not a solution description.]

## User Story
As a [human persona],
I want [goal],
So that [benefit].

## Scope
- In scope: [what this ticket covers]
- Out of scope: [what this ticket does NOT cover]

## Acceptance Criteria
[2–5 testable ACs — see rules below]
```

### Problem statement quality bar

The **Problem** section is the most-misused part of a ticket. The default failure mode is to write a *task description* ("this ticket exists to…") or a *solution description* ("add field X that does Y") — neither of which tells anyone *who hurts and why*.

A strong problem statement:

- ✅ Names the persona and their observable pain
- ✅ Describes the business consequence of *not* solving it (revenue, retention, compliance, NPS, ops cost)
- ✅ Reads as a fact about the world, not a description of the ticket

A weak problem statement does any of these:

- ❌ Names a specific value, threshold, field name, or endpoint — those belong in AC
- ❌ Recounts decision history ("finalised on date X, superseding Y")
- ❌ Frames the ticket as "this ticket exists to verify / lock in / configure…"
- ❌ Describes the solution (the *what*) instead of the pain (the *why*)
- ❌ Is written from a dev/internal perspective ("move job X to pipeline Y") with no user or business value visible

**Self-reflection before submitting**: re-read the Problem section in isolation. If a developer read *only* this section, would they understand who is in pain and why it matters — without learning anything about the implementation? If not, rewrite.

For paired before/after examples, see [references/problem_statement_examples.md](references/problem_statement_examples.md).

## Step 4 — Acceptance Criteria rules

Use the Given/When/Then format with a short title per AC:

```
**AC1: [Title]**
- Given: [precondition]
- When: [action]
- Then: [observable, verifiable outcome]
```

**Each AC must:**
- Be verifiable by a single action a QA or automated test can perform.
- Describe an observable outcome (response, UI state, side effect), not an internal process.

**Do NOT write ACs like:**
- "Root cause identified and fixed" — not testable, just restates the task.
- "No regression in existing flows" — belongs in the team's Definition of Done, not per-ticket ACs.
- "Code is reviewed / documented / deployed" — process, not outcome.

Keep it to **2–5 ACs maximum**. If you find yourself writing more, the ticket is too big — split it.

## Step 5 — Create the ticket in Jira

1. Always write in English.
2. Always create the ticket directly in Jira (don't draft to the user for approval unless something is ambiguous).
3. Use the specified project key, or default to **OS**.
4. If a sprint is specified: look up the sprint ID first via JQL `project = OS AND sprint = "Sprint X"`, then set the numeric sprint ID in `customfield_10020`.
5. If a priority is specified, set it via `additional_fields`.
6. For bugs, use issue type **Bug**. For features, use **Story**.
7. After creating, transition to **Open** using `getTransitionsForJiraIssue` and `transitionJiraIssue`.
8. Return the URL to the user.

## Step 6 — BE / FE / Design splitting

**Split only when both layers genuinely need work.** A pure API bug, a pure UI copy change, or a backend-only refactor should be **one ticket**, not two.

- Backend-only ticket: prefix `BE - `
- Frontend-only ticket: prefix `FE - `
- Both layers needed: create one `BE - ` and one `FE - ` ticket, link them with a "Blocks" issue link (BE blocks FE).
- If ambiguous, ask the user before splitting.

### Design tickets

When creating a FE ticket, judge whether a Design ticket is also needed:
- **Yes** for: new UI components, new flows, significant visual changes.
- **No** for: minor changes like disabling a button, showing an existing toast, copy tweaks.

If yes:
- Create the Design ticket in the **same project** as the FE ticket (OS, CF, or CX — never UX).
- Issue type: **Design**.
- Assignee: **Katharina Treptow** (`712020:2c26d4fe-2a9e-4876-9e74-7e7311a8112d`).
- Link as a blocker of the FE ticket ("FE ticket blocked by Design").
- Inform the user that a Design ticket was created.

## Step 7 — Link related context

If the user references a parent initiative, the original feature ticket that introduced the bug, or a related ticket, link it with `createIssueLink` using an appropriate link type ("Relates to" for context, "Blocks" for hard dependencies).
