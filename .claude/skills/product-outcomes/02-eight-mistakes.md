# The 8 Most Common Mistakes When Defining Product Outcomes

From Teresa Torres and Hope Gurion (Product Talk). Use this file when evaluating a draft outcome or KR — work through whichever mistakes seem relevant, not necessarily all eight.

---

## Mistake 1: Disguising an Output as an Outcome

**What it looks like**: "Our outcome is to deliver the Android app." / "Our outcome is to launch the new onboarding flow."

**Why it's a problem**: These are things you *build*, not impacts you *create*. You can ship an Android app that nobody uses. You can launch a new onboarding flow that doesn't change completion rates. Shipping ≠ value created.

**The tell**: If your "outcome" could appear on a project tracker as a deliverable, it's probably an output.

**The fix**: Ask "What change in customer behaviour are we hoping this creates?" The answer to that question is your outcome.
- "Deliver Android app" → "X% of mobile users complete their first case submission within 48 hours"
- "Launch new onboarding flow" → "Onboarding completion rate increases from 34% to 55%"

---

## Mistake 2: Setting a Business Outcome Instead of a Product Outcome

**What it looks like**: "Our outcome is to grow revenue." / "Our outcome is to reduce churn."

**Why it's a problem**: These are real and important — but they're too far removed from what a product team controls day to day. Revenue is influenced by pricing, sales, marketing, seasonality, and dozens of other factors. A team assigned "grow revenue" has no clear signal about whether their specific work is contributing.

**The tell**: If your "outcome" is something an executive would report to the board, it's probably a business outcome, not a product outcome.

**The fix**: Deconstruct the business outcome. Ask "What customer behaviour, if it changed, would drive this business result?" Follow the causal chain downward until you find something the team can observe and influence.
- "Reduce churn" → "% of active users who complete at least one full case workflow per month" (because you have evidence that engaged users renew)
- "Grow revenue" → "% of free users who initiate a paid case within 30 days of signup"

---

## Mistake 3: Using a Traction Metric

**What it looks like**: "Our outcome is to increase the number of searches." / "Our outcome is to increase login frequency."

**Why it's a problem**: Traction metrics measure adoption of a specific feature or action, not customer value. More searches often means customers are struggling to find things — it can go up even as satisfaction goes down. Traction metrics tempt teams to optimise for usage of their solution rather than value created.

**The tell**: Your "outcome" is tied to one specific feature or action rather than a broader customer goal.

**The fix**: Zoom out. Ask "What is this feature trying to help customers accomplish? What would success look like for *them*, not for the feature?"
- "Increase number of searches" → "% of users who find and open the relevant document within their first session" (the underlying goal)
- "Increase login frequency" → "Users complete at least one meaningful action per week" (frequency is a proxy — this gets at the real thing)

---

## Mistake 4: Setting an Outcome Outside the Team's Control

**What it looks like**: "Our outcome is to reduce the time lawyers spend on administrative tasks" — when the team doesn't control the lawyer-facing tooling.

**Why it's a problem**: Teams need real agency over their outcomes. If hitting the metric depends heavily on another team shipping something, or on external decisions, the team becomes frustrated and the outcome becomes a source of blame rather than motivation.

**The tell**: "We could hit this outcome if only [other team / partner / external factor] did X."

**The fix**: Find the version of the outcome that sits within the team's sphere of influence. This might mean narrowing the scope or choosing a different point in the customer journey.
- "Reduce lawyer admin time" (requires other team) → "% of case updates lawyers can complete without leaving the platform" (what this team can move)

---

## Mistake 5: Measuring Actions Instead of Value

**What it looks like**: "Our outcome is to increase the number of users who click 'Submit'." / "Our outcome is to increase the number of documents uploaded."

**Why it's a problem**: Actions are not the same as value created. A user might upload a document and still have a terrible experience. The action happened; the value didn't. Optimising for clicks and uploads can lead to dark patterns — friction reduction that feels good in the metric but harms users.

**The tell**: Your outcome is an action the customer performs, not a result the customer experiences.

**The fix**: Ask "After they take this action, what does success look like for them?" Connect the action to the outcome it's supposed to serve.
- "Increase documents uploaded" → "% of cases where all required documents are in place within 72 hours of intake" (the actual goal)
- "Increase 'Submit' clicks" → "% of users who successfully complete a full case submission without abandoning"

---

## Mistake 6: Relying on Sentiment Metrics Alone

**What it looks like**: "Our outcome is to improve NPS." / "Our outcome is to improve CSAT scores."

**Why it's a problem**: Sentiment metrics are lagging indicators — they reflect how customers felt in the past, often measured infrequently (quarterly surveys, post-interaction ratings). They're hard to act on because they don't tell you *what* to change. A team that sets NPS as their outcome has to infer what behaviours might move it.

**The tell**: The metric is a survey score collected after the fact, not an observable behaviour happening in the product.

**The fix**: Sentiment metrics can be useful as *context* or a *secondary signal*, but pair them with a behavioural outcome the team can actually observe and influence.
- "Improve NPS" → "% of users who successfully complete their first case with no support contact" + NPS as a secondary check
- "Improve CSAT" → "Average time from case intake to first meaningful lawyer response" (the behaviour likely driving satisfaction)

---

## Mistake 7: No Clear Connection to Business Value

**What it looks like**: "Our outcome is to increase time spent in the app." / "Our outcome is to increase the number of features used."

**Why it's a problem**: An outcome that doesn't have a plausible path to business value is just a vanity metric with extra steps. Time-in-app and feature breadth can go up while the business is declining. If you can't articulate *why* this customer behaviour drives business results, you may be optimising for the wrong thing.

**The tell**: You'd struggle to draw a causal arrow from this outcome to a business result someone upstairs cares about.

**The fix**: For every product outcome, be able to state the theory: "If [this customer behaviour] increases, we believe [this business result] will follow, because [reason]." If you can't articulate the reason, challenge the choice of metric.
- "Increase time in app" → Challenge: why? → Replace with "% of users who complete at least one end-to-end workflow per week" and state the causal theory.

---

## Mistake 8: No Accountability Model

**What it looks like**: The outcome exists in a doc somewhere but nobody is sure who owns it, how often it's reviewed, or what "making progress" looks like.

**Why it's a problem**: Outcomes without ownership and review cadences quietly fade. Teams fall back to output delivery because output is easier to see and count.

**The tell**: "We have outcomes" but nobody can tell you what the current number is or what changed it last.

**The fix**: For each outcome, establish: Who owns it? What's the current baseline? How often do we review it? What does it mean if it moves? Outcomes need the same operational rigour as any other product metric.

---

## Quick Diagnostic: Five Questions for Any Outcome

1. **Is it a behaviour or a build?** If it's something you ship, it's an output.
2. **Can this team directly influence it?** If not, it's probably a business outcome or depends on someone else.
3. **Is it tied to one specific feature?** If so, it's probably a traction metric.
4. **Can you draw a causal arrow to a business result?** If not, it's a vanity metric.
5. **Does someone own it and review it regularly?** If not, it's aspirational decoration.
