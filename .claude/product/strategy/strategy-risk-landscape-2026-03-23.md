*Created: 2026-03-23*

# Strategic Risk Landscape — What We're Not Seeing

*This document challenges the business strategy from March 2026 by surfacing risks that weren't fully captured. The purpose is uncomfortable clarity, not reassurance.*

---

## What the Current Strategy Got Right — and Where It Stops

The business strategy correctly identified four problems: flat complaint rate, unreliable lawyer supply, operational overhead scaling with headcount, and long-term AI disruption. These are real. But the strategy looked at risks that were already visible from inside the company. It didn't look at the structural risks in the business model itself.

The user's instinct is correct: **the biggest unaddressed risk is the RSV dependency**. But it's not one risk — it's a cluster of five distinct problems that all share the same root cause: we have built a business where the most critical decisions are made by people who are not us.

---

## Risk Cluster 1: RSV Dependency — Five Distinct Problems, Not One

The business strategy treats RSV dependency as "complaint volume might trigger termination." That is only one of five ways this dependency can hurt us.

### 1.1 Revenue Concentration — We May Have 2–3 Clients

HUK is already trending at 25% of all Q1 complaints (11 → 20 → 26/month) and has escalated to Vorstand level. The strategy targets "10+ RSV partners" — which implies we have significantly fewer today. If our top 2-3 RSV partners represent 70–80% of revenue (a common pattern at this stage), we are not a platform business. We are a managed service provider with 2-3 clients. The entire business can be restructured by one phone call from one procurement director at one insurance company.

**Why this isn't in the strategy**: Revenue concentration feels like a sales problem ("go get more RSV partners"). It isn't. It's a structural fragility that requires knowing your actual numbers — and being honest about what they mean.

**The question to answer now**: What % of revenue is our top 3 RSV partners? If it's above 60%, that number belongs in the diagnosis — not as a goal to improve, but as a risk to name.

### 1.2 Bargaining Power Asymmetry — They Know We Need Them

Because RSV insurers know we depend on them, they have structural pricing power. This manifests in:
- Demands for lower per-case fees as volume increases ("we're sending you so much volume — we expect a discount")
- Requests for custom reporting formats, custom workflow adaptations, custom integrations unique to their systems
- Slow payment terms (legal cases take months — so does invoicing and collection)
- SLA terms that hold us accountable for lawyer behavior we don't fully control

Each concession seems reasonable in isolation. Cumulatively, they turn us into a bespoke IT services provider for each RSV partner — with fragmented codebases, maintenance overhead, and zero ability to say no. This is not a future risk. It is probably already happening.

**The strategic trap**: Our current strategy proposes "deepening RSV integrations to raise switching costs." Correct in theory. But deep integrations raise switching costs in both directions. A deeply integrated partner can threaten to leave and hold us hostage to demands we don't want to meet. Dependency is mutual — but they have more leverage.

### 1.3 In-House Build Risk — We're Teaching Them How It's Done

Every month we successfully run RSV case orchestration, we prove the model works and demonstrate what it looks like. Large RSV insurers (Allianz, AXA, HUK) have significant technology budgets and in-house engineering capacity. If we scale to the point where they're sending us hundreds of millions of euros in legal work annually, the build-vs-buy calculation changes. They could build an internal version of what we do. We train their operational understanding every day.

**The counter-argument**: Building this is genuinely hard — not just technically, but operationally. The lawyer network, the vetting processes, the operational knowledge are real barriers. This risk is real but not near-term. The window it creates is 3–5 years, which aligns with the AI disruption horizon.

**What this means for strategy**: The answer to in-house build risk is the same as the answer to AI disruption risk — become irreplaceable through data depth and network effects before the window closes. But we need to acknowledge the risk exists and track it.

### 1.4 RSV Insurer Consolidation or Strategic Shifts We Can't Predict

The German RSV market is fragmented today (~1,000 insurers), but insurance markets tend to consolidate. If two of our major RSV partners merge, we may go from 2 independent client relationships to 1, with reduced bargaining power and potentially conflicting contractual obligations. If an RSV insurer is acquired, the acquirer may have an existing platform relationship that doesn't include us.

Additionally: RSV insurers make strategic decisions about legal service delivery that we have no visibility into. If a major partner decides to shift from outsourced case management to in-house handling — for any reason — our revenue disappears with almost no warning.

**The question this raises**: Do we have contractual protections? Minimum volume commitments? Notice periods? These aren't product problems, but they directly determine how much strategic warning time we have before a crisis.

### 1.5 Regulatory Changes to RSV Business Models

