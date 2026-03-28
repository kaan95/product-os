# Weekly Planner

Act as your personal product management planning assistant to help you focus on the most impactful work each week. Generate a concise, high-level weekly plan based on your product strategy, outcomes, initiatives, and best practices.

$ARGUMENTS

## Arguments

The user may provide the following optional arguments:

- **Week**: Which week to plan for. Options: current, next. Default: current
- **Focus**: Specific focus area for the week. Options: discovery, delivery, outcomes, strategy, communication, all. Default: all

## Instructions

### Phase 1: Gather Context

1. **Review Product Management Operating Guide**: Read `/product/operating-guide.md` to understand time allocation framework and critical habits
2. **Review Strategic Context**: Read all files in `/product/strategy/` to understand current strategy and priorities
3. **Review Current Outcomes**: Read the most recent file in `/product/outcomes/2026/` to understand top 3 outcomes and recommended actions
4. **Review Active Initiatives**: Read the most recent file in `/product/initiatives/2026/` to understand current work and blockers

### Phase 2: Identify Priorities

1. **Extract Top 3 Priorities** from outcomes document - these are the highest-impact outcomes to move this week
2. **Identify Critical Actions** from outcomes recommendations - what are the specific next steps?
3. **Ensure Critical Habits** - Must include 1-2 interviews, 2 discovery activities, 2-4 experiments per operating guide

### Phase 3: Generate Concise Plan

Create a **short, scannable** weekly plan (less than 1 minute to read) that includes:
1. **Top 3 Priorities** - What outcomes you're moving this week
2. **Activities by Category** - Discovery, Outcomes, Delivery, Strategy
3. **Success Criteria** - How you'll know you had a good week

## Output Structure

Generate a **concise** markdown document with the following structure:

```markdown
# Weekly Plan: Week of {Date}

## 🎯 Top 3 Priorities

1. **[Outcome/Goal]** - [Why it matters in 1 sentence] → [This week's specific goal]
2. **[Outcome/Goal]** - [Why it matters in 1 sentence] → [This week's specific goal]
3. **[Outcome/Goal]** - [Why it matters in 1 sentence] → [This week's specific goal]

---

## 🔍 Discovery (Target: 3-4 hours)

**Interviews:**
- [ ] Interview #1: [Who/Topic] - [Day]
- [ ] Interview #2: [Who/Topic] - [Day]

**Discovery Activities:**
- [ ] [Activity 1]: [Specific task]
- [ ] [Activity 2]: [Specific task]

**Experiments to Launch:**
- [ ] Experiment 1: [Hypothesis to test]
- [ ] Experiment 2: [Hypothesis to test]
- [ ] Experiment 3: [Hypothesis to test]
- [ ] Experiment 4: [Hypothesis to test]

---

## 📊 Outcomes & Analytics (Target: 2-3 hours)

- [ ] [Key outcome tracking activity]
- [ ] [Analytics review or metric analysis]
- [ ] [Experiment results analysis]

---

## 🚀 Delivery (Target: 3-4 hours)

- [ ] [User story writing or refinement activity]
- [ ] [Backlog refinement or sprint ceremony]
- [ ] [Critical blocker to unblock]

---

## 🎨 Strategy (Target: 1-2 hours)

- [ ] [Strategic alignment activity]
- [ ] [Prioritization or roadmap decision]

---

## 💬 Communication (Target: 1-2 hours)

- [ ] Product Weekly: Share [key update/learning]
- [ ] [Stakeholder update or sync]
- [ ] [Team alignment activity]

---

## ✅ Success Criteria

- ✓ [Specific deliverable or milestone for Priority 1]
- ✓ [Specific deliverable or milestone for Priority 2]
- ✓ [Specific deliverable or milestone for Priority 3]
- ✓ 2 customer interviews completed
- ✓ 2-4 experiments launched

---

## ⚠️ Watch Out For

- **[Potential blocker 1]**: [How to mitigate]
- **[Potential blocker 2]**: [How to mitigate]

---

**Context Sources**: [Operating Guide](../operating-guide.md) | [Strategy](../strategy/) | [Outcomes](../outcomes/2026/outcomes-q1-2026.md) | [Initiatives](../initiatives/2026/initiatives-q1-2026.md)
```

## Execution Steps

When the user invokes `/plan`, follow these steps:

1. **Gather Context**: Read operating guide, strategy, outcomes, and initiatives files
2. **Extract Top 3 Priorities**: Pull directly from the "Top 3 Outcomes to Focus On" section in outcomes document
3. **Identify Specific Actions**: Extract recommended actions from outcomes document for each priority
4. **Ensure Critical Habits**:
   - 1-2 interviews (REQUIRED)
   - 2 discovery activities (REQUIRED)
   - 2-4 experiments to launch (REQUIRED)
5. **Populate Activities**: Organize specific tasks by category (Discovery, Outcomes, Delivery, Strategy, Communication)
6. **Keep It Concise**: Total output should be scannable in under 1 minute
7. **Save to File**:
   - Create `/to-dos/` folder if it doesn't exist
   - Save plan to `/to-dos/plan-{YYYY-MM-DD}.md` (e.g., `plan-2026-02-16.md`)
   - Use the Monday date of the week being planned
   - Present the plan to user AND provide clickable link to saved file

## Important Notes

### Format Requirements
- **Concise**: No day-by-day breakdown, no hourly allocation, no unnecessary detail
- **Scannable**: Use checkboxes, bullets, and clear headings
- **Actionable**: Every item is a specific task, not vague guidance
- **Aligned**: Directly tied to Top 3 priorities from outcomes document

### Discovery Requirements (Non-Negotiable)
**MUST include:**
- 1-2 customer interviews (specific who/topic/day)
- 2 discovery activities (research, analysis, product usage)
- 2-4 experiments to launch (with hypothesis)

### Time Allocation (Reference Only)
Use operating guide framework as rough guide:
- Discovery: 25% (~10h) → Aim for 3-4h of focused discovery
- Outcomes: 20% (~8h) → Aim for 2-3h
- Delivery: 25% (~10h) → Aim for 3-4h
- Strategy: 15% (~6h) → Aim for 1-2h
- Communication: 15% (~6h) → Aim for 1-2h

Don't include this breakdown in the output - just use it to ensure balanced activities.

### Prioritization
- Top 3 priorities come directly from outcomes document "Top 3 Outcomes to Focus On" section
- Activities should directly support these 3 priorities
- If an activity doesn't connect to a top priority, don't include it

### Tone
- Direct and actionable
- No fluff or unnecessary explanation
- Assume the user knows their context - just tell them what to do

### File Management
- **ALWAYS save the plan** to `/to-dos/plan-{YYYY-MM-DD}.md`
- Use the Monday date of the week being planned (e.g., if planning week of Feb 16-22, use `plan-2026-02-16.md`)
- Create the `/to-dos/` folder if it doesn't exist
- After generating the plan, show it to the user AND provide a clickable link to the saved file

## Example Output Length

The entire output should be approximately 30-40 lines of markdown (including whitespace), scannable in under 60 seconds.

Good example length:
- Top 3 Priorities: 3-5 lines
- Discovery: 6-8 checkboxes
- Outcomes: 2-3 checkboxes
- Delivery: 2-3 checkboxes
- Strategy: 1-2 checkboxes
- Communication: 2-3 checkboxes
- Success Criteria: 4-5 bullets
- Blockers: 2 items

**Total: ~30-40 lines**

Bad example: Anything longer than 50 lines or requiring more than 1 minute to read.
