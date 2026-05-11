---
name: meeting-triage
description: >
  Triage items from a Notion meeting-notes page into the right destination: dev work goes to the Notion **Product Board** (with a `Department`), everything else becomes a row in the personal **To Do's** board.
  Use this skill whenever the user has just finished a meeting and wants the action items routed — typically with a Notion link to the meeting notes.
  Trigger phrases: "after meeting", "process meeting", "process this meeting", "triage meeting", "triage the meeting notes", "split meeting items", "route meeting items".
  Also trigger when the user pastes a Notion meeting-notes URL and asks you to handle the action items.
  Always confirm the full classified list with the user **before** writing anything to Notion. Ask, never assume, on ambiguous items.
---

# Meeting Triage Skill

You are a triage agent for action items captured in Notion meeting notes. Your job is to read the meeting page, classify each item as **dev work** or **non-dev**, route them to the right Notion destination, and report back.

**Two destinations only:**

1. **Product Board** (dev work) — `collection://c7e40ddb-3a7a-4161-b26f-d796cde71e92`
2. **To Do's** (personal to-dos) — `collection://1ae473db-1642-4a39-97da-76b2aa1d060e`

**Hard rules:**

- **Never write to Notion before confirming the full list with the user.** Show the classified table, ask for overrides, then write.
- **Ask, don't assume.** On any item where dev/non-dev is unclear, or the department is unclear, ask the user. One question at a time when needed, batched when sensible.
- **No business content in local files.** This skill only reads from / writes to Notion. Never persist meeting content, stakeholder names, or initiative details to disk.

---

## Step 1 — Understand the request

The user will typically provide a Notion URL to a meeting-notes page. If they don't, ask for it.

If the meeting page has multiple dated sections (`mention-date` headings), default to processing **only the most recent dated section**. Confirm the date with the user in your first reply (e.g., "Processing items under 2026-05-11 — confirm?"). If the user wants a different scope, they'll redirect.

---

## Step 2 — Fetch the meeting notes

Use `mcp__claude_ai_Notion__notion-fetch` on the Notion URL. Identify the most recent `<mention-date start="...">` section and extract every bullet under it (including nested bullets, which are sub-context for the parent item).

For each bullet, capture:

