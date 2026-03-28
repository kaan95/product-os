# 🔍 Discovery

> *"The purpose of product discovery is to address four critical risks: value, usability, feasibility, and business viability — before we commit to building."*
> — Marty Cagan

**Time allocation: ~25% (~10h/week)**

Discovery is not a phase. It is a continuous, weekly habit that runs in parallel with delivery. Its number one goal is to reduce the risk of building the wrong thing.

---

## Why It Matters (Cagan)

Without continuous discovery, you are building on assumptions. Cagan calls teams that skip discovery "feature factories" — they ship constantly but rarely move the needle because they never validated they were solving the right problems. Discovery is what separates empowered product teams from order-takers.

The key insight: **most of our initial ideas are wrong**. The job of discovery is to find that out cheaply and quickly, before engineering is involved.

---

## Problem Space vs. Solution Space — A False Dichotomy

A common mistake is treating "problem discovery" and "solution discovery" as separate phases, where you first fully validate the problem and only then explore solutions.

Cagan's view: **this separation is overly simplistic and often stifles innovation**.

The reality:
- Many breakthroughs happen precisely when problem and solution thinking are intertwined. The iPhone didn't just solve a known problem — it revealed problems people didn't know they had.
- **Most product efforts fail not because of insufficient demand, but because the solution isn't good enough to get people to switch.** Poor solutions masquerade as demand problems — "the market doesn't want this" often means "we didn't build something compelling enough."
- Discovery must therefore invest the majority of its effort not just in validating that a problem exists, but in developing a *genuinely great solution* that is valuable, usable, feasible, and viable.

**Implications for how we work:**
1. Validate problems efficiently using proven techniques, but don't over-invest here
2. Spend most discovery effort on solution quality — iterating prototypes, testing usability, stress-testing feasibility and viability
3. Cross-functional collaboration between PM (value/viability), Design (usability), and Engineering (feasibility) must happen *during* discovery — not after it

---

## The Four Risks to Eliminate in Discovery

| Risk | Question to Answer |
|---|---|
| **Value** | Will customers actually want this? Will they use it? |
| **Usability** | Can they figure out how to use it without help? |
| **Feasibility** | Can our team build it with current technology and time? |
| **Viability** | Does it work for our business — legally, financially, ethically? |

All four must be addressed before committing to build. Skipping any one is how teams waste quarters.

---

## The Discovery Stack

### 1. Opportunities
Opportunities are customer problems, needs, or pain points — not solutions. They come from:

- **User interviews** (primary source — minimum 1-2 per week)
- Product analytics and usage data (PostHog)
- Customer complaints and support tickets
- Bug reports and friction points
- Stakeholder sessions and internal feedback
- NPS responses from clients
- Observing users completing tasks in your own product

Captured and organised in the **Opportunity Solution Tree (OST)**:
- Break opportunities into smaller, more specific sub-opportunities
- Synthesise patterns across interviews — not just raw input collection
- Prioritise by: frequency, severity, alignment with business objectives

### 2. Assumptions
Once opportunities are identified, form explicit assumptions about how to solve them:

- *"We believe that [solution] will solve [problem] for [user] because [reason]."*
- Make assumptions explicit and visible — hidden assumptions are the biggest risk
- Rank assumptions by risk (how wrong could we be?) and importance (how much does it matter?)

### 3. Experiments
Test the riskiest assumptions before building. Experiments should be:

- **Small** — days, not weeks
- **Fast** — get signal quickly
- **Low-risk** — no full engineering investment
- **Time-bound** — set a deadline and a decision date

Experiment formats: prototypes, mockups, landing pages, fake-door tests, concierge tests, manual workflows, Wizard of Oz tests.

**Before launching any experiment:**
- Define the success criteria upfront
- Decide: what result would make us proceed? What result would make us pivot?

### 4. Learnings
After each experiment:

- Extract what was learned — be honest, even if the result invalidates your favourite idea
- Update the OST with learnings
- Share with the squad and relevant stakeholders
- Use learnings to inform the next experiment or to commit to building

---

## How to Do Great User Interviews (Cagan + Torres)

- **Talk to at least 1-2 users every week** — no exceptions, no matter how busy delivery gets
- Interview to understand problems, not to validate solutions
- Use the **continuous interview** format: short (30-45 min), recurring, habit-based
- Ask about the past, not hypotheticals: *"Tell me about the last time you..."*
- Do NOT guide, lead, or suggest — your job is to listen and observe
- After each interview: extract 3-5 key learnings and update the OST

---

## Connection to Business Objectives

Discovery is not free-floating exploration. It is anchored to business objectives:

1. Leadership provides the most important business objectives for the quarter
2. From those, we form **Product Outcomes** we want to influence
3. Discovery work surfaces the opportunities most relevant to those outcomes
4. Only opportunities connected to our outcomes go on the OST

This prevents interesting-but-irrelevant discovery work.

---

## Common Discovery Excuses — And Why They're Wrong

Strong product organisations treat discovery as a core competency, not optional work. These are the most common excuses used to avoid it, and the honest rebuttals:

| Excuse | The Truth |
|---|---|
| **"There's no demand"** | A poor solution masquerades as lack of demand. It's easier on the ego to blame the market than to acknowledge the solution isn't compelling enough. |
| **"Our customers hate change"** | Customers resist *bad* change. They embrace improvements that genuinely make their lives better. Slack, Stripe, and countless others proved this. |
| **"We're in a regulated industry"** | Every industry has constraints. Constraints create competitive moats — they are not a shield against doing discovery. Techniques exist specifically for regulated environments. |
| **"It's a new product type / unproven category"** | All products eventually need real user testing. Delaying discovery doesn't accelerate success — it just delays the inevitable feedback. |
| **"We can't talk to customers"** | Usually a sales team protecting account access. Solve the tension collaboratively. There is almost always a path to customer conversations. |
| **"It's impossible to test"** | This signals a lack of discovery education. Prototyping and testing techniques exist for virtually every type of problem or solution. |
| **"We don't have time"** | The weakest excuse. Discovery testing requires an order of magnitude less effort than full development. Skipping it is what actually wastes time. |

---

## Weekly Discovery Checklist

### Problem Discovery
- [ ] 1-2 user interviews completed (or scheduled for this week)
- [ ] OST updated with new opportunities and learnings
- [ ] Product analytics checked for new signals
- [ ] Customer complaints / support tickets reviewed
- [ ] Spent time using the product as a user would

### Solution Discovery
- [ ] Active solution candidate(s) identified — there is always at least one solution being actively explored, not just problems being documented
- [ ] Riskiest assumptions for current solution(s) made explicit and ranked — what would have to be true for this to work?
- [ ] At least one solution-focused test running or completed this week — prototype, usability test, concierge test, or Wizard of Oz (not just a problem interview)
- [ ] Experiment results reviewed: did they de-risk or invalidate the solution direction? What changes as a result?
- [ ] Cross-functional alignment check: Design and Engineering are aware of current solution direction and have flagged usability or feasibility concerns
- [ ] At least 2 solution variants considered before committing to one direction — first idea is rarely the best idea

---

*← [Back to Index](./00-index.md) | Next: [Outcomes & Analytics →](./02-outcomes-and-analytics.md)*
