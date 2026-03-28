# Interview Synthesis

Synthesize feedback from a product interview transcript to extract insights and identify improvement areas with prioritization.

$ARGUMENTS

## Arguments

The user will provide:

- **Transcript**: The interview transcript (required) - can be pasted directly or provided as a file path
- **Interviewee**: Name/role of the person interviewed (optional)
- **Date**: Interview date (optional) - defaults to today
- **Type**: Interview type. Options: user, stakeholder, customer, internal, discovery. Default: user
- **Focus**: Specific focus area for synthesis. Options: all, pain-points, feature-requests, usability, satisfaction. Default: all

## Instructions

1. **Read and Understand the Transcript**: Carefully analyze the entire interview transcript to understand:
   - Context and background
   - Pain points and frustrations
   - Feature requests and suggestions
   - Behavioral patterns and workflows
   - Emotional reactions and satisfaction levels
   - Unmet needs and underlying motivations

2. **Apply Product Interview Analysis Frameworks**: Use proven frameworks to extract insights:
   - Jobs-to-be-Done (JTBD): What job is the user trying to accomplish?
   - Pain-Gain Map: What pains are they experiencing and what gains do they seek?
   - 5 Whys: Dig deeper into root causes
   - Kano Model: Classify features as basic, performance, or delighters
   - User Journey Mapping: Identify friction points in the workflow

3. **Map the Opportunity Space (Teresa Torres – Continuous Discovery Habits)**: Opportunities are not solutions — they describe the customer's world. Extract and categorize every opportunity surfaced in the interview into three types:
   - **Problems**: Things that are going wrong, frustrations, obstacles, failures ("It's annoying when...", "I can't...", "This breaks when...")
   - **Needs**: Things the customer requires or is missing but doesn't have yet ("I need to...", "I have to manually...", "There's no way to...")
   - **Desires**: Aspirational wants and wishes, often unarticulated ("I wish...", "It would be great if...", "Ideally...")

   For each opportunity:
   - Write it from the **customer's perspective**, not as a product feature
   - Identify where in their **experience** it occurs (context/moment)
   - Note the **emotional weight** (frustration level, excitement, resignation)
   - Capture the **exact quote** that surfaces it
   - Assess whether it is **explicit** (directly stated) or **implicit** (inferred from behavior/language)

   Then organize opportunities into a **hierarchy** — large, broad opportunities that contain smaller, more specific sub-opportunities. This reflects how Teresa Torres' opportunity space works: bigger parent opportunities (e.g., "Getting clarity on case status") break down into narrower child opportunities (e.g., "Knowing when a lawyer has read my message").

4. **Extract Key Themes**: Identify recurring patterns, themes, and topics that emerged during the interview

4. **Prioritize Insights**: Rank findings based on:
   - **Impact**: How significantly does this affect the user's experience or business outcomes?
   - **Frequency**: How often was this mentioned or emphasized?
   - **Urgency**: How critical is this to address?
   - **Feasibility**: How complex would it be to address this?
   - **Alignment**: How well does this align with product strategy and business goals?

5. **Categorize Improvement Areas**: Organize findings into clear categories:
   - Critical Issues: Must-fix problems blocking user success
   - High-Value Opportunities: Features/improvements with significant impact
   - Quick Wins: Low-effort, high-value improvements
   - Long-term Enhancements: Strategic improvements for the roadmap
   - Research Questions: Areas requiring further investigation

6. **Connect to Business Outcomes**: For each insight, identify how addressing it would impact:
   - User satisfaction and retention
   - Product adoption and engagement
   - Business metrics and KPIs
   - Competitive positioning

7. **Extract Actionable Recommendations**: For each improvement area, provide specific, actionable next steps

## Output Structure

Generate a structured markdown document with the following format:

