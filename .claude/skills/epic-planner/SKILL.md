---
name: epic-planner
description: |
  Analyze epics and features for readiness, surface gaps and dependencies,
  and slice them into the smallest shippable increments. Use when the user
  provides an epic, feature, or PRD and wants to know if it's ready to build,
  what's missing, or how to break it down for delivery. Do NOT use for writing
  individual user stories — defer to the user-story skill for that.
  Trigger phrases: "analyze this epic", "break this down", "is this ready to build",
  "slice this feature", "what's missing from this epic", "epic planner".
---

# Epic Planner

Analyze a feature or epic for delivery readiness, surface gaps and dependencies, and decompose it into the thinnest shippable slices.

$ARGUMENTS

## Step 1 — Gather input

Determine the source of the epic:

**Jira key provided** (e.g. `PROJ-123`):
- Fetch the epic: `mcp__claude_ai_Atlassian__getJiraIssue` with the key.
- Fetch child issues via JQL: `parent = PROJ-123 ORDER BY created ASC` using `mcp__claude_ai_Atlassian__searchJiraIssuesUsingJql`.
- Use the epic summary, description, and child issue summaries as your analysis input.

**Text / PRD / Confluence content provided**:
- Use the content in the conversation directly. No fetch needed.

**Input too vague to analyze**:
- Do not proceed. Tell the user what's missing: e.g. "I need at least a goal, target user, and a rough scope to analyze this. Can you provide those?"

---

## Step 2 — Gaps & Dependencies

Produce two lists. Be specific — reference the user's actual input, not generic filler.

### Gaps

Things that are missing, ambiguous, or assumed that could stall development or cause rework. Assign each a severity:

- 🔴 **Blocker** — must resolve before development starts
- 🟡 **Pre-sprint** — resolve before sprint planning
- 🟢 **During development** — can resolve in-sprint

Format each gap as: `🔴/🟡/🟢 [Short label] — [what's missing or ambiguous and why it matters]`

### Dependencies

Anything this feature needs that the team does not directly control. For each: name the dependency and what it blocks.

Examples: another team's API work, third-party service SLA, design assets, legal/compliance approval, infrastructure provisioning.

---

## Step 3 — Blocker gate

If there are any 🔴 blockers:

1. Present the Gaps and Dependencies output.
2. Stop and say: "There are [N] blockers above that should be resolved before slicing this feature for delivery. Resolve them, or tell me to proceed anyway and I'll slice with the information available."
3. Wait for the user's response before continuing to Step 4.

If there are no blockers, proceed directly to Step 4.

---

## Step 4 — Shippable Slicing

Redecompose the feature into vertical slices — each must deliver independent, observable user value. A slice is too large if it takes more than one sprint; flag it and suggest a further split.

Apply these strategies to find thinner slices:
1. Core happy path end-to-end first
2. One user type, one object type, one channel — reduce variation before adding coverage
3. Manual or admin fallback before automation
4. Read before write
5. Hardcoded before configurable

For each slice, produce:

| # | Slice | User value | Size |
|---|-------|------------|------|
| 1 | Short name | One sentence: what the user can do and why it matters | S / M / L |

If a slice is **L**, add a note below the table: "Slice N is large — consider splitting by [specific dimension, e.g. user type, data source, trigger]."

---

## Step 5 — Recommended Sequence

Order the slices from Step 4 by:
1. Dependency order (what must exist before the next slice can work)
2. Risk reduction (spikes, unknowns, third-party integrations — do these early)
3. User value (highest value earliest, all else equal)

Present as a numbered list. Mark the **MVP** — the smallest contiguous set of slices that is worth shipping independently:

```
1. [Slice name] — [one-line rationale]
2. [Slice name] — [one-line rationale]
── MVP line ──
3. [Slice name] — [one-line rationale]
...
```

---

## Step 6 — Handoff offer

After presenting the sequence, ask:

> "Want me to create Jira user stories for any of these slices? If so, tell me which ones (by number) and I'll use the user-story skill to write and file them one at a time."

If the user says yes: invoke the user-story skill for each selected slice in order, passing the slice name and user value sentence as input. Do not batch — complete one before starting the next so the user can review.
