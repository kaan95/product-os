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
4. If a sprint is specified, assign the story to that sprint.
5. If a priority is specified, set the priority accordingly.
6. Use the specified project key, or default to "OS" if not provided.
7. Return the URL link to the ticket to me when you are done.

## Output

Create a user story with:

1. **Title**: Clear, concise summary
2. **Problem Definition**: A clear problem definition that helps anyone reading the ticket understand what the problem actually is about.
2. **User Story Statement**: 
"As a [persona], 
I want [goal], 
So that [benefit]"
3. **Acceptance Criteria**: Specific, testable criteria using Title for each Acceptance Criteria, and a Given/When/Then format
4. Format for Acceptance Criteria
Title for Acceptance Criteria
- Given: ...
- When: ...
- Then: ...

