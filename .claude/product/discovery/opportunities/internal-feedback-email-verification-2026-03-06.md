# Opportunities: Unverified Email Addresses at Case Creation

**Source**: Internal operations feedback (verbal report)
**Source Date**: 2026-03-06
**Source Author**: Internal team
**Stakeholder Perspective**: internal (primary), client (secondary)
**Extracted**: 2026-03-06
**Total Opportunities**: 4

---

## Opportunity Summary

| # | Opportunity | Type | Pain | Reach | Frequency | Score | Parent |
|---|------------|------|------|-------|-----------|-------|--------|
| 1 | Invalid client email addresses are not caught during case creation, blocking downstream communication | Problem | High | Broad | Constant | 27 | -- |
| 2 | Client information surveys cannot be delivered due to wrong email addresses, delaying case progress | Problem | High | Significant | Regular | 12 | 1 |
| 3 | Operations team has no visibility into email delivery failures until cases are already delayed | Problem | Medium | Significant | Regular | 8 | 1 |
| 4 | No automated email validation or verification step exists in the intake workflow | Need | High | Broad | Constant | 27 | 1 |

---

## Opportunity Tree

```
Invalid client emails not caught at case creation [Score: 27]
  ├── Client surveys undeliverable, delaying cases [Score: 12]
  ├── No visibility into email delivery failures [Score: 8]
  └── No email validation in intake workflow [Score: 27]
```

---

## Detailed Opportunities

### Parent Opportunity 1: Invalid client email addresses are not caught during case creation, blocking downstream communication

**Type**: Problem
**Stakeholder**: Internal (operations), Client (indirect)
**Description**: When cases are created, client email addresses are not verified or validated. This means typos, non-existent mailboxes, and incorrect addresses enter the system unchecked. Since email is a critical communication channel for client surveys, case updates, and document requests, invalid emails break the entire downstream communication flow and delay case handling.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High | Causes significant case delays. Over 500 undeliverable emails in 3 months means hundreds of cases experienced disrupted communication. |
| Reach | Broad | Affects the entire case intake flow -- every case where the email is wrong is impacted. 500+ cases in 3 months suggests a systemic issue, not edge cases. |
| Frequency | Constant | With 500+ failures in 3 months (~167/month, ~5-6/day), this is a daily occurrence. |
| **Score** | **27** | |

**Supporting Evidence**:
> "In the last three months we had over 500 emails which could not be delivered due to wrong Mailbox meaning wrong email addresses."
> -- Internal operations feedback

> "We often have the problem that emails are not verified when cases are being created."
> -- Internal operations feedback

**Where it occurs**: Case creation / intake workflow -- the point where client contact data is captured
**Current workaround**: Presumably manual follow-up via phone to obtain correct email, causing additional delays and operational overhead
**Strategic relevance**: Directly connects to **Pillar 1: Platform Orchestration** (structured case intake) and **Pillar 3: Process Standardization** (quality gates before case progresses). Also impacts case velocity metrics and the complaint rate target (<1%).

---

#### Child: Client information surveys cannot be delivered due to wrong email addresses, delaying case progress

**Type**: Problem
**Stakeholder**: Internal (operations), Lawyer (downstream), Client (delayed service)
**Description**: After case creation, LH sends clients a survey to gather additional information needed for case handling. When the email address is invalid, this survey never arrives. The case stalls because critical client information cannot be collected, creating a bottleneck that delays the entire case lifecycle.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High | Cases are "significantly delayed" -- the survey is a critical dependency for case progress. Without it, lawyers lack information to start substantive work. |
| Reach | Significant | 500+ emails in 3 months is a substantial volume. Not all cases are affected, but those that are experience meaningful delays. |
| Frequency | Regular | ~167 cases per month affected based on 3-month data. |
| **Score** | **12** | |

**Supporting Evidence**:
> "This then leads to the problem that we cannot send out the survey that we have for clients to get further information which delays the case significantly."
> -- Internal operations feedback

**Where it occurs**: Post-intake, when the client information survey is triggered
**Current workaround**: Unknown -- likely requires manual outreach (phone call) to obtain missing information, adding operational cost and delay
**Strategic relevance**: Impacts case velocity (intake -> lawyer assignment target: <24 hours) and connects to **Pillar 2: AI-Powered Automation** (structured intake data capture)

---

#### Child: Operations team has no visibility into email delivery failures until cases are already delayed

