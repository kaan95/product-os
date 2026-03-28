---
name: rice-score-sync
description: Sync RICE scores from the Jira Product Discovery (PD) board to connected delivery issues.
---

# RICE Score Sync

Sync RICE scores from the Jira Product Discovery (PD) board to connected delivery issues in the OS project.

$ARGUMENTS

## Arguments

The user may provide the following optional arguments:

- **Dry Run**: If "yes", only calculate and display RICE scores without updating delivery issues. Default: no
- **Filter**: Optional JQL filter to narrow down PD items (e.g., status = "In Progress"). Default: none (all Features and Improvements)

## Instructions

### Overview

This skill fetches all Features and Improvements from the PD (Product Discovery) project, calculates their RICE scores, finds connected delivery issues (in the OS project), and updates the RICE Score custom field on those delivery issues.

### RICE Formula

```
RICE Score = Reach (1-5) x Impact (1-5) x Confidence (1-100) / Effort (1-5)
```

### Field Mappings

**PD Project (Source - Product Discovery):**
- `customfield_10327`: Reach (1-5)
- `customfield_10324`: Impact (1-5)
- `customfield_10337`: Confidence (1-100)
- `customfield_10335`: Effort (1-5)

**OS Project (Target - Delivery):**
- `customfield_10574`: RICE Score

### Execution Steps

1. **Load Required Tools**: Use ToolSearch to load the following Atlassian MCP tools:
   - `mcp__atlassian__searchJiraIssuesUsingJql`
   - `mcp__atlassian__editJiraIssue`
   - `mcp__atlassian__getJiraIssue`

2. **Fetch All PD Features and Improvements**: Query the PD project for all Features and Improvements using JQL. Paginate through all results using `nextPageToken`.

   ```
   JQL: project = PD AND issuetype in (Feature, Improvement) ORDER BY created DESC
   Fields: summary, issuetype, customfield_10327, customfield_10324, customfield_10337, customfield_10335, customfield_10339, issuelinks
   Max Results: 100 (per page)
   Cloud ID: legal-hero.atlassian.net
   ```

   **IMPORTANT**: Continue fetching pages using `nextPageToken` until `isLast` is `true` to ensure ALL items are processed.

3. **Calculate RICE Scores**: For each Feature/Improvement:
   - Extract: Reach (`customfield_10327`), Impact (`customfield_10324`), Confidence (`customfield_10337`), Effort (`customfield_10335`)
   - Skip items where any RICE component is null/missing - track these as "skipped" items
   - Calculate: `RICE = Reach x Impact x Confidence / Effort`
   - Round to 2 decimal places

4. **Identify Connected Delivery Issues**: For each PD item with a calculated RICE score:
   - Look through `issuelinks` for links with type name `"Polaris work item link"`
   - The delivery issue is in the `inwardIssue` field of these links (link direction: PD item "is implemented by" OS issue)
   - Collect the delivery issue key (e.g., `OS-3166`)
   - Items without delivery issue links should be tracked as "no delivery link"

5. **Update Delivery Issues**: For each connected delivery issue:
   - Use `mcp__atlassian__editJiraIssue` to set `customfield_10574` to the calculated RICE score
   - Cloud ID: `legal-hero.atlassian.net`
   - If in dry run mode, skip this step

6. **Generate Output Report**: Present results as a structured summary.

### Output Format

Present the results in the following format:

```
## RICE Score Sync Results

**Date**: {current date}
**Items Processed**: {total Features + Improvements found}
**Scores Calculated**: {items with complete RICE data}
**Delivery Issues Updated**: {count of OS issues updated}

### Updated Delivery Issues

| PD Item | Summary | Reach | Impact | Confidence | Effort | RICE Score | Delivery Issue |
|---------|---------|-------|--------|------------|--------|------------|----------------|
| PD-XXX  | ...     | X     | X      | XX         | X      | XXX.XX     | OS-XXXX        |

### Skipped - Missing RICE Data

| PD Item | Summary | Missing Fields |
|---------|---------|----------------|
| PD-XXX  | ...     | Reach, Effort  |

### Skipped - No Delivery Issue Linked

| PD Item | Summary | RICE Score |
|---------|---------|------------|
| PD-XXX  | ...     | XXX.XX     |
```

### Important Notes

- Always use `legal-hero.atlassian.net` as the cloudId
- Confidence is used as-is (1-100 scale), NOT converted to decimal
- Only update delivery issues that are in the OS project (or other non-PD projects)
- If a PD item has multiple delivery issue links, update ALL of them with the same RICE score
- Track and report all categories: updated, skipped (missing data), skipped (no delivery link)
- Make update calls in parallel where possible to speed up execution (batch parallel calls)