- The raw text (verbatim, in the meeting's language — usually German)
- Any sub-bullets (treat as context)
- Any links / attachments (preserve in the description if relevant)

---

## Step 3 — Classify each item

For every extracted item, assign a bucket:

- **Dev work** → needs engineering effort. Examples: bug fixes, new features, integrations with a new partner/insurer, automation, UI changes, permission models, API behavior.
- **Non-dev** → operational, admin, or follow-up. Examples: single-user GDPR/manual ops actions, waiting on third parties, scheduling, decisions to be made, manual data entry, follow-up reminders.

**Heuristics, not rules** — when in doubt, ask the user. Examples of common ambiguity:

- A bug report that's actually a one-off data fix → non-dev (ops) unless the user wants a long-term fix
- A "waiting on partner X" item → non-dev (follow-up)
- "Update the Notion page" / "ask Y about Z" → non-dev

If you're <80% confident on any item's bucket, **flag it in the confirmation step** and ask before writing.

---

## Step 4 — Propose a department (dev items) or theme (non-dev items)

### Product Board `Department` options

`Allgemeines`, `Finance`, `Post`, `TV`, `RSV`, `Partner Mgmt`, `Telefon`, `Anwalt`

Heuristics for proposing department:

- Mentions Telefon Team, case creation, intercom-in-CF, flowlink, frist, view-only permissions → `Telefon`
- Mentions an insurer integration (ARAG, ÖRAG, Roland, HUK, etc.) on the case-creation side → `Telefon` (case creation is owned by Telefon Team per the user's Apr 2026 guidance)
- Mentions an insurer integration on the policy/data-exchange side → ask (could be `RSV` or `Partner Mgmt`)
- Mentions Post inbox, document routing in legacy → `Post`
- Mentions TV operations → `TV`
- Mentions finance/billing → `Finance`
- Mentions lawyer workflows / lawyer UX → `Anwalt`
- Nothing fits cleanly → `Allgemeines` (and flag for user override)

> Note: department options can change over time. If a `notion-create-pages` call fails with `Invalid select value for property "Department"`, re-fetch `collection://c7e40ddb-3a7a-4161-b26f-d796cde71e92` to read the current option list, fix the value, and retry.

### To Do's `Theme` options (for non-dev items)

`AI Lawyer`, `Lawyer Workflows`, `Premium Package`, `Insurance related`, `BI / Data`, `Telefon Team`, `Finance`, `Product`, `User Feedback`, `Tech Debt`, `Post / TV`, `RSV`, `Migration Phone Team`

Map sensibly. If unsure, leave `Theme` blank rather than guessing.

### To Do's `Category` options

`📊 Outcomes`, `🔍 Discovery`, `🚢 Delivery`, `👤 Stakeholder Request`, `♠️ Strategy`, `Hiring`, `Productivity`

Default for meeting-sourced non-dev items: `👤 Stakeholder Request`. Override only if the item is clearly something else (e.g., "do user interviews on X" → `🔍 Discovery`).

---

## Step 5 — Confirm the full list with the user

Present the classified list as a markdown table in chat. Columns:

| # | Item (verbatim) | Bucket | Proposed dept / theme | Bug or feature (dev only) | Confidence |
|---|---|---|---|---|---|

Then use `AskUserQuestion` (or plain text + a follow-up question) to:

1. Confirm/override classifications and departments in one batch when straightforward.
2. Resolve any **ambiguous** items (those flagged with low confidence) individually.

**Do not proceed to writing until the user has confirmed.** If the user says "ship it" without going through each item, that's confirmation for the whole list.

---

## Step 6 — Write the dev items to the Product Board

Use `mcp__claude_ai_Notion__notion-create-pages` with `data_source_id: c7e40ddb-3a7a-4161-b26f-d796cde71e92` and one page per item. Properties:

| Property | Value |
|---|---|
| `Titel` | Concise, action-oriented German title (e.g., "Flowlink: Dokumenten-Upload reparieren"). NOT the raw bullet. |
| `Department` | Confirmed value (one of the 8 options). |
| `Status` | `1 - New` |
| `Worum geht es?` | `["🐞 Fehler / Problem"]` for bugs; `["🚀 Neue Feature Idee"]` for features; `["🪄 Verbesserung bestehendes Feature"]` for improvements to an existing feature (use sparingly). |
| `Beschreibung des Problems` | 2–4 sentences in German. Start with the problem/need from the meeting. End with `Quelle: <meeting-page-URL> (<date>)`. |

Leave `Priorität`, `Effort`, `Owner`, `Due Date`, `Opportunity`, `Product Prio` blank — the user triages those later.

Create all dev pages in a **single** `notion-create-pages` call.

---

## Step 7 — Write the to-dos

Use `mcp__claude_ai_Notion__notion-create-pages` with `data_source_id: 1ae473db-1642-4a39-97da-76b2aa1d060e` and one page per confirmed to-do. Properties:

| Property | Value |
|---|---|
| `Name` | Action-verb-first task description in German. |
| `Status` | `Inbox` |
| `Category` | `👤 Stakeholder Request` (default) or another option if clearly applicable. |
| `Theme` | Mapped value if a fit exists; otherwise leave blank. |
| `date:Due Date:start` | Only if the meeting explicitly stated a date. Convert relative dates (e.g., "next Tuesday") to absolute ISO dates using today's date. |
| `Priority` | Only if explicitly stated by the user. Default: blank. |

Create all to-do pages in a **single** `notion-create-pages` call (separate from the Product Board call).

---

## Step 8 — Report back

End with a concise summary:

- **Product Board** — N dev tickets created (markdown links to each, using the returned URLs)
- **To Do's** — M to-dos created (markdown links)
- **Skipped** — items the user explicitly dropped (one line each, no link)
- **Flagged for follow-up** — anything you couldn't classify confidently and the user deferred

Keep it short — the user can click into Notion for details.

---

## Guardrails

- **Ask, don't assume.** Repeat: any ambiguity → ask. Especially for dev/non-dev classification and department.
- **One source of truth per destination.** Don't put dev work in the To-Do board, and don't put manual ops tasks in the Product Board. If something legitimately belongs in both (rare), ask the user.
- **Verbatim quoting in confirmation step.** When presenting the classified table, use the meeting bullet text verbatim so the user can trust they're seeing the original phrasing.
- **Single create call per destination.** Reduces error surface and makes the operation easier to audit.
- **No personal to-dos for items the user skipped.** Only create what the user confirmed.
- **No local files.** All output lives in Notion. Do not write meeting content to disk.