**Type**: Problem
**Stakeholder**: Internal (operations)
**Description**: There appears to be no proactive alerting or monitoring when survey emails bounce or fail to deliver. The problem is likely discovered only when follow-up actions stall (e.g., survey responses don't come back), by which point the case is already delayed. Earlier detection would allow faster remediation.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | Medium | Delayed detection compounds the original problem. If bounces were caught immediately, the team could reach out same-day via phone. Instead, days may pass before anyone notices. |
| Reach | Significant | Affects all cases with invalid emails (~500 in 3 months). |
| Frequency | Regular | Every bounced email is a missed detection opportunity. |
| **Score** | **8** | |

**Supporting Evidence**:
> Inferred from the fact that 500+ emails accumulated over 3 months -- if bounce detection were immediate and actionable, the problem would have been addressed sooner or escalated earlier.

**Where it occurs**: Email delivery monitoring / post-send workflow
**Current workaround**: Unknown -- the accumulation of 500+ cases suggests no systematic bounce handling exists
**Strategic relevance**: Connects to **Pillar 4: Data-Driven Infrastructure** (automated detection of at-risk cases)

---

#### Child: No automated email validation or verification step exists in the intake workflow

**Type**: Need
**Stakeholder**: Internal (operations), Client
**Description**: The intake workflow lacks an email validation step -- either real-time format/syntax validation during data entry, or a verification step (e.g., confirmation email) before the case proceeds. Implementing validation at the point of data capture would prevent the downstream cascade of failures.

| Dimension | Rating | Evidence |
|-----------|--------|----------|
| Pain Level | High | The absence of validation is the root cause of all downstream problems. A simple validation step would eliminate the entire issue category. |
| Reach | Broad | Would benefit every case flowing through the platform -- prevention at source. |
| Frequency | Constant | Every case creation is a moment where validation should occur. |
| **Score** | **27** | |

**Supporting Evidence**:
> "We often have the problem that emails are not verified when cases are being created."
> -- Internal operations feedback, explicitly identifying the missing validation as the root cause

**Where it occurs**: Case creation form / intake workflow
**Current workaround**: None -- invalid emails pass through unchecked
**Strategic relevance**: Directly supports **Pillar 3: Process Standardization** (quality gates) and **Pillar 1: Platform Orchestration** (structured case intake). Email validation is a standard quality gate that should exist before a case can progress.

---

## Cross-References

### Overlaps with Existing Opportunities

1. **Strong overlap with survey-partner-lawyers Opportunity 8 (Case intake quality inconsistent)** -- Lawyers report that "Viele Falle beginnen, obwohl die wichtigsten Infos fehlen." Invalid email addresses are another dimension of the same intake quality problem. The lawyer survey captures the downstream frustration; this source captures the upstream root cause for one specific data type (email).

2. **Related to survey-partner-lawyers Opportunity 9 (Contact/address data often incomplete or wrong)** -- Invalid emails are a specific instance of the broader Stammdaten quality problem. Gabriela Riley's quote -- "keine Kontaktdaten der Gegenseite, kein Gericht, kein Geschaftsfuhrer, keine Email Adresse" -- describes the same category of issue.

3. **Connected to complaint-insights Opportunity 4 (Intake & Handover Quality)** -- Complaint insights identified intake errors and poor data capture as a recurring LH-side failure. Invalid emails are a quantified instance of this broader pattern.

### New Themes Identified

1. **Quantified intake quality gap**: This is the first source that provides a hard number (500+ failures in 3 months) for a specific intake data quality issue. Previous sources described intake quality qualitatively but lacked metrics.

2. **Email as critical case dependency**: The source reveals that email-based surveys are a critical step in the case lifecycle -- without them, cases stall. This dependency was not previously documented.

3. **Prevention vs. detection gap**: The root cause is a missing validation step (prevention), not a detection or remediation issue. This suggests the intake workflow lacks basic quality gates.

### Gaps & Uncertainties

1. **Total case volume context**: 500 undeliverable emails in 3 months -- but what percentage of total cases does this represent? If LH handles 5,000 cases/month, this is ~3%. If 1,000/month, it's ~17%. The severity assessment depends on this ratio.

2. **Root cause breakdown**: Are these typos during manual entry? Auto-imported data from RSV systems? Client self-service submissions? The root cause determines the right solution (validation UI vs. RSV data quality vs. automated verification).

3. **Delay quantification**: Cases are "significantly delayed" but we don't have data on how much delay. Is it days? Weeks? Quantifying the delay would strengthen the business case.

4. **Recovery process**: What happens today when an email bounces? Is there a defined process to obtain the correct email, or does each case manager handle it ad hoc?

5. **Other communication channels affected**: If email is wrong, are other contact details (phone, address) also unreliable? This may be symptomatic of broader intake data quality issues.

---

## Source Notes

**Source quality**: Low-medium -- single verbal report with one key data point (500 emails in 3 months). Provides a clear problem statement but limited detail on root causes, current processes, or impact quantification.

**Limitations**:
- No breakdown of where invalid emails originate (manual entry, RSV import, client self-service)
- No data on case delay duration caused by invalid emails
- No information on current remediation process
- Single internal perspective -- no cross-validation with other teams
- The 500 number is stated but not verified against system data

**Recommended follow-up**:
1. **Pull system data**: Verify the 500 number and calculate it as a % of total cases to understand true reach
2. **Root cause analysis**: Determine where invalid emails originate -- intake phone calls? RSV data feeds? Client portal? Each source requires a different fix
3. **Delay measurement**: Track the average additional delay on cases with email bounce vs. successful delivery
4. **Solution evaluation**: Assess options -- real-time syntax validation, email verification API (e.g., ZeroBounce, NeverBounce), confirmation email flow, or fallback to SMS
5. **Broader Stammdaten audit**: Check error rates across all contact data fields (phone, address, email) to determine if this is an email-specific or systemic data quality issue
