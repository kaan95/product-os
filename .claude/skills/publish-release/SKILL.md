---
name: publish-release
description: >
  Orchestrator that publishes release notes AND updates the changelog on every
  affected initiative's Notion page in one go. Use when the user says "publish
  release", "ship release notes and update initiatives", "end-of-sprint
  publish", or wants the release-notes + initiative-changelog flow chained
  together. Do NOT use this when the user only wants release notes (use
  release-notes directly) or only wants to refresh one initiative (use
  context-update directly).
---

# Publish Release Orchestrator

You are a workflow runner. Your only job is to chain two existing skills with a clean handoff between them:

1. **release-notes** — produces a published Notion release notes page and the structured list of shipped items grouped by epic.
2. **context-update** — appends a changelog entry to each affected initiative's Notion page, using the release notes page as the source link.

You do not re-implement either skill. You invoke them, carry the handoff payload between them, and report the combined result.

---

## Step 1 — Run release-notes

Invoke the **release-notes** skill, passing through any arguments the user gave (`since`, `dry-run`, `title`).

Wait for it to complete. From its output, capture:

- **release_page_url** — the URL of the new Notion release notes page (or the rendered body if `dry-run: true`)
- **release_date** — the date used in the page title (today, unless overridden)
- **groups** — the epic-grouped structure that was published. For each group, you need:
  - `epic_name` — the original Jira epic name (NOT the German user-facing header)
  - `header_de` — the German user-facing header that was used on the release notes page
  - `bullets` — the exact German bullets that were published, with their Jira links intact
- Special groups:
  - The `Generelles` group has no epic and is **skipped** by this orchestrator (no initiative to update).
  - The `Fixes` group is grouped by epic *under the hood* — split it back out by each bug's parent epic before handoff. Bugs whose parent epic has no matching initiative are dropped from the orchestrator's scope (they still appear on the public release notes page).

If `dry-run: true` was passed, **stop after release-notes completes** and report what would have been pushed to which initiatives. Do not call context-update in dry-run.

If release-notes errors or produces no shipped items, stop and report that. Do not proceed.

---

## Step 2 — Map epics to initiatives

For each `epic_name` from Step 1:

1. Query the Notion **Product Initiatives** database (`collection://32f5e8ca-ce39-80d7-ad58-000b9fa65b14`) for a page whose `Name`, `Epic`, or linked-epic property matches the Jira epic name.
2. If exactly one match is found, use it.
3. If multiple match, list them and ask the user to pick (one prompt covering all ambiguous epics, not one per epic).
4. If no match is found, **skip that epic** and add it to the unmapped list reported at the end. Do not create new initiatives from this skill.

Build a list of `(initiative_page, header_de, bullets)` tuples to hand off.

---

## Step 3 — Run context-update for each affected initiative

For each tuple from Step 2, invoke the **context-update** skill with an explicit payload rather than a free-form ask, so the child skill doesn't re-fetch Slack/Notion sources:

> "Append a changelog entry to initiative `<page title>` (page id `<id>`) under a `🚀 Shipped` section. Source: `<release_page_url>`. Date: `<release_date>`. Items:
> - <bullet 1 verbatim from release notes, including the Jira link>
> - <bullet 2 …>
>
> Do not re-fetch Slack or Notion. This is a direct write from the publish-release orchestrator. Add one Update Log row: `<release_date> — Release Notes — <N> items shipped`. Do not modify Overview, Open Questions, or To Do's."

Notes:

- The `🚀 Shipped` section is reverse-chronological: newest release at the top.
- If the section doesn't exist on the initiative page yet, context-update creates it (as a `Heading 2`).
- Bullets are appended verbatim — same German wording, same Jira links — so the initiative page mirrors the public release notes page exactly for those items.
- Run initiatives **sequentially**, not in parallel. One initiative may have edits from a prior step that the next needs to read; sequential keeps the audit trail clean.

If context-update fails for one initiative, log the failure and continue with the rest. Do not abort the whole orchestrator.

---

## Step 4 — Report

A single combined report at the end:

1. **Release notes page**: link.
2. **Initiatives updated**: bulleted list of `<initiative name> — <N> items appended` with page links.
3. **Epics with no matching initiative**: list, so the user can decide whether to create one.
4. **Failures**: any initiative where context-update errored, with the error.
5. **Counts carried over from release-notes**: tickets included, bugs filtered, sub-tickets rolled up (so the user gets one report, not two).

---

## Guardrails

- **No business content in local files.** This orchestrator only triggers other skills; it never writes initiative, customer, or stakeholder content into the working directory.
- **No re-implementation.** Anything about Slack scanning, Jira enrichment, German bullet writing, or Notion page structure belongs in the child skills — not here. If you find yourself adding logic of that kind to this file, that's a smell.
- **Don't widen scope.** Only the two child skills run. Don't kick off sprint-planner, weekly-todo-sweep, or anything else from here unless the user explicitly extends the workflow.
- **Idempotency awareness.** If the user re-runs publish-release for the same window, release-notes will create a second page and context-update will append duplicate Shipped entries. Detect this: if a release notes page already exists for `<release_date>`, ask the user whether to skip, replace, or proceed before running.
