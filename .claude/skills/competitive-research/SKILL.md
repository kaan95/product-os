---
name: competitive-research
description: Conduct comprehensive competitive intelligence research on the legal tech landscape to inform Legalhero's product strategy, identify innovation opportunities, and maintain awareness of market movements.  
---

# Competitive Research

Conduct comprehensive competitive intelligence research on the legal tech landscape to inform Legalhero's product strategy, identify innovation opportunities, and maintain awareness of market movements.

$ARGUMENTS

## Arguments

The user may provide the following optional arguments:

- **Focus**: The type of competitive research to perform. Options: landscape, company, feature, funding, trends
  - `landscape` - Broad overview of the competitive landscape across legal tech (default)
  - `company` - Deep dive into a specific competitor (requires company name)
  - `feature` - Analyze a specific product feature or capability across competitors
  - `funding` - Focus on recently funded startups, investment trends, and emerging players
  - `trends` - Identify macro trends, emerging technologies, and market shifts

- **Company**: Specific company to analyze (used with `company` focus). Examples: "Harvey AI", "Legora", "Clio", "Ironclad"

- **Region**: Geographic focus. Options: global, europe, dach, us. Default: global
  - `global` - Worldwide legal tech landscape
  - `europe` - European legal tech companies and market dynamics
  - `dach` - Germany, Austria, Switzerland focus (most relevant to Legalhero)
  - `us` - US market (often leading in innovation, relevant for trend-spotting)

- **Depth**: Level of analysis. Options: quick, standard, deep. Default: standard
  - `quick` - High-level summary with key takeaways (good for standups/quick updates)
  - `standard` - Comprehensive analysis with actionable insights
  - `deep` - Exhaustive research with detailed analysis, market sizing, and strategic implications

## Instructions

1. **Research Using Web Search**: Use `WebSearch` and `WebFetch` tools extensively to gather current, real-time competitive intelligence. Do NOT rely on outdated training data alone — always search for the latest information.

2. **Review Legalhero Context First**: Before conducting research, review the following to understand Legalhero's current position:
   - **Product Strategy**: Review `/product/strategy/` folder
   - **Current Initiatives**: Review `/product/initiatives/` folder
   - **Company Context**: Review `/context/` folder and `CLAUDE.md`

   This ensures all competitive analysis is framed relative to Legalhero's position and priorities.

3. **Core Competitors to Track**: Always include analysis of these key competitor categories:

   ### Tier 1 — Direct Competitors (Legal Case Management / Legal Ops in DACH/Europe)
   - **Legora** — German legal tech, AI-powered legal research and case management
   - **rightmart / Legalbird** — German legal tech platforms focused on consumer legal services
   - **Advocado** — German legal tech marketplace connecting lawyers and clients
   - **ROLAND Rechtsschutz digital initiatives** — Insurance-side legal tech
   - **Anwalt.de** — German lawyer marketplace and legal information platform
   - **Geblitzt.de / Flightright** — Specialized German legal tech for specific claim types

   ### Tier 2 — International Innovators (Setting the pace globally)
   - **Harvey AI** — AI-powered legal assistant for law firms (US, rapidly expanding)
   - **Clio** — Leading cloud-based legal practice management (Canada/Global)
   - **Ironclad** — Contract lifecycle management (US)
   - **EvenUp** — AI for personal injury claims (US)
   - **Atrium / Lawtrades** — Legal services platforms (US)
   - **Luminance** — AI-powered legal intelligence (UK)
   - **Darrow** — AI justice intelligence platform (Israel)
   - **Leya** — AI legal assistant (Sweden/Europe)

   ### Tier 3 — Recently Funded / Emerging Players
   - Search for latest YC legal tech companies
   - Search for recent Series A/B legal tech raises
   - Search for legal tech companies featured in TechCrunch, Sifted, or Handelsblatt
   - Look for stealth-mode companies and new market entrants