German insurance regulation is tightening generally. If BaFin (Bundesanstalt für Finanzdienstleistungsaufsicht) requires RSV insurers to change how they source legal services — data handling requirements, lawyer independence requirements, reporting standards — our RSV partners may be forced to restructure their vendor relationships. We would be compliant collateral damage.

This is low probability but non-zero, and we have essentially zero ability to predict or control it.

---

## Risk Cluster 2: The Business Model Has a Hidden Identity Problem

### 2.1 Are We a Technology Company or a Managed Service Provider?

This question sounds philosophical. It isn't. It determines our cost structure, margin potential, competitive position, and valuation.

**If we're a technology company**: Our revenue scales faster than our costs. Margins expand with volume. Competitive moats come from software and data. We can be valued on a revenue multiple.

**If we're a managed service provider**: Our costs scale roughly with revenue. Margins are constrained by labor (operations teams, account management, quality management). We compete on operational excellence and relationships, not technology. We're valued on EBITDA, not ARR.

**The uncomfortable truth today**: Our operations look like a managed service provider. We have Post teams, phone teams, finance teams, complaint handling teams — all of which scale with case volume. The strategy aspires to replace them with technology, but until that technology works at production quality and scale, we're the second kind of company operating under the assumption that we're the first kind.

**Why this matters now**: Investors, RSV partners, and potential acquirers will make this judgment. If we present ourselves as a tech platform but our margins and operational structure look like a services company, the gap creates a credibility problem. More importantly, if we don't resolve this question internally, we'll keep making resource allocation decisions as if we're a tech company (invest in AI, resist headcount) while our operational reality requires a services company approach (hire people to handle volume).

### 2.2 The Lawyer Monetization Bet Is Unvalidated and May Not Work

The revenue strategy describes a freemium model where lawyers pay for premium AI features. The Q2 strategy projects €8.2M ARR from Premium Package take rates. These numbers are projections — they have never been tested at price.

The core assumption: lawyers will pay for features that make them more efficient on cases they're already getting from RSV partners.

**The risk**: Lawyers receive case flow through RSV mandate. They didn't choose Legalhero — they were directed to use it. A platform you're required to use feels different from one you chose. When you charge people for better access to something they didn't ask to be on in the first place, the value perception is fundamentally different from a true freemium product where users opted in.

**The alternative scenario**: Lawyers treat Legalhero as administrative infrastructure they're obligated to engage with for mandate payment. The "premium" upsell doesn't resonate because they don't see the platform as something to invest in — they see it as paperwork. If take rates land at 10% instead of the projected ~49%, the revenue strategy needs to be rebuilt.

**This should be validated before it becomes a strategic pillar**, not after €8.2M ARR has been promised to anyone.

---

## Risk Cluster 3: Structural Risks We're Not Talking About

### 3.1 The Customization Trap — Each RSV Partner Pulls Us in a Different Direction

As we deepen relationships with each RSV partner, each one has slightly different:
- Data formats and system integrations
- Reporting requirements
- Workflow preferences
- Coverage check processes
- Communication standards

Each adaptation seems reasonable. Accumulated across 5–10 RSV partners over 2–3 years, they fragment the codebase, create per-partner maintenance overhead, and make it impossible to build a standardized, scalable product. We become a bespoke IT shop for each insurance company.

**The evidence this is already happening**: The E-Consult / Webakte integration (OS-1511) exists specifically to adapt to RSV partner infrastructure. The move of ops teams to Caseforce (OS-2249) is partly about creating RSV-partner-specific workflows. These are fine individually. The question is whether there's an architectural principle governing which adaptations we make and which we refuse.

**What this requires**: An explicit policy about what we standardize (non-negotiable platform behavior) versus what we customize (partner-specific configuration). Without this policy, every new RSV partner negotiation will produce more fragmentation.

### 3.2 Key Person / Relationship Dependency

Who owns the HUK relationship? Who owns the AXA relationship? If those relationships are held by 1–2 people (founders, senior leadership), their departure creates an immediate existential risk to that revenue.

This is not mentioned anywhere in the strategy. It's the kind of risk that feels "too obvious to write down" until it happens.

**The version of this that's already a problem**: The Q2 strategy mentions "HUK escalated to Vorstand level." If that escalation happens through a personal relationship with a founder or senior leader, it may be manageable. If that person leaves, the escalation path disappears.

### 3.3 The Operations Complexity Trap — Automating Standard Work Concentrates the Exceptions

As we automate document processing, invoice creation, and case routing for standard cases, what remains is everything that doesn't fit the standard. Edge cases, disputed coverage, complex multi-party cases, lawyer disputes, regulatory anomalies.