```markdown
# Interview Synthesis - {Interviewee Name/Role}

**Interview Date**: {Date}
**Interview Type**: {Type}
**Synthesized**: {Current Date}
**Synthesized By**: Claude (Product Interview Synthesis)

---

## Executive Summary

[2-3 paragraph overview covering:
- Who was interviewed and why
- Main themes and insights
- Top 3 most critical findings
- Recommended immediate actions]

---

## Interview Context

**Interviewee**: {Name/Role}
**Company/Segment**: {If applicable}
**Use Case**: {Primary use case or job-to-be-done}
**Current Solution**: {What they're using now}
**Interview Focus**: {What we wanted to learn}

---

## Key Insights

### 🎯 Top Insights (Prioritized)

#### 1. {Insight Title} - Priority: 🔴 Critical / 🟡 High / 🟢 Medium
**What We Learned**:
[Clear statement of the insight]

**Evidence from Interview**:
> "{Direct quote from transcript}"

**Why This Matters**:
[Impact on user success, business outcomes, or product strategy]

**Root Cause**:
[Underlying reason - use 5 Whys approach]

**Recommended Action**:
- [ ] {Specific action item}
- [ ] {Specific action item}

**Impact if Addressed**: {Quantify expected impact}
**Effort Estimate**: Low / Medium / High
**Priority Score**: {X/10}

---

#### 2. {Insight Title} - Priority: 🔴/🟡/🟢
[Same structure as above]

---

#### 3. {Insight Title} - Priority: 🔴/🟡/🟢
[Same structure as above]

---

[Continue for all major insights, ranked by priority]

---

## Improvement Areas by Category

### 🔴 Critical Issues (Must Address)

**{Issue Title}**
- **Problem**: {Description}
- **User Impact**: {How this blocks or frustrates users}
- **Quote**: > "{Supporting quote}"
- **Recommendation**: {What to do}
- **Timeline**: Immediate / This Sprint / Next 2 Weeks
- **Owner**: {Suggested owner}

---

### 🟡 High-Value Opportunities

**{Opportunity Title}**
- **Opportunity**: {Description}
- **Business Impact**: {Revenue, retention, adoption impact}
- **User Benefit**: {How users would benefit}
- **Quote**: > "{Supporting quote}"
- **Recommendation**: {What to build/improve}
- **Timeline**: Next Quarter / This Quarter
- **Effort vs. Impact**: {Assessment}

---

### 🟢 Quick Wins

**{Quick Win Title}**
- **What**: {Simple improvement}
- **Why**: {User benefit}
- **Effort**: Low
- **Impact**: Medium/High
- **Timeline**: Next Sprint / This Month
- **Implementation Notes**: {How to do it}

---

### 🔵 Long-term Enhancements

**{Enhancement Title}**
- **Vision**: {Long-term improvement}
- **Strategic Value**: {How this supports product vision}
- **User Need**: {Underlying need}
- **Timeline**: 3-6 months / 6-12 months
- **Dependencies**: {What needs to happen first}

---

### ❓ Research Questions

**{Question}**
- **What We Don't Know**: {Knowledge gap}
- **Why It Matters**: {Impact of not knowing}
- **How to Answer**: {Research method}
- **Next Step**: {Specific action to learn more}

---

## Themes & Patterns

### Theme 1: {Theme Name}
**Frequency**: Mentioned {X} times
**Sentiment**: Positive / Negative / Neutral
**Key Points**:
- {Point 1}
- {Point 2}
- {Point 3}

**Representative Quotes**:
> "{Quote 1}"
> "{Quote 2}"

**Analysis**: {What this pattern reveals}

---

### Theme 2: {Theme Name}
[Same structure]

---

## User Journey & Pain Points

### Current Workflow
```
[Map the user's current workflow/journey as described in interview]
1. {Step 1} → Pain: {Pain point if any}
2. {Step 2} → Pain: {Pain point if any}
3. {Step 3} → Pain: {Pain point if any}
```

### Pain Point Analysis

**Most Severe Pain Points** (Ranked):
1. **{Pain Point}** - Severity: {High/Medium/Low}
   - **Where It Happens**: {Stage in journey}
   - **Frequency**: {How often}
   - **Workaround**: {Current workaround if any}
   - **Cost**: {Time/money/effort cost}
   - **Quote**: > "{Supporting quote}"

2. **{Pain Point}** - Severity: {High/Medium/Low}
   [Same structure]

---

## Opportunity Space (Teresa Torres – Continuous Discovery Habits)

> Opportunities are unmet needs, pain points, and desires from the customer's perspective. They describe the customer's world — not solutions.

### Opportunity Map

```
[Parent Opportunity]
  └── [Sub-opportunity]
  └── [Sub-opportunity]
      └── [Narrower sub-opportunity]
[Parent Opportunity]
  └── [Sub-opportunity]
```

### Problems
*Things going wrong, frustrations, obstacles*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | {Problem statement from customer POV} | > "{Quote}" | {Where in their experience} | Explicit/Implicit | High/Med/Low |

### Needs
*Requirements and missing capabilities*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | {Need statement from customer POV} | > "{Quote}" | {Where in their experience} | Explicit/Implicit | High/Med/Low |

### Desires
*Aspirational wants and unarticulated wishes*

| # | Opportunity | Quote | Context/Moment | Explicit/Implicit | Emotional Weight |
|---|------------|-------|----------------|-------------------|-----------------|
| 1 | {Desire statement from customer POV} | > "{Quote}" | {Where in their experience} | Explicit/Implicit | High/Med/Low |

### Opportunity Hierarchy

**{Parent Opportunity}**
- **Type**: Problem / Need / Desire
- **Description**: {What this covers broadly}
- **Child Opportunities**:
  - {Sub-opportunity 1} — {type}
  - {Sub-opportunity 2} — {type}
    - {Narrower opportunity} — {type}

---

## Jobs-to-be-Done Analysis

### Main Job(s)
**Primary Job**: {What the user is trying to accomplish}
- **Functional Job**: {Functional dimension}
- **Emotional Job**: {How they want to feel}
- **Social Job**: {How they want to be perceived}

**Supporting Quote**: > "{Quote about their goal}"

### Job Performance
**Current Performance**: {How well current solution performs the job}
**Gaps**: {Where current solution falls short}
**Opportunities**: {How we can help them do the job better}

---

## Feature Requests & Suggestions

### Explicit Requests
| Feature Request | Urgency | User Benefit | Effort | Priority |
|----------------|---------|--------------|--------|----------|
| {Feature 1} | High/Med/Low | {Benefit} | High/Med/Low | P0/P1/P2 |
| {Feature 2} | High/Med/Low | {Benefit} | High/Med/Low | P0/P1/P2 |

### Implicit Needs
**{Need}**
- **What They Said**: > "{Quote}"
- **What They Really Need**: {Interpreted need}
- **Why**: {Underlying motivation}
- **Solution Ideas**: {How we might address this}

---

## Satisfaction & Sentiment Analysis

### Overall Sentiment
**Satisfaction Level**: {Very Satisfied / Satisfied / Neutral / Dissatisfied / Very Dissatisfied}

**What's Working Well** ✅:
- {Positive 1}: > "{Quote}"
- {Positive 2}: > "{Quote}"

**What's Not Working** ❌:
- {Negative 1}: > "{Quote}"
- {Negative 2}: > "{Quote}"

**Emotional Indicators**:
- Frustration: {Areas where user showed frustration}
- Delight: {Areas where user showed delight}
- Confusion: {Areas where user showed confusion}

---

## Competitive Insights

### Mentioned Competitors/Alternatives
**{Competitor/Alternative}**
- **Usage**: {How/why they use it}
- **Strengths**: {What they like about it}
- **Weaknesses**: {What they don't like about it}
- **Opportunity**: {How we can differentiate}

---

## Prioritization Matrix

### Priority Scoring Breakdown
| Insight/Improvement | Impact | Frequency | Urgency | Feasibility | Alignment | Total Score | Priority |
|---------------------|--------|-----------|---------|-------------|-----------|-------------|----------|
| {Item 1} | {1-5} | {1-5} | {1-5} | {1-5} | {1-5} | {X/25} | P0/P1/P2 |
| {Item 2} | {1-5} | {1-5} | {1-5} | {1-5} | {1-5} | {X/25} | P0/P1/P2 |

**Scoring Guide**:
- **Impact**: 5 = Transformative, 3 = Significant, 1 = Minimal
- **Frequency**: 5 = Mentioned 5+ times, 3 = 2-4 times, 1 = Once
- **Urgency**: 5 = Critical/Blocking, 3 = Important, 1 = Nice to have
- **Feasibility**: 5 = Very easy, 3 = Moderate effort, 1 = Very difficult
- **Alignment**: 5 = Perfect fit, 3 = Somewhat aligned, 1 = Off-strategy

**Priority Levels**:
- **P0 (Critical)**: Score 20-25 - Address immediately
- **P1 (High)**: Score 15-19 - Plan for next sprint/quarter
- **P2 (Medium)**: Score 10-14 - Consider for roadmap
- **P3 (Low)**: Score 0-9 - Backlog/deprioritize

---

## Recommended Actions

### Immediate (This Week)
1. **{Action}**
   - **Why**: {Reason}
   - **Owner**: {Suggested owner}
   - **Output**: {Expected outcome}

### Short-term (Next 2-4 Weeks)
1. **{Action}**
   - **Why**: {Reason}
   - **Owner**: {Suggested owner}
   - **Output**: {Expected outcome}

### Medium-term (This Quarter)
1. **{Action}**
   - **Why**: {Reason}
   - **Owner**: {Suggested owner}
   - **Output**: {Expected outcome}

---

## Follow-up & Next Steps

### Additional Research Needed
- [ ] {Research question/method}
- [ ] {Research question/method}

### Validation Required
- [ ] {Hypothesis to validate}
- [ ] {Hypothesis to validate}

### Stakeholder Communication
- [ ] Share findings with: {Stakeholders}
- [ ] Schedule follow-up discussion about: {Topics}
- [ ] Create user stories for: {Items}

---

## Raw Insights & Notable Quotes

### Memorable Quotes
> "{Powerful quote 1}"
— {Context}

> "{Powerful quote 2}"
— {Context}

### Additional Notes
- {Observation that didn't fit elsewhere}
- {Context or nuance worth capturing}

---

## Appendix

### Interview Methodology
**Interview Type**: {Structured / Semi-structured / Unstructured}
**Duration**: {Duration}
**Format**: {In-person / Remote / Phone}
**Recording**: {Yes/No}

### Related Documents
- [Interview Transcript](link-to-transcript)
- [Interview Guide/Questions](link-if-available)
- [Previous Interviews](link-if-available)

---

**Document Owner**: {Product Manager/Researcher}
**Last Updated**: {Timestamp}
**Next Review**: {When this should be revisited}
```

## Execution Steps

When the user invokes `/interview-synthesis`, follow these steps:

1. **Receive Transcript**: Accept the interview transcript from the user (pasted text or file path)

2. **Read the Full Transcript**:
   - If a file path is provided, read the entire file
   - If pasted directly, process the pasted content
   - Understand the full context before analyzing

3. **Extract and Categorize**:
   - Identify all insights, pain points, feature requests, and patterns
   - Note direct quotes to support each finding
   - Categorize findings by type and severity

4. **Map the Opportunity Space (Teresa Torres)**:
   - Identify every opportunity (problem, need, or desire) surfaced in the transcript
   - Write each opportunity from the customer's perspective, not as a product feature
   - Capture the exact quote, context/moment, and emotional weight for each
   - Classify each as explicit (directly stated) or implicit (inferred)
   - Organize into a hierarchy: parent opportunities containing narrower sub-opportunities

5. **Apply Prioritization Framework**:
   - Score each insight using the 5-criteria matrix (Impact, Frequency, Urgency, Feasibility, Alignment)
   - Calculate total scores and assign priority levels
   - Rank insights from highest to lowest priority

6. **Identify Themes and Patterns**:
   - Look for recurring topics across the interview
   - Note sentiment and emotional indicators
   - Map to user journey stages where applicable

7. **Generate Actionable Recommendations**:
   - For top priorities, provide specific next steps
   - Suggest timeline and ownership
   - Connect to business outcomes

8. **Create Structured Document**:
   - Compile all findings into the markdown template
   - Save to `.claude/product/interviews/{YYYY-MM-DD}-{interviewee-slug}.md`
   - Use the interview date (when the interview took place) as the timestamp
   - Example: `.claude/product/interviews/2026-02-15-john-doe-insurance-agent.md`

9. **Summarize Key Findings**:
   - Present top 3-5 insights to user
   - Highlight critical issues requiring immediate attention
   - Suggest next steps for validation or action

## Important Notes

- **Stay Objective**: Base insights on evidence from the transcript, not assumptions
- **Preserve User Voice**: Use direct quotes liberally to maintain authenticity
- **Think Critically**: Look beyond surface-level statements to understand underlying needs
- **Be Specific**: Vague insights like "improve UX" aren't helpful - be concrete and actionable
- **Quantify When Possible**: Note frequency, duration, cost of pain points
- **Connect Dots**: Link insights to product strategy, business goals, and user outcomes
- **Question Assumptions**: Challenge whether feature requests are the right solution
- **Focus on Jobs**: Understand what job the user is trying to accomplish
- **Identify Trade-offs**: Note any conflicting needs or requests
- **Suggest Validation**: Recommend follow-up research for uncertain findings

## Tone & Style

- **Analytical and Evidence-Based**: Support every insight with quotes and evidence
- **Action-Oriented**: Focus on what to do with these insights
- **Clear and Structured**: Make it easy to scan and find key information
- **Honest**: Don't sugarcoat problems or inflate minor issues
- **Empathetic**: Show understanding of user frustrations and needs
- **Strategic**: Connect tactical insights to strategic product decisions

## Output Location

Save the synthesized document to:
- **Path**: `.claude/product/interviews/{YYYY-MM-DD}-{interviewee-slug}.md`
- **Naming Convention**: `{interview-date}-{interviewee-name-slug}.md`
- **Date Format**: Use the actual interview date (when the interview took place), not today's date
- Example: `.claude/product/interviews/2026-02-15-john-doe-insurance-agent.md`

Create the `.claude/product/interviews/` directory if it doesn't exist.