4. **Analysis Dimensions**: For each competitor (depth varies by `Depth` argument), analyze:

   #### Business & Strategy
   - **What they do**: Core value proposition and positioning
   - **Problem they solve**: Primary pain point addressed
   - **Target customer**: Who they serve (law firms, consumers, insurers, corporates)
   - **Business model**: How they make money (SaaS, marketplace, transaction-based, hybrid)
   - **Strategy**: Go-to-market approach, expansion plans, partnerships
   - **Differentiation**: What makes them unique vs. alternatives

   #### Product & Innovation
   - **Core product**: Main product offering and key features
   - **AI/Tech capabilities**: Use of AI, automation, data, and technology
   - **Innovative features**: Notable product innovations or unique capabilities
   - **User experience**: Quality of UX/UI and user-facing workflows
   - **Platform/API**: Ecosystem, integrations, and platform play
   - **Product velocity**: Speed of shipping new features and product updates

   #### Traction & Growth
   - **Funding**: Total raised, latest round, investors, valuation (if available)
   - **Growth signals**: User numbers, revenue, headcount growth, market expansion
   - **Partnerships**: Strategic partnerships (insurers, law firms, courts, etc.)
   - **Market presence**: Geographic reach and market penetration
   - **Customer testimonials/case studies**: Evidence of success and outcomes

   #### Outcomes & Impact
   - **Success metrics**: Published outcomes (case resolution speed, cost savings, etc.)
   - **Market validation**: Signs of product-market fit
   - **Awards/recognition**: Industry awards, press coverage, rankings
   - **Customer satisfaction**: NPS, reviews, testimonials

5. **Always Connect to Legalhero**: Every analysis should include:
   - **Relevance to Legalhero**: How does this competitor or trend affect us?
   - **Lessons & inspiration**: What can we learn or adapt?
   - **Threats**: What risks does this pose to our positioning?
   - **Opportunities**: What gaps or ideas can we exploit?
   - **Actionable recommendations**: Specific product/strategy actions for Legalhero

6. **Save Research Output**: Save the research document to `/.claude/product/competition/` folder:
   - Landscape reports: `landscape-{date}.md`
   - Company deep dives: `company-{company-name}-{date}.md`
   - Feature analyses: `feature-{feature-name}-{date}.md`
   - Funding reports: `funding-{date}.md`
   - Trend reports: `trends-{date}.md`

## Research Process

When the user invokes `/competitive-research`, follow these steps:

1. **Load Context**: Read Legalhero's strategy, initiatives, and company context to frame the research.

2. **Conduct Web Research**: Use `WebSearch` to gather current intelligence:
   - Search for each competitor by name + recent news
   - Search for "legal tech funding 2025 2026"
   - Search for "YC legal tech startups"
   - Search for "legal tech trends {current year}"
   - Search for "legal tech Europe / DACH"
   - Search for specific product features or capabilities
   - Use `WebFetch` to read detailed articles, press releases, and product pages

3. **Analyze & Synthesize**: Organize findings into the structured output format below.

4. **Generate Legalhero Implications**: For every insight, articulate what it means for Legalhero.

5. **Save & Summarize**: Save the document and provide a brief executive summary to the user.

## Output Structure

Structure the research document as follows:

