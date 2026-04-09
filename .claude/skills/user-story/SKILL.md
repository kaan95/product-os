---
name: user-story
description: Create a well-structured user story in Jira based on provided input. 
---

# Create User Story

Generate a well-structured user story based on the following input:

$ARGUMENTS

## Arguments

The user may provide the following optional arguments:

- **Sprint**: The sprint to assign the story to (e.g., "Sprint 30")
- **Project**: The Jira project key (e.g., "OS"). Default: OS
- **Priority**: The priority level. Options: highest, high, medium, low. Default: medium

## Instructions

1. Always write the user story in English.
2. Always create or update the user story directly in Jira.
3. Only add the following 3 sections: Problem, User Story, Acceptance Criteria. Do not add anything else.
4. If a sprint is specified, assign the story to that sprint. To assign a sprint, look up the sprint ID first by querying an existing issue in that sprint (JQL: `project = OS AND sprint = "Sprint X"`), then use the numeric sprint ID in `customfield_10020`.
5. If a priority is specified, set the priority accordingly.
6. Use the specified project key, or default to "OS" if not provided.
7. Return the URL link to the ticket to me when you are done.
8. Keep Acceptance Criteria concise: **2–5 ACs maximum**.
9. **BE vs FE split:** Always divide work into separate backend and frontend tickets.
   - Backend tickets must have the prefix: `BE - `
   - Frontend tickets must have the prefix: `FE - `
   - If it is unclear whether the ticket is BE or FE, ask the user before creating it.
10. After creating the ticket, **transition it to "Open"** status using `getTransitionsForJiraIssue` and `transitionJiraIssue`.
11. **Dependencies:** If tickets have dependencies (e.g. a BE ticket must be done before a FE ticket), link them in Jira using `createIssueLink`:
    - The FE ticket is "blocked by" the BE ticket.
    - Use link type "Blocks": inwardIssue = BE ticket (blocker), outwardIssue = FE ticket (blocked).
12. **Design tickets:** When creating a FE ticket, judge whether a Design ticket is also needed (e.g. new UI components, new flows, significant visual changes).
    - If yes, create the Design ticket in the **same project** as the FE ticket (OS, CF, or CX — never in the UX project).
    - Always use issue type **"Design"** for these tickets.
    - Always assign the Design ticket to **Katharina Treptow** (accountId: `712020:2c26d4fe-2a9e-4876-9e74-7e7311a8112d`).
    - Link the Design ticket as a dependency of the FE ticket ("blocked by" Design).
    - Inform the user that a Design ticket was created.
    - If the change is minor (e.g. disabling a button, showing a toast), skip the Design ticket.

## Output

Create a user story with:

1. **Title**: Clear, concise summary (with BE/FE prefix)
2. **Problem Definition**: A clear problem definition that helps anyone reading the ticket understand what the problem actually is about.
3. **User Story Statement**: 
"As a [persona], 
I want [goal], 
So that [benefit]"
4. **Acceptance Criteria**: 2–5 specific, testable criteria using a title + Given/When/Then format:

Title for Acceptance Criteria
- Given: ...
- When: ...
- Then: ...
