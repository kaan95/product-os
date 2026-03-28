# Invoice Automation Logic

**Category:** finance
**Created:** 2026-01-26
**Last Updated:** 2026-02-19
**Source:** [Finance Automation Squad Meeting](https://www.notion.so/Finance-Automation-Squad-2f15e8cace3980219712d4a19cbe97ab)

---

## Overview

This document describes the automated invoice generation and payment processing system for out-of-court legal cases. The system automatically creates invoices when cases are closed, with a review and approval workflow to ensure accuracy before finalization. It also covers the payment matching process where bank transactions are matched to invoices and payment records are created.

## Purpose

This documentation exists to:
- Define the scope and boundaries of invoice automation
- Document which invoice types and cases are included/excluded
- Explain the automation triggers and workflow
- Clarify the review and approval process
- Document the payment matching and recording process
- Guide technical implementation and configuration updates

**Target Audience:** Product team, developers, finance team, and operations staff

## Key Concepts

- **TEB (Telefonische Erstberatung)**: Telephone initial consultation service
- **Sammelabrechnung**: Collective billing process for specific case types
- **Out-of-court cases (Steps 1-3)**: Cases that don't proceed to court litigation
- **Court invoices**: Complex invoices for cases that go to litigation (NOT automated)
- **Invoice configuration**: Template settings that define fee structures and calculations
- **Invoice group**: Category of invoice determined by how a case is closed
- **Streitwert**: Value in dispute (required by some insurances)
- **Gebühr Akteneinsicht**: Fee for file inspection in criminal law cases
- **Payment entry**: Record in the payment table linking a bank transaction to an invoice
- **PAID status**: Invoice status when full payment amount has been received
- **PARTIALLY_PAID status**: Invoice status when partial payment has been received but full amount is still outstanding
- **Payment matching**: Process of linking incoming bank transactions to outstanding invoices

## Logic/Process Flow

### High-Level Flow

```
Case Closed → Automation Check → Invoice Generated → Review Queue → Approval/Rejection → Finalization →
Send to Insurance → Insurance Transfer Money → Finance Imports Payments → Payment Matching →
Payment Recording → Export Matched Records → Upload to DATEV
```

### Detailed Process

#### Step 1: Case Closure Trigger

When a lawyer closes a case:
1. System checks if the case qualifies for automation (see Business Rules)
2. If qualified, system reads the case closure type and captured information
3. System determines the appropriate invoice configuration based on:
   - Case closure type
   - Insurance provider
   - Case type (TEB, document check, out-of-court)
   - Additional lawyer inputs (e.g., document review performed)

#### Step 2: Invoice Generation

1. System applies the appropriate invoice configuration
2. Generates invoice content based on:
   - Base fee structure
   - Additional fees from lawyer inputs (e.g., +€12 for document review)
   - Case-specific data (client info, case details)
3. Creates invoice in **draft** state (no invoice number assigned yet)
4. Generates HTML preview of the invoice document

#### Step 3: Review Queue

1. Invoice added to review queue
2. Notification sent to **invoicing group** (excludes Jan, Valentin, and Leo)
3. Reviewer can:
   - View invoice preview
   - Automatically navigate to related case
   - See all invoice details and calculations

#### Step 4: Approval or Rejection

**If Approved:**
1. Invoice number is assigned
2. Invoice is finalized and marked as ready for sending
3. PDF is generated from the approved HTML document

**If Rejected:**
1. Reviewer must provide a comment explaining the reason
2. Comment is stored in action history
3. Invoice remains in draft state
4. Finance team must create a new invoice manually from scratch

#### Step 5: Document Editing (Optional)

Before approval, reviewers can edit the HTML document preview to fix minor issues:
- Missing Streitwert values
- Incorrect client addresses
- Other non-calculation fields required by insurance

**Important:**
- Document edits happen at runtime (before PDF generation)
- Edits do NOT update the underlying database values
- Table cells with invoice calculations can be made uneditable to prevent errors

#### Step 6: Invoice Sent to Insurance

Once the invoice is approved:
1. Invoice is sent to the insurance provider
2. Invoice status is tracked in the system
3. Invoice awaits payment from insurance

#### Step 7: Insurance Payment Transfer

1. Insurance processes the invoice
2. Insurance transfers payment to Legalhero's bank account
3. Bank transaction appears in daily bank statements

#### Step 8: Payment Import

1. Finance team imports bank transactions into the system **daily**
2. Bank transactions are loaded into the system as unmatched payments
3. Transactions contain:
   - Transaction date
   - Amount
   - Reference information (e.g., invoice number, case reference)
   - Sender information

#### Step 9: Payment Matching

**Manual or Automated Matching:**

Finance team matches bank transactions to invoices based on:
- Invoice number in transaction reference
- Payment amount matching invoice amount
- Case reference numbers
- Insurance provider information
- Manual review and matching when automatic matching fails

**Matching Outcomes:**
- **Full Match**: Transaction amount = Invoice amount
- **Partial Match**: Transaction amount < Invoice amount
- **Overpayment**: Transaction amount > Invoice amount (edge case)
- **No Match**: Transaction cannot be linked to any invoice

#### Step 10: Payment Recording

Once a bank transaction is matched to an invoice:

1. **Create Payment Entry:**
   - System creates a new record in the **payment table**
   - Payment entry links the bank transaction to the invoice
   - Records:
     - Payment amount
     - Payment date
     - Bank transaction reference
     - Matched invoice ID
     - Payment method (bank transfer)

2. **Update Invoice Status:**
   - If payment amount = invoice amount: Invoice status → **PAID**
   - If payment amount < invoice amount: Invoice status → **PARTIALLY_PAID**
   - Outstanding balance is calculated and tracked
   - Payment history is maintained for the invoice

3. **Record Audit Trail:**
   - Who performed the matching
   - When the match was made
   - Any notes or comments about the payment

#### Step 11: Export Matched Payments

1. Finance team exports matched payment records
2. Export includes:
   - Invoice details
   - Payment details
   - Bank transaction information
   - Matching metadata
3. Export format: CSV file with specific naming convention (EXTF_*.csv)
4. Export format: Semicolon-separated CSV for DATEV compatibility

See related stories:
- Backend: [OS-2921](https://legal-hero.atlassian.net/browse/OS-2921) - Export file generation
- Frontend: [OS-3086](https://legal-hero.atlassian.net/browse/OS-3086) - Export button UI

#### Step 12: Upload to DATEV

1. Exported CSV file is uploaded to DATEV (accounting software)
2. DATEV processes the payment records
3. Accounting books are updated with payment information
4. Financial reconciliation completed

## Business Rules

### Automated Invoice Types

**INCLUDED:**
- ✅ TEB (Telefonische Erstberatung) invoices
- ✅ Document check invoices
- ✅ Out-of-court cases (steps 1, 2, and 3)
- ✅ Converted TEB cases that become normal cases

**EXCLUDED:**
- ❌ Court invoices (too complex for automation)
- ❌ Advance invoices for lawsuits (complex calculations)
- ❌ Non-converted TEB cases in Sammelabrechnung (separate job handles these)
- ❌ ARAG Sammelabrechnung cases (invoices created but not sent)
- ❌ R&V Sammelabrechnung cases (invoices created but not sent)

### Trigger Conditions

**Primary Trigger:** Case closure event

**Conditions for Automation:**
1. Case is an out-of-court case (steps 1-3)
2. Case is NOT part of Sammelabrechnung (unless converted TEB)
3. Case has a valid invoice configuration mapping
4. Case type allows for standard fee calculations

**Invoice Group Determination:**
- Determined by HOW the case is closed (closure type)
- NOT determined by coverage type
- Mapped through comprehensive sheet (being created by Rabea)

### Payment Matching Rules

**Payment Status Rules:**
1. **PAID Status:**
   - Applied when: Total payments received = Invoice total amount
   - Invoice is marked as fully paid
   - No further payments expected
   - Invoice is ready for DATEV export

2. **PARTIALLY_PAID Status:**
   - Applied when: Total payments received < Invoice total amount
   - Outstanding balance calculated: Invoice amount - Total payments received
   - Invoice remains open for additional payments
   - Subsequent payments can be added until fully paid

3. **Multiple Payments:**
   - An invoice can have multiple payment entries
   - Each payment is recorded separately in the payment table
   - Status is determined by sum of all payments vs. invoice amount
   - Payment history is maintained chronologically

**Matching Requirements:**
1. Each bank transaction must be matched before creating payment entry
2. Payment entries cannot be created without a matched invoice
3. One bank transaction can be split across multiple invoices (rare)
4. One invoice can receive multiple payments (common for partial payments)

**Export Requirements:**
1. Only matched payments are included in DATEV export
2. Unmatched bank transactions remain in the system for manual review
3. Export filename must follow format: EXTF_*.csv
4. Export must be semicolon-separated CSV format

## Configuration

### Invoice Configuration Structure

Invoice configurations contain:
- Base fee amounts
- Additional fee elements (e.g., Gebühr Akteneinsicht for criminal law)
- Calculation rules
- Insurance-specific requirements
- Field mappings from case data

### Configuration Updates Needed

**Known Gaps:**
1. New case closure types require new configuration entries
2. Criminal law configurations missing values:
   - Gebühr Akteneinsicht (file inspection fee)
   - New €180 invoice type (currently manual)
3. Additional fees based on lawyer input during closure:
   - €12 for document review in court cases
   - Other closure-specific fees

### Configuration Process

1. Rabea creates comprehensive mapping sheet:
   - All case closure types
   - All insurance providers
   - Appropriate invoice configuration for each combination
2. Rabea and Kaan review invoice configurations together
3. Identify and add missing configuration values
4. Test configurations with actual case data

## Examples

### Example 1: Standard TEB Invoice (Automated)

**Scenario:** Client completes a telephone consultation that is NOT converted to a full case.

**Process:**
- Case closed as "TEB completed"
- System identifies this as Sammelabrechnung case
- Automation SKIPPED (separate Sammelabrechnung job handles this)

### Example 2: Converted TEB to Full Case (Automated)

**Scenario:** TEB consultation converts to full legal case, case resolved out of court.

**Process:**
- Case closed as "Resolved - Out of court"
- System identifies: converted TEB, out-of-court resolution
- Invoice configuration: Standard out-of-court fee structure
- Invoice generated automatically
- Sent to review queue

### Example 3: Court Case with Advance Invoice (NOT Automated)

**Scenario:** Case proceeds to litigation, advance invoice needed.

**Process:**
- Lawyer initiates lawsuit
- System recognizes: Court invoice configuration required
- Automation SKIPPED (too complex)
- Finance team creates invoice manually

### Example 4: Criminal Law with Document Review (Automated with Additional Fee)

**Scenario:** Criminal law case, lawyer reviewed court documents.

**Process:**
- Case closed as "Criminal case - resolved"
- Lawyer indicates: "Yes, I reviewed documents" during closure
- System applies: Criminal law configuration + €12 document review fee
- Invoice generated with additional fee
- Sent to review queue

### Example 5: Full Payment Match (PAID Status)

**Scenario:** Invoice for €500 sent to insurance, full payment received.

**Process:**
- Invoice approved and sent to insurance (Invoice Amount: €500)
- Insurance transfers €500 to Legalhero bank account
- Finance imports bank transactions daily
- Bank transaction matched to invoice (Reference: Invoice #12345)
- Payment entry created: €500
- Invoice status updated: **PAID**
- Invoice ready for DATEV export

### Example 6: Partial Payment (PARTIALLY_PAID Status)

**Scenario:** Invoice for €800 sent to insurance, receives €500 first, then €300 later.

**Process:**
- Invoice approved and sent (Invoice Amount: €800)
- First payment received: €500
  - Payment entry #1 created: €500
  - Invoice status: **PARTIALLY_PAID**
  - Outstanding balance: €300
- Second payment received: €300
  - Payment entry #2 created: €300
  - Total payments: €800
  - Invoice status updated: **PAID**
  - Outstanding balance: €0
- Invoice ready for DATEV export

### Example 7: Multiple Invoices from Daily Import

**Scenario:** Daily bank statement contains 50 transactions to be matched.

**Process:**
- Finance imports bank statement CSV
- System loads 50 transactions
- Finance team reviews transactions for matching:
  - 40 transactions have clear invoice references → Auto-matched
  - 8 transactions require manual review → Manually matched
  - 2 transactions cannot be matched → Remain unmatched for investigation
- Payment entries created for 48 matched transactions
- 48 invoices have status updated (PAID or PARTIALLY_PAID)
- Matched payments available for DATEV export

## Edge Cases

### 1. Missing Required Fields

**Issue:** Client address missing, but insurance requires it.

**Handling:**
- Invoice generated and sent to review
- Reviewer edits HTML document to add address
- Document editing doesn't affect database
- Invoice approved with corrected HTML

### 2. Incorrect Fee Calculation

**Issue:** System applies wrong configuration, fee amount is incorrect.

**Handling:**
- Reviewer rejects invoice with explanation comment
- Comment stored in action history
- Finance team creates new invoice manually
- Root cause investigated for configuration update

### 3. Sammelabrechnung Status Unclear

**Issue:** Unclear if TEB case should be in Sammelabrechnung or get individual invoice.

**Handling:**
- System checks conversion status
- If converted: Individual invoice (automated)
- If NOT converted: Sammelabrechnung (separate process)
- Edge case: Manually review if conversion status ambiguous

### 4. New Insurance Provider

**Issue:** New insurance provider not in configuration mapping.

**Handling:**
- Automation fails gracefully
- Case flagged for manual invoice creation
- Finance team creates invoice manually
- Configuration updated to include new provider

### 5. Multiple Closures for Same Case

**Issue:** Case closed, reopened, then closed again.

**Handling:**
- Each closure triggers automation check
- System prevents duplicate invoices for same case/closure
- Previous rejected invoices remain in history
- Only latest approved invoice is finalized

### 6. Overpayment from Insurance

**Issue:** Insurance pays more than the invoice amount.

**Handling:**
- Payment entry created for full amount received
- Invoice status: **PAID**
- Overpayment amount flagged for review
- Finance team investigates:
  - Was it intended for multiple invoices?
  - Should excess be refunded?
  - Should it be applied to future invoices?
- Manual resolution required

### 7. Unmatched Bank Transaction

**Issue:** Bank transaction received but cannot be matched to any invoice.

**Handling:**
- Transaction remains in system as **unmatched**
- Finance team investigates:
  - Check for missing invoice number in reference
  - Check for typos in case reference
  - Contact insurance to clarify payment purpose
- Once clarified, manual matching performed
- Payment entry created after successful match

### 8. Duplicate Payment Detection

**Issue:** Insurance accidentally sends payment twice for same invoice.

**Handling:**
- System detects invoice already marked as PAID
- Second payment flagged for review
- Finance team verifies duplication
- Options:
  - Refund duplicate payment to insurance
  - Apply to future invoice if agreement exists
- Payment entry created with notes about duplication

### 9. Wrong Amount Received

**Issue:** Invoice is for €500, but insurance pays €450.

**Handling:**
- Payment entry created for €450
- Invoice status: **PARTIALLY_PAID**
- Outstanding balance: €50
- Finance team investigates discrepancy:
  - Was there a deduction/adjustment by insurance?
  - Was it an error?
- Resolution:
  - Request additional €50 from insurance, OR
  - Write off €50 difference if agreed, OR
  - Adjust invoice and payment records

### 10. Payment Before Invoice Approval

**Issue:** Payment received before invoice is approved/finalized.

**Handling:**
- Bank transaction imported and remains unmatched
- Invoice goes through approval process
- Once invoice is approved and finalized:
  - Existing unmatched payment can be matched
  - Payment entry created retroactively
  - Invoice status updated appropriately

### 11. Matching to Wrong Invoice

**Issue:** Finance team accidentally matches payment to wrong invoice.

**Handling:**
- Payment entry incorrectly links transaction to wrong invoice
- Wrong invoice marked as PAID/PARTIALLY_PAID
- Correct invoice remains unpaid
- **Resolution Process:**
  - Delete incorrect payment entry (or mark as reversed)
  - Revert invoice status to previous state
  - Match transaction to correct invoice
  - Create new payment entry with correct invoice
  - Update audit trail with correction notes

### 12. Split Payment Across Multiple Invoices

**Issue:** Single bank transaction covers multiple invoices (rare but possible).

**Handling:**
- Finance team identifies transaction covers multiple invoices
- Manual process required:
  - Create payment entry #1 for invoice #1 with portion of amount
  - Create payment entry #2 for invoice #2 with remaining amount
  - Both payment entries reference same bank transaction
- Each invoice status updated based on amount received
- Special flag/note added to indicate split payment

## Dependencies

### Data Dependencies

- **Case Data:**
  - Case type and status
  - Closure type and reason
  - Client information
  - Insurance provider
  - Case value (Streitwert)
  - Lawyer inputs during closure

- **Configuration Data:**
  - Invoice configuration templates
  - Fee structures by insurance
  - Mapping sheet (case closures → invoice types)

- **Payment Data:**
  - Bank transaction records (imported daily)
  - Payment table entries
  - Invoice-to-payment mappings
  - Payment matching rules and criteria
  - Outstanding balance calculations

### System Dependencies

- Case management system (case closure events)
- Invoice generation engine
- Document preview/editing system
- Notification system (for invoicing group)
- PDF generation service
- Action history/audit logging
- Bank transaction import system (daily import)
- Payment matching system (manual and automated)
- Payment table/database
- CSV export functionality for DATEV
- DATEV integration/upload system

### Team Dependencies

- **Rabea:** Creating and maintaining closure-to-invoice mapping sheet
- **Anton:** Implementing document preview editing functionality
- **Finance Team (Invoicing Group):** Review and approval of automated invoices
- **Melanie:** Currently handles manual criminal law €180 invoices

## Technical Notes

### Document Preview Editing

- Editing happens at **runtime** before PDF generation
- No document exists while invoice is in draft state
- Document is generated on-demand when:
  - Reviewer opens preview
  - Invoice is approved (for PDF generation)
- HTML document can be edited directly
- Table cells (calculations) should be made uneditable via CSS/JS
- Edits are temporary and only affect the generated document, NOT database

**Technical Approach:**
- Server-side HTML generation with editable fields
- Contenteditable attributes on allowed fields
- JavaScript to prevent editing of calculation cells
- Submit edited HTML back to server for PDF generation

### Rejection Workflow

**Database Considerations:**
- Cannot easily edit underlying invoice action entry
- Mutation of original data is risky and complex
- Rejected invoices remain in database with rejection reason
- New invoice creation preferred over editing rejected ones

**Action History:**
- All approvals and rejections logged
- Rejection comments stored
- Audit trail for all invoice actions

### Review Process Evolution

**Phase 1 (Initial):**
- 100% manual review of all automated invoices
- Goal: Validate automation accuracy
- Collect data on rejection rates and reasons

**Phase 2 (Future):**
- Spot-checking of automated invoices
- Only certain invoice types require review
- High-confidence cases automatically approved
- Risk-based review selection

### Payment Matching System

**Data Model:**

```
Payment Table Structure:
- payment_id (PK)
- invoice_id (FK)
- bank_transaction_id (FK)
- payment_amount
- payment_date
- payment_method
- matching_method (auto/manual)
- matched_by (user_id)
- matched_at (timestamp)
- notes
- created_at
- updated_at
```

**Invoice Status Tracking:**
- Invoice has status field: DRAFT, PENDING, SENT, PAID, PARTIALLY_PAID, CANCELLED
- Status transitions tracked in audit log
- Payment history maintained for each invoice
- Outstanding balance calculated: Invoice Amount - SUM(Payments)

**Matching Algorithm:**
1. **Automatic Matching Criteria:**
   - Exact invoice number match in transaction reference
   - Amount matches invoice amount exactly
   - Transaction date within expected range
   - Sender matches insurance provider

2. **Manual Matching:**
   - Finance user selects unmatched transaction
   - Searches for invoice by number, case reference, or amount
   - Reviews invoice details and confirms match
   - System validates match is possible
   - Payment entry created with manual flag

**Export Generation:**
- Query matched payments within date range
- Generate CSV with EXTF_ prefix
- Semicolon-separated format for DATEV compatibility
- Include all required fields per DATEV specification
- File downloaded to finance user's machine
- User uploads file to DATEV system

**Technical Constraints:**
- Payment entries are immutable once created (for audit)
- Corrections require reversal + new entry
- All changes logged in audit trail
- Payment matching requires active invoice (not draft/cancelled)
- Daily import runs as scheduled job
- Export generation happens on-demand (user-triggered)

## References

- [Finance Automation Squad Meeting - Jan 23, 2026](https://www.notion.so/Finance-Automation-Squad-2f15e8cace3980219712d4a19cbe97ab)
- Related context: [Buchungen Finance](/context/finance/buchungen-finance.md)
- Invoice configuration system (to be documented)
- Rabea's closure mapping sheet (in progress)
- **Payment Export Implementation:**
  - [OS-2921](https://legal-hero.atlassian.net/browse/OS-2921) - BE: Export File for Matched Payments
  - [OS-3086](https://legal-hero.atlassian.net/browse/OS-3086) - FE: Export Button for Matched Payments
- **Parent Epic:**
  - [OS-3068](https://legal-hero.atlassian.net/browse/OS-3068) - Finance: Achieve 80% Matching Rate for Invoice <-> Payments - Q1 2026

## Timeline & Milestones

**Q1 2026 Goals:**
- ✅ Define automation scope and boundaries
- 🔄 Complete closure-to-invoice mapping sheet (Rabea)
- 🔄 Update invoice configurations with missing values (Rabea & Kaan)
- 🔄 Implement document preview editing (Anton)
- ⏳ Initial automation testing
- ⏳ First production deployment with 100% review
- ⏳ Evaluate results after 2 weeks

**Success Metrics:**
- Automation coverage (% of invoices automated)
- Rejection rate (target: <10%)
- Approval time (target: <24 hours)
- Manual intervention frequency
- Configuration accuracy
- **Payment Matching Metrics:**
  - Payment matching rate (target: 80% in Q1 2026)
  - Auto-match success rate (% of payments automatically matched)
  - Average time to match payment (manual)
  - Unmatched transaction resolution time
  - Payment status accuracy (correct PAID/PARTIALLY_PAID assignment)

## Questions/Open Items

### Resolved
- ✅ Should court invoices be automated? **No - too complex**
- ✅ Can invoice actions be edited? **No - too risky; rejection workflow instead**
- ✅ Who receives approval notifications? **Invoicing group only**

### Open Questions

1. **Configuration Completeness:**
   - Are all new case closure types mapped?
   - Are all insurance providers covered?
   - Are all criminal law fee elements configured?
   - **Owner:** Rabea & Kaan
   - **Due:** Before initial testing

2. **Document Editing Scope:**
   - Which fields should be editable?
   - Which fields should be locked?
   - How to handle validation errors?
   - **Owner:** Anton
   - **Due:** Before production deployment

3. **Review Process:**
   - What triggers spot-checking vs. full review?
   - How to determine confidence levels?
   - When to transition from 100% review to spot-checking?
   - **Owner:** Team decision after 2 weeks of data

4. **Error Handling:**
   - How to handle missing configuration?
   - How to notify finance team of automation failures?
   - How to track failed automation attempts?
   - **Owner:** Development team

5. **Sammelabrechnung Integration:**
   - How does automation interact with existing Sammelabrechnung job?
   - Are there any conflicts or duplications?
   - **Owner:** To be discussed

6. **Payment Matching Automation:**
   - What are the criteria for automatic vs manual matching?
   - Can we improve auto-match success rate?
   - What fields in bank transactions are most reliable for matching?
   - **Owner:** Finance team & Development team
   - **Due:** During Q1 2026 optimization

7. **Payment Export to DATEV:**
   - What is the exact DATEV CSV format specification?
   - Are all required fields available in our payment data?
   - How often should exports be generated?
   - **Owner:** Finance team
   - **Due:** Before production deployment

8. **Partial Payment Handling:**
   - How to notify insurances of outstanding balances?
   - What is the follow-up process for partial payments?
   - Should system send automatic reminders?
   - **Owner:** Finance team & Product team

### Action Items

**Invoice Automation:**
- [ ] **Rabea:** Complete Notion sheet mapping case closures to invoice types for all insurances
- [ ] **Rabea & Kaan:** Review invoice configuration together to identify and add missing values
- [ ] **Anton:** Implement edit button for invoice document preview with locked calculation cells
- [ ] **Team:** Conduct initial automation tests before next meeting
- [ ] **Team:** Meet in ~2 weeks to review first automation results
- [ ] **Team:** Evaluate coverage, reject/approval rates, and overall performance

**Payment Matching & Export:**
- [ ] **Backend Team:** Implement payment entry creation when invoice is matched to bank transaction (OS-2921)
- [ ] **Backend Team:** Implement invoice status update logic (PAID vs PARTIALLY_PAID)
- [ ] **Backend Team:** Implement CSV export endpoint for matched payments with EXTF_*.csv format
- [ ] **Frontend Team:** Implement export button in matched payments UI (OS-3086)
- [ ] **Finance Team:** Document exact DATEV CSV format requirements
- [ ] **Finance Team:** Define auto-matching rules and criteria
- [ ] **Team:** Test payment matching workflow end-to-end
- [ ] **Team:** Measure payment matching rate and identify improvement opportunities

---

**Document Status:** Updated to include payment matching and recording process (2026-02-19)
**Next Review:** After payment matching implementation and Q1 2026 goal evaluation
**Maintenance:** Update as payment matching process evolves and DATEV integration is refined