```markdown
# Competitive Research: {Focus} — {Date}

**Research Focus**: {Focus description}
**Region**: {Region}
**Depth**: {Depth level}
**Generated**: {Date}

## Executive Summary

[3-5 bullet points summarizing the most important findings and their implications for Legalhero]

## Competitive Landscape Overview

### Market Map
[High-level categorization of players by segment, positioning, and relevance to Legalhero]

### Key Themes
1. [Theme with brief explanation]
2. [Theme with brief explanation]
3. [Theme with brief explanation]

## Competitor Profiles

### {Competitor Name}
**Category**: [Direct / International Innovator / Emerging]
**HQ**: [Location]
**Founded**: [Year]
**Funding**: [Total raised, last round]

**What They Do**
[Core value proposition in 2-3 sentences]

**Problem They Solve**
[Primary pain point addressed]

**Strategy**
[Go-to-market approach and strategic direction]

**Product & Innovation**
- Key features: [Notable product capabilities]
- AI/Tech: [Technology approach]
- Recent launches: [Latest product updates]

**Traction & Growth**
- Users/Customers: [Numbers if available]
- Revenue signals: [Growth indicators]
- Partnerships: [Key partnerships]
- Headcount: [Team size and growth]

**Outcomes**
[Published results, case studies, success metrics]

**Legalhero Implications**
- Threat: [How this affects our position]
- Opportunity: [What we can learn or exploit]
- Action: [Specific recommendation]

[Repeat for each competitor]

## Recently Funded Startups

| Company | HQ | Raised | Round | Focus | Relevance |
|---------|-----|--------|-------|-------|-----------|
| [Name] | [Location] | [Amount] | [Stage] | [Description] | [Why it matters] |

## Innovation Radar

### Breakthrough Features & Products
1. **[Feature/Product]** by [Company]
   - What it does: [Description]
   - Why it matters: [Impact]
   - Legalhero application: [How we could adapt this]

2. **[Feature/Product]** by [Company]
   [Same structure]

### Emerging Technologies in Legal Tech
1. [Technology trend and implications]
2. [Technology trend and implications]

## Strategic Implications for Legalhero

### Threats to Monitor
1. [Threat with explanation and mitigation]
2. [Threat with explanation and mitigation]

### Opportunities to Capture
1. [Opportunity with explanation and recommended action]
2. [Opportunity with explanation and recommended action]

### Competitive Advantages to Strengthen
1. [Advantage and how to deepen it]
2. [Advantage and how to deepen it]

### Product Ideas & Inspiration
1. **[Idea Name]**: [Description, inspired by whom, how it fits Legalhero]
2. **[Idea Name]**: [Description, inspired by whom, how it fits Legalhero]

## Recommendations

### Immediate Actions (Next 30 Days)
1. [Specific action item]
2. [Specific action item]

### Strategic Initiatives (Next Quarter)
1. [Strategic initiative]
2. [Strategic initiative]

### Long-term Positioning (6-12 Months)
1. [Positioning move]
2. [Positioning move]

## Watch List

Companies and developments to monitor closely:
1. [Company/Trend] — [Why and what to watch for]
2. [Company/Trend] — [Why and what to watch for]

---

**Sources**: [List of URLs and sources used in research]
**Last Updated**: {Timestamp}
**Next Review**: {Suggested date for next competitive review}
```

## Focus-Specific Guidance

### Landscape Mode
- Cover all three competitor tiers
- Provide a broad market map
- Identify 5-7 key themes shaping the market
- Focus on strategic implications over individual company details

### Company Mode
- Go deep on the specified company
- Research their product roadmap, recent launches, hiring patterns
- Analyze their technology stack and AI capabilities
- Look for interviews, blog posts, and conference talks by their leadership
- Compare their approach directly to Legalhero's

### Feature Mode
- Research how multiple companies implement the specified feature
- Analyze best-in-class implementations
- Identify gaps and opportunities for Legalhero
- Provide specific UX/product recommendations

### Funding Mode
- Focus on recently funded companies (last 6-12 months)
- Analyze investment trends and where money is flowing
- Identify hot segments and investor theses
- Flag emerging competitors early

### Trends Mode
- Focus on macro trends and market shifts
- Analyze technology trends (AI, automation, data)
- Look at regulatory changes affecting legal tech
- Identify inflection points and timing opportunities

## Important Notes

- **Always use fresh data**: Legal tech is moving fast. Always search for the latest information. Do not rely solely on training data.
- **Be specific and evidence-based**: Back up claims with sources, data points, and concrete examples.
- **Frame everything relative to Legalhero**: Every insight should connect back to what it means for us.
- **Distinguish facts from speculation**: Clearly label what is confirmed vs. what is inferred or speculated.
- **Include sources**: Always cite URLs and sources so findings can be verified.
- **Think like a product leader**: Focus on actionable product and strategy insights, not just information gathering.
- **Consider the European/DACH context**: Legalhero operates in DACH. US innovations may need adaptation for the European market, regulatory environment, and customer expectations.
- **Update regularly**: Competitive intelligence is perishable. Recommend a review cadence (monthly for landscape, quarterly for deep dives).
