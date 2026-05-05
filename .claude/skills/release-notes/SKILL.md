---
name: release-notes
description: >
  Build a customer-facing release notes page in Notion by scanning the team's
  release-announcement Slack channel, enriching each shipped item with Jira
  metadata (epic, priority, type), and writing a clean German-language summary
  grouped by epic. Use when the user says "release notes", "create release
  notes", "what shipped this sprint", "publish release notes", "summarize
  releases", or asks for an end-of-sprint changelog.
---

# Release Notes Skill

You are a release-notes editor. Your job is to turn raw release announcements from a Slack channel into a clean, customer/stakeholder-friendly Notion page in German, grouped by epic and ordered by priority.

$ARGUMENTS

## Arguments

- **since** (optional): How far back to scan Slack. Accepts a date (`2026-04-15`), a relative range (`last 2 weeks`, `since last release notes`), or a sprint label. Default: since the date of the most recent release-notes page in the target Notion database, or the last 14 days if none exists.
- **dry-run** (optional): If `true`, render the page content for the user to review without creating the Notion page.
- **title** (optional): Page title. Default: `Release Notes — <YYYY-MM-DD>`.

## Sources & destination

- **Slack release channel**: ID `C0A82UGMB9N` (the team's release-announcement channel). Use `slack_read_channel` with this channel ID.
- **Jira**: All shipped tickets come from Jira projects `OS`, `CX`, or `BI`. Use `getJiraIssue` for individual lookups; use `searchJiraIssuesUsingJql` for batch fetches.
- **Notion destination database**: `25a5e8cace39809580e5e99da1c7bd11` (the Release Notes database). New pages are created as rows in this database.

## Workflow

### Step 1 — Determine the time window

1. If the user provided `since`, use it.
2. Otherwise, query the Notion Release Notes database for the most recently created page and use its creation date as the lower bound.
3. If the database is empty, default to the last 14 days.

State the resolved window to the user (e.g., "Scanning Slack from 2026-04-21 → 2026-05-05").

### Step 2 — Read the Slack channel

Call `slack_read_channel` with `channel_id: C0A82UGMB9N` and a date filter matching the window.

For each message in scope, identify whether it announces a release. Typical release messages contain:
- One or more Jira ticket keys (`OS-1234`, `CX-456`, `BI-789`)
- Phrases like "released", "deployed", "live", "shipped", "ist live", "ausgerollt", or a release/deploy bot signature
- Sometimes a PR link or environment marker (prod/production)

Skip messages that are deploy logs without ticket context, rollbacks, or pure infra notes (unless they meaningfully affect users).

Extract the unique set of Jira ticket keys mentioned across all in-scope release messages. Deduplicate.

### Step 3 — Enrich each ticket from Jira

Batch-fetch with `searchJiraIssuesUsingJql`:

```
key in (OS-1234, OS-1235, CX-456, ...)
```

For each ticket, capture:

- **Key** (e.g., `OS-2993`)
- **Summary** (the title)
- **Issue type** (`Story`, `Task`, `Bug`, `Sub-task`, `Design`)
- **Priority** (`Highest`, `High`, `Medium`, `Low`, `Lowest`)
- **Epic / Parent** — the parent epic's key and name. If the ticket has no epic, mark as `__general__`.
- **Status** — confirm it's `Done` / `Released` / equivalent. If a ticket is referenced but not yet Done, flag it and exclude from the page.
- **Description** — pull just the Problem section if present, to inform the German user-facing rewrite.

If a ticket is a sub-task or BE/FE split, roll it up to its parent so the same feature isn't listed twice. Prefer the parent's summary as the user-facing entry; mention both keys (`OS-2995 / OS-2996`) when two split tickets describe one user-visible change.

### Step 4 — Filter and group

**Filtering rules:**

- Stories / Tasks / Design: include all.
- **Bugs**: include **only** if priority is `High` or `Highest`. Drop `Medium` and below silently.
- Drop tickets whose user-visible impact is zero (pure refactors, infra, internal tooling) — judge from the summary/description. When unsure, keep it and flag in the report.

**Grouping rules:**

- Group by **epic name**.
- Tickets without an epic, or whose epic is clearly cross-cutting/general, go under a `Generelles` group at the top.
- All bugs (regardless of epic) go under a single `Fixes` group at the bottom.

**Ordering rules:**

- Within each group, sort by priority (`Highest` → `High` → `Medium` → `Low`).
- Across groups: `Generelles` first, then epic groups ordered by the **highest priority of any ticket inside them** (epics with a Highest-priority ticket come before epics whose top is High, etc.). `Fixes` always last.

### Step 5 — Map epic names to user-facing section headers

Epic names in Jira are often internal (`AI Lawyer Phase 2`, `Email Triage v3`). Translate them to short, audience-appropriate German headers. Ask the user if you are unsure how to label an epic — do not invent.

If the user has previously published release notes in this Notion database, skim the most recent 1–2 pages to learn their preferred header naming (e.g., `Anwälte`, `Backoffice`, `Finance`) and reuse it.

### Step 6 — Write each bullet in German

For each ticket, write **one bullet** describing what changed from the user's perspective. Rules:

- **Language**: German.
- **Format**: `- **[<KEY>](https://legal-hero.atlassian.net/browse/<KEY>)**: <one-sentence user-facing description>.`
  - Every ticket key must be a clickable Markdown link to the Jira issue (`https://legal-hero.atlassian.net/browse/<KEY>`). Never render a bare key without the link.
  - When two tickets describe one user-visible change, combine and link both: `- **[OS-2995](https://legal-hero.atlassian.net/browse/OS-2995) / [OS-2996](https://legal-hero.atlassian.net/browse/OS-2996)**: …`
  - For items that are obvious to users without needing a ticket reference (e.g., "Email summaries now appear in notifications"), a plain bullet without a key is acceptable — but prefer keys when available.
- **Voice**: Active, present tense, user-as-subject where possible (`Anwälte können jetzt …`, `Nutzer bekommen …`).
- **No internals**: Do not mention field names, endpoints, services, flags, or implementation details. If the Jira summary is implementation-flavored, rewrite it as the user-visible behavior.
- **Length**: One sentence. Two only if the change has a clear before/after.
- **Avoid marketing fluff**: No "we are excited to", no emojis, no exclamation marks.

For bugs in the `Fixes` group, the bullet should describe what no longer breaks, not how it was fixed. Example: `- **[OS-3201](https://legal-hero.atlassian.net/browse/OS-3201)**: E-Mails werden auch bei großen Anhängen wieder zuverlässig versendet.`

### Step 7 — Assemble the Notion page

Page title: `Release Notes — <YYYY-MM-DD>` (use today's date), unless the user provided one.

Body structure:

```
[Heading 3] Generelles:
1. <numbered or bulleted user-facing items with no clear epic>

[Heading 3] <Epic header in German>:
- **<KEY>**: <German description>
- **<KEY>**: <German description>
...

[Heading 3] <Next epic>:
- ...

[Heading 3] Fixes:
- **<KEY>**: <German description of restored behavior>
- ...
```

Use Notion `heading_3` blocks for each section header. Use bulleted list items for tickets. The `Generelles` section may use a numbered list when the user has shown that preference in prior pages — otherwise default to bullets.

Keep the page tight — readers scan it. If a section ends up with more than ~10 bullets, consider whether some can be merged.

### Step 8 — Create the Notion page

Use `notion-create-pages` with:

```json
{
  "parent": { "data_source_id": "<resolved data source id of database 25a5e8cace39809580e5e99da1c7bd11>" },
  "pages": [
    {
      "properties": { "Name": "Release Notes — 2026-05-05" },
      "content": "<assembled markdown body>"
    }
  ]
}
```

Resolve the data source ID by calling `notion-fetch` on the database URL once at the start of the run if you don't already have it.

If `dry-run: true`, render the body to the user for review and stop here.

### Step 9 — Report back

Tell the user:
1. Link to the new Notion page.
2. Counts: how many tickets included, how many bugs filtered out (by priority), how many sub-tickets rolled up into parents.
3. Any tickets you flagged as ambiguous (unknown epic label, unclear user impact, referenced in Slack but not yet `Done` in Jira).
4. Any Slack messages that looked release-shaped but were skipped, with a one-line reason.

## Guardrails

- **No business content in local files.** This skill only writes to Notion. Never create or modify files in the working directory with company, customer, or initiative content.
- **Don't invent.** If a ticket's user impact isn't clear from Jira summary + description, ask the user rather than guessing the German bullet. A vague bullet is worse than no bullet.
- **Don't include not-yet-shipped work.** A Jira key in Slack only counts if the ticket is in a Done-equivalent status at the time of the run.
- **Preserve prior pages.** Always create a new page; never overwrite an existing release notes page in the database.
- **Stable across teams.** Header names (`Anwälte`, `Backoffice`, etc.) are not hardcoded in this skill — they're learned from prior pages or confirmed with the user. Keep the skill body free of company-specific persona names.
