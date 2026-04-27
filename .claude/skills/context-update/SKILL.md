---
name: context-update
description: >
  Harvest context from Notion and/or Slack and write it back to the initiative's page in the Notion "Product Initiatives" database.
  Use this skill whenever the user wants to update initiative context, capture meeting notes, pull decisions or learnings from Slack, or keep an initiative's Notion page in sync with what's happening in conversations and meetings.
  Trigger phrases: "update context", "sync context", "add this meeting to context", "pull context from Notion", "update initiative docs", "capture what we discussed", "add the Slack thread to context", "context update for [initiative]".
  Always use this skill when the user references an initiative AND a Notion link, Slack channel, or thread they want to incorporate.
---

# Context Update Skill

You are a context harvester for product initiatives. Your job is to read information from live sources — Notion meeting notes and Slack channels/threads — and distill it into the initiative's page in the Notion **Product Initiatives** database.

The initiative's Notion page is the single source of truth for "what's happening now". Other skills (sprint planning, stakeholder updates, PRD writing) should read it from there. Keep it dense with signal, free of noise.

**Important: this skill must never write business, customer, stakeholder, or initiative content into local files.** All such content lives in Notion. The skill itself stays free of company-specific identifiers so it ports cleanly to other contexts.

---

## Step 1: Understand the request

Determine from the user's message:

- **Initiative name** — which initiative this context belongs to
- **Sources** — what to pull from:
  - A Notion page URL or page title (meeting notes, decision log, research doc)
  - A Slack channel name for recent messages
  - A Slack thread URL or description

If any of these are missing and the user's intent isn't clear, ask. One question at a time.

---

## Step 2: Locate the initiative page in Notion

The destination is the **Product Initiatives** database:
`collection://32f5e8ca-ce39-80d7-ad58-000b9fa65b14`

1. Query the database by `Name` (case-insensitive substring match) to find the initiative's page.
2. If exactly one match is found, use that page.
3. If multiple match, list them and ask the user to pick.
4. If no match is found, ask the user to confirm before creating a new page in the database. When creating, populate at minimum: `Name`, `Quarter`, `Assigned Team`, `Status` (default `Not started`).

Always fetch the existing page body before writing, so you understand what's already captured.

---

## Step 3: Fetch from sources

### From Notion

Use the Notion MCP to fetch the provided page. Extract:
- Concrete decisions that affect the initiative
- Open questions or unresolved issues
- New learnings, validated/invalidated assumptions
- Action items with owners

Capture the **block-level link** to each item (Notion supports per-block URLs) so each entry can be traced back to its origin.

### From Slack

**If the user provides a channel name**: search and read recent messages (last 7–14 days unless specified). To suppress noise, only ingest threads that meet at least one of:
- ≥3 replies, OR
- contains a decision/blocker keyword (e.g., "decided", "agreed", "blocked", "next step", "action", "owner")

**If the user provides a thread URL or description**: read that thread end-to-end.

For each item kept, capture the **Slack message permalink** as the source.

---

## Step 4: Synthesize and write to the Notion page

Don't paste raw notes. Distill — extract signal, drop noise. For each item, ask: *Does this change what someone needs to know about this initiative to make good decisions?* If yes, include it; if it's logistics or tangent, skip it.

### Page body structure

The initiative page should follow this section structure (use native Notion blocks where possible: callouts, to-dos, toggles).

```
[Callout] Overview
  2–4 sentences: what the initiative is, why it exists, current status.
  Update this when direction or status meaningfully shifts.

[Heading 2] Key Decisions
  Bulleted list. Each entry:
  • YYYY-MM-DD — <decision> — <one-line rationale> — [source link]

[Heading 2] Open Questions & Blockers
  To-do blocks (so they're checkable in Notion). Each entry:
  ☐ <question or blocker> — raised YYYY-MM-DD — [source link]

  When resolved: check the box AND move the resolution to Key Decisions
  if it represents a real decision. Archive checked items into the
  "Resolved" toggle after 2 weeks.

[Heading 2] Insights & Learnings
  Bulleted list. Each entry:
  • YYYY-MM-DD — <what was learned/validated/invalidated> — [source link]

[Heading 2] Action Items
  To-do blocks. Each entry:
  ☐ <task> — owner: <name> — due: <date if known> — [source link]

  Mark done in Notion as items complete. Archive done items into the
  "Completed" toggle after 2 weeks.

[Toggle, collapsed] Update Log
  • YYYY-MM-DD — <source> — <one-line summary of what was added>
```

### Section size budgets (not file size)

- Open Questions: max ~10 active. If more, the initiative is too broad — flag to the user.
- Action Items: max ~15 active. Older items get archived into the toggle.
- Update Log: keep all entries; the toggle keeps it out of sight.

---

## Step 5: Update, don't overwrite

When updating an existing page:

- **Append** new decisions, insights, questions, action items.
- **Update** the Overview if direction or status has meaningfully changed.
- **Add a row** to the Update Log for every run of this skill.
- **Deduplicate**: match new items against existing ones by normalized text (lowercase, first 60 chars). If matched, update in place (e.g., add a newer source link, mark resolved); else append.
- **Never delete** a user's hand-written content. Only modify content this skill previously added.

The page is an accumulating, self-maintaining document. Every run should make it more useful — not longer and noisier.

---

## Step 6: Confirm and report

After writing, tell the user:
- Which Notion page was updated (with link) — or created
- What was added (e.g., "2 decisions from the Notion meeting, 3 open questions from Slack, 4 action items")
- What was **intentionally dropped as noise** (1-line examples — sanity check on the distillation)
- Anything you couldn't extract clearly or had to skip
- Any stale-looking action items or open questions that might need user review

---

## Guardrails

- **No local writes of business content.** This skill must not create or modify any file under the working directory that contains initiative, customer, stakeholder, or decision content. All such content goes to Notion. If you find yourself about to write a `.md` file with business specifics, stop — that violates the portability principle.
- If the Notion DB query or Slack fetch errors or returns empty, tell the user and continue with whatever sources are available.
- Don't add speculation or interpretation — only things actually said or decided. If a decision is implied but not stated, list it under Open Questions, not Key Decisions.
- For ambiguous initiative matches, always confirm with the user before writing.
- Source links are required for every entry. If you can't get a link, note `<source: Notion meeting>` or `<source: Slack #channel>` as a fallback, but flag it in the report.
