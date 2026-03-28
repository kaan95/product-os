---
name: weekly-todo-sweep
description: Scan last week's Notion meeting notes and Gmail inbox, extract action items / to-dos, and add them to the Notion To Do's database. Use when the user says "sweep todos", "extract action items", "weekly todo sweep", "check meetings for todos", or "process my meetings".
---

# Weekly To-Do Sweep

Extract action items from last week's Notion meeting notes (and optionally Gmail inbox) and add them to the Notion To Do's database.

$ARGUMENTS

## Arguments

- **weeks** (optional): How many weeks back to scan. Default: 1.
- **dry-run** (optional): If "true", list found to-dos without creating them in Notion.

## Data Sources

### Notion Meeting Notes
Query the user's meeting notes from the past week using the `notion-query-meeting-notes` tool.

### Gmail Inbox
**Not yet available.** Requires a Gmail MCP server to be configured. When available, scan the inbox for emails containing action items, follow-ups, or explicit requests directed at the user. Skip newsletters, notifications, and automated emails.

## To Do's Database

- **Database URL**: `https://www.notion.so/9c05abda3cb04e7c92ed87cf2cc52ab6`
- **Data Source ID**: `1ae473db-1642-4a39-97da-76b2aa1d060e`

### Schema (relevant properties)

| Property | Type | Valid Values |
|---|---|---|
| Name | title | Free text — concise, actionable task name |
| Status | status | `Inbox`, `Next`, `Doing`, `Blocked`, `Done` |
| Category | select | `📊 Outcomes`, `🔍 Discovery`, `🚢 Delivery`, `👤 Stakeholder Request`, `🪄 Product`, `♠️ Strategy` |
| Due Date | date | ISO-8601 date |
| Initiative | select | `AI Lawyer`, `Premium Package` |
| User Group | select | `Finance`, `BI`, `Lawyer` |
| Priority | select | `Highest`, `High`, `Medium`, `Low` |

## Workflow

### Step 1 — Fetch meetings from the past week

Use `notion-query-meeting-notes` with a date filter for the past week (or N weeks if specified):

```json
{
  "filter": {
    "operator": "and",
    "filters": [
      {
        "property": "created_time",
        "filter": {
          "operator": "date_is_within",
          "value": { "type": "relative", "value": "the_past_week" }
        }
      }
    ]
  }
}
```

If `weeks` > 1, use a custom relative filter with `"unit": "week", "count": <weeks>`.

### Step 2 — Fetch each meeting's content

For each meeting returned, use `notion-fetch` with the meeting's page ID to get the full content including summaries and action items.

### Step 3 — Extract action items

From each meeting, extract:
- Explicit action items (marked with `- [ ]` or listed under "Action Items")
- Decisions that imply follow-up work
- Commitments made by the user (look for "Kaan" as the owner)
- Deadlines or timelines mentioned

For each action item, determine:
1. **Name**: A concise, actionable task title (start with a verb)
2. **Due Date**: Extract from context. If a relative date like "next week" or "in 2 weeks" is mentioned, convert to absolute date based on the meeting date. If no date mentioned, leave empty.
3. **Category**: Map based on context:
   - Technical integration, development, API work → `🚢 Delivery`
   - Research, user interviews, data analysis → `🔍 Discovery`
   - Metrics, KPIs, reporting → `📊 Outcomes`
   - Request from stakeholder/partner → `👤 Stakeholder Request`
   - Product specs, PRDs, roadmap → `🪄 Product`
   - Strategy discussions, market positioning → `♠️ Strategy`
4. **Initiative**: Only set if clearly related to `AI Lawyer` or `Premium Package`. Otherwise leave empty.
5. **User Group**: Only set if clearly related to `Finance`, `BI`, or `Lawyer`. Otherwise leave empty.
6. **Priority**: Infer from urgency signals. Default to `Medium` if unclear.

### Step 4 — Deduplicate

Before creating, query existing to-dos in the database to avoid duplicates. Use `notion-search` with the data source URL to check for similar task names.

### Step 5 — Present findings to user

Display a table of all extracted to-dos with their proposed properties:

```
| # | Name | Source Meeting | Due Date | Category | Initiative | User Group | Priority |
|---|------|---------------|----------|----------|------------|------------|----------|
```

If `dry-run` is "true", stop here.

### Step 6 — Create to-dos in Notion

After user confirmation, use `notion-create-pages` to create all to-dos:

```json
{
  "parent": { "data_source_id": "1ae473db-1642-4a39-97da-76b2aa1d060e" },
  "pages": [
    {
      "properties": {
        "Name": "Task name here",
        "Status": "Inbox",
        "Category": "🚢 Delivery",
        "Priority": "Medium",
        "date:Due Date:start": "2026-03-20",
        "date:Due Date:is_datetime": 0
      }
    }
  ]
}
```

- Always set Status to `Inbox` for new items.
- Batch create all pages in a single `notion-create-pages` call (up to 100).
- Only set Initiative and User Group if confidently identified.

### Step 7 — Confirm

Report back:
1. Number of to-dos created
2. Link to the To Do's database view: `https://www.notion.so/9c05abda3cb04e7c92ed87cf2cc52ab6?v=3025e8cace39809eab1e000ce826682b`
3. Any items skipped as duplicates

## Gmail (Future)

When a Gmail MCP server is available, add a step between Step 1 and Step 2:
- Search inbox for emails from the past week
- Filter for emails that contain action-oriented language (requests, follow-ups, deadlines)
- Extract to-dos using the same property mapping logic
- Mark the source as "Gmail" instead of the meeting name