You cannot automate exceptions. The manual ops burden may not shrink proportionally to the automation we build — it may remain roughly constant in volume but concentrate in genuinely hard, high-stakes problems that require more judgment, not less.

**The strategic implication**: The Post team headcount reduction projected from AI automation may be optimistic. The people who remain after automation are handling the hardest 20% of problems. That's not the same as having 20% of the original headcount.

---

## Risk Cluster 4: Competitive Moat — What Actually Protects Us?

The business strategy and product strategy both reference multiple moats. Let's stress-test them honestly.

| Claimed Moat | What It Actually Requires | Current State | Verdict |
|---|---|---|---|
| Network effects | More RSVs → more cases → better lawyers; more lawyers → better matching → happier RSVs | We have few RSV partners today; matching algorithm improvements have no dedicated initiative | **Not yet real** — aspirational |
| Data moat | Proprietary case outcome data that competitors can't replicate | Our data is valuable but RSVs own much of the outcome data; we have operational data, not outcome data | **Partial** — real but overstated |
| Integration moat | Deep system integrations that make switching painful | OS-1511 (E-Consult) still in progress; integrations are shallow today | **Not yet real** — in progress |
| Process moat | Standardized workflows that took years to develop | We have operational knowledge but limited process codification | **Partial** — in human heads, not systems |
| Quality moat | Brand reputation for reliable, high-quality service | Complaint rate flat at 76/month, HUK escalating to Vorstand | **Currently negative** — active quality risk |

**The honest summary**: Our actual durable advantage today is relationships and operational knowledge held by key people. This is not nothing — but it is fragile, non-scalable, and undefendable against a well-capitalized competitor.

The moats described in the strategy are what we're trying to build. They are not yet what we have.

---

## Risk Cluster 5: Regulatory Risk to the Business Model

### 5.1 Lawyer Independence Under German Law

German lawyers are *unabhängige Organe der Rechtspflege* (independent officers of the legal system) under §1 BRAO. Our mandate distribution model, performance scoring, SLA enforcement, and potential offboarding of low-performing lawyers could be challenged on grounds that we are compromising lawyer professional independence.

The Rechtsanwaltskammer (bar association) has historically scrutinized platforms that exercise significant control over legal practice. If our performance tier system is characterized as "directing legal work" rather than "operating infrastructure," we face regulatory exposure.

**This is a slow-moving risk but potentially catastrophic.** A bar association ruling that our model violates lawyer independence would require a fundamental redesign of how we manage partner lawyers.

**What we should do now**: Get a legal opinion on where our current model sits relative to the independence requirements. If we don't have this, we're building the lawyer performance accountability system without knowing its legal perimeter.

---

## What Should Be Added to the Business Strategy Diagnosis

Of the risks above, three rise to the level of deserving a place in the business strategy diagnosis alongside the four already named:

**Add to Diagnosis:**

1. **Revenue concentration — our top 2-3 RSV partners likely represent most of our revenue, creating a single point of failure risk that no operational improvement can protect against.** This requires knowing the actual number and building toward genuine distribution.

2. **We are currently a managed service provider, not a technology platform — and the gap between our self-presentation and our operational reality creates risk in every direction (investor expectations, RSV negotiations, hiring, product decisions).** The strategy must name which kind of company we are today vs. intend to become, and what the transition actually requires.

3. **Our competitive moats are aspirational, not actual.** The strategy argues network effects, data, and integration as defenses. These require being built deliberately and will take 2–3 years to become real barriers. In the meantime, a well-funded competitor — or an in-house RSV build — could get there first.

---

## The Three Questions No One Is Asking (But Should Be)

**1. What happens if HUK terminates in Q2?**
Not "what's our recovery plan" — what happens to the business? What % of revenue disappears? How long before we're in existential trouble? This scenario should be stress-tested explicitly, not treated as something to prevent by hoping the complaint rate improves.

**2. Why would a partner lawyer pay for a premium subscription to a platform they didn't choose to be on?**
This question must be answered before the Premium Package becomes a strategic bet. The take rate projections (48.72%) are specific but not validated. What's the alternative scenario if it's 15%?

**3. If we resolved all four problems in the current business strategy — complaint rate controlled, lawyer supply reliable, ops automated, AI position established — would that be enough to survive if one of our top RSV partners chose to leave for any reason?**
If the answer is no, then the current strategy is necessary but not sufficient. The RSV concentration risk needs its own set of actions, not just the complaint reduction path.

---

*This document is input to revising the business strategy diagnosis. The four existing problems remain valid. This adds three that are equally important.*
