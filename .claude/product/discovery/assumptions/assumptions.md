# Product Assumptions

This document contains all assumptions extracted from the opportunity mapping board that need to be validated through experiments.

---

## 1. The case summary provided by AI is useful and accurate

**Category:** AI-Powered Features / Case Context

**Description:** The AI-generated case summaries will provide accurate and useful information that lawyers can rely on for understanding case context.

**Related Opportunities:**
- Lawyers struggle with understanding the context of a case
- Lawyers spend too much time on a case

**Related Solution:** Create case summary with LLM

**Validation Method:** Implement a feedback button where the lawyers can give a thumbs up / down for the usefulness

**Success Criteria:** To be defined

**Status:** Pending validation

---

## 2. The lawyer will see and read the case summary

**Category:** AI-Powered Features / Case Context

**Description:** Lawyers will actually notice the AI-generated case summary in the interface and take the time to read it.

**Related Opportunities:**
- Lawyers struggle with understanding the context of a case
- Lawyers spend too much time on a case

**Related Solution:** Create case summary with LLM

**Validation Method:** Create a case summary for 5 cases and send it to the lawyer

**Success Criteria:** To be defined

**Status:** Pending validation

**Notes:** Even if summaries are accurate and useful, they won't provide value if lawyers don't notice or read them. This tests the discoverability and placement of the feature.

---

## 3. A summary will meaningfully reduce the time lawyers spend understanding case context

**Category:** AI-Powered Features / Case Context

**Description:** The AI-generated case summary will significantly reduce the time lawyers need to spend understanding a case's context compared to reading through case history and documents manually.

**Related Opportunities:**
- Lawyers struggle with understanding the context of a case
- Lawyers spend too much time on a case
- Lawyer need too much time to gain context from case history and documents

**Related Solution:** Create case summary with LLM

**Validation Method:** Manually create a case summary for 5 cases and send it to the lawyer

**Success Criteria:** 75% of the summaries are valuable according to the lawyer

**Status:** Pending validation

**Notes:** This assumption tests whether the time investment in reading a summary is actually less than the time saved by not having to read through all the raw information.

---

## 4. The lawyer will find the summary useful

**Category:** AI-Powered Features / Document Context

**Description:** Lawyers will perceive the document summary as valuable to their workflow and find it helpful for their work.

**Related Opportunities:**
- Lawyers struggle with understanding the context of a case
- Gaining context from case history is difficult
- Struggle to gain context from documents

**Related Solution:** Create case and document summaries with LLM

**Validation Method:** To be defined

**Success Criteria:** To be defined

**Status:** Pending validation

**Notes:** This assumption is related to but distinct from accuracy - a summary can be accurate but not useful if it doesn't surface the right information or is formatted poorly.

---

## 5. Users do not want to see every information about a case

**Category:** Case History / Information Display

**Description:** Users prefer a filtered or summarized view of case information rather than seeing every single detail and action in the case history.

**Related Opportunities:**
- The case history feels bloated
- Actions are displayed that do not provide the user with any additional information

**Related Solutions:**
- Hide certain actions from the action history
- Give users the option to hide certain actions from the case history

**Validation Method:** Reproduce one or different cases and show different levels of detail in the action history

**Success Criteria:** To be defined

**Status:** Pending validation

**Notes:** This assumption is critical for determining whether to implement filtering or hiding of certain actions in the case history. Appears twice in the board with slightly different contexts.

---

## 6. Users want to configure their work environment so that they can adapt the software to their needs

**Category:** User Experience / Customization

**Description:** Users prefer having configuration options that allow them to customize their work environment and adapt the software to their specific workflows and preferences.

**Related Opportunities:**
- The case history feels bloated
- Users have different requirements regarding the level of detail in the action history

**Related Solution:** Give users the option to hide certain actions from the case history

**Validation Method:** Reproduce one or different cases and show different levels of detail in the action history

**Success Criteria:** To be defined

**Status:** Pending validation

**Notes:** This tests whether users value customization or prefer opinionated defaults. Configuration adds complexity, so it's important to validate if users actually want this control.

---

## 7. Users have different requirements regarding the level of detail in the action history

**Category:** Case History / Information Display

**Description:** Different users (or the same user in different contexts) require varying levels of detail in the case action history. There is no one-size-fits-all approach.

**Related Opportunities:**
- The case history feels bloated
- Actions are displayed that do not provide the user with any additional information

**Related Solution:** Give users the option to hide certain actions from the case history

**Validation Method:** Reproduce one or different cases and show different levels of detail in the action history

**Success Criteria:** To be defined

**Status:** Pending validation

**Notes:** This assumption supports the need for configurability. If all users have the same requirements, a single optimized view would be sufficient.

---

## 8. These steps give the user enough information to make further steps

**Category:** Case Management / Status Indicators

**Description:** The status indicators (icons, checklists) provide sufficient information for lawyers to understand the case state and decide on their next actions without needing to dig into the action history.

**Related Opportunities:**
- Finding specific actions in the action history is cumbersome
- To check if all necessary documents are available is time consuming

**Related Solutions:**
- Give direct feedback about the status of specific actions using icons
- Show the user a checklist of open/started actions in the case overview (flow based)

**Validation Method:** Reproduce a case and add the checklist / Icon to the case and show it to users

**Success Criteria:** To be defined

**Status:** Pending validation

**Notes:** This tests whether visual indicators and checklists can effectively replace the need to search through detailed action history for status information.

---

## 9. User receive additional case data via documents

**Category:** Data Entry / Document Management

**Description:** A significant portion of case data that needs to be entered into the system arrives via documents (PDFs, scanned files, etc.) rather than through direct data entry or APIs.

**Related Opportunities:**
- Manual input from existing documents to document creation is time consuming
- Extracting information from existing documents is time consuming
- Inputs that have been made before, are not usable with placeholders

**Related Solutions:**
- Extract case data from documents by AI
- Allow to use case data as placeholder and edit it directly from POI
- Allow to edit case data from documents

**Validation Method:** To be defined

**Success Criteria:** To be defined

**Status:** Pending validation

**Notes:** This assumption validates whether AI-powered data extraction from documents would address a real workflow pattern. If most data comes from other sources, this feature would have limited value.

---

## Summary

**Total Assumptions:** 9

**By Category:**
- AI-Powered Features: 4 assumptions
- Case History / Information Display: 3 assumptions
- User Experience / Customization: 1 assumption
- Case Management / Status Indicators: 1 assumption
- Data Entry / Document Management: 1 assumption

**Validation Status:**
- Pending validation: 9 assumptions
- In progress: 0 assumptions
- Validated: 0 assumptions
- Invalidated: 0 assumptions
