# Buchungen Finance - Payment-to-Invoice Matching

**Category**: Finance
**Last Updated**: 2026-02-18

## Overview

This document describes the payment-to-invoice matching system that automates the reconciliation of incoming bank payments with invoices in our system, replacing the manual DATEV workflow.

## Problem Statement

Currently one Finance team member is spending 60 hours per week matching invoices with incoming payments.

## Current Flow

1. Finance exports bank transactions from DATEV Unternehmen Online
2. Finance exports invoices from CaseForce
3. Both datasets are imported into DATEV
4. Matching of payments to invoices happens manually inside DATEV

## Pain Points

- DATEV's matching capabilities are insufficient
- Finance spends ~50 hours per week manually matching payments to invoices
- High cognitive load and inefficiency
- Corrections in DATEV are hard to track and audit

## Goals

- Automate payment-to-invoice matching as much as possible
- Handle edge cases in CaseForce instead of DATEV
- Reduce manual effort for Finance to exception handling only

---

## Matching Logic

### Matching Statuses

The system categorizes each payment-to-invoice match into one of three statuses:

- **FULL**: Payment amount exactly matches the invoice amount
- **PARTIAL**: Payment amount partially covers the invoice amount (underpayment)
- **NONE**: No match could be established between payment and invoice

### Matching Process

1. System loads incoming payments from bank transactions
2. System loads invoices from CaseForce
3. Automated matching algorithm attempts to match payments to invoices based on:
   - Invoice number references in payment descriptions
   - Customer identifiers
   - Amount correlation
   - Date proximity
4. Each match is assigned a matching status (FULL, PARTIAL, NONE)

---

## Export Functionality

### Export Configuration

Finance users can export matched payments with flexible filtering:

- **Export ALL statuses**: Exports all matched payments regardless of status
- **Export specific status**: Select one or more statuses to export (e.g., "FULL only" or "FULL + PARTIAL")

### Export Behavior

When payments are exported:

1. User selects which matching statuses to include in the export
2. System generates the export file with selected payments
3. Exported payments are **removed from the default view**
4. Export is saved and becomes accessible via "View Past Exports"

**Important**: The export action marks these payments as "processed" and moves them out of the active work queue.

---

## View Management

### Default View

**Purpose**: Active work queue for Finance team

**Contents**:
- Only payments that have **not been exported yet**
- All matching statuses (FULL, PARTIAL, NONE)
- Represents pending work that requires review or action

**Behavior**:
- This is the landing view when Finance opens the matching tool
- Shows only unprocessed/non-exported payments
- Once a payment is exported, it disappears from this view

### View Past Exports Tab

**Purpose**: Historical record and audit trail

**Contents**:
- All previously exported payment batches
- Each export shows:
  - Export timestamp
  - Number of payments included
  - Matching statuses included
  - User who performed the export

**Behavior**:
- Accessible via dedicated "View Past Exports" tab
- Allows Finance to review past exports
- Provides audit trail for reconciliation
- Payments in this view are read-only (already processed)

---

## Edge Cases

### Double Payments / Overpayments

**Scenario**: Insurance companies sometimes overpay an invoice (multiple times per day)

**Requirements**:
- System must detect when a single invoice has received multiple payments
- Double payments should be **clearly visible in the matching table**
- Visual indicator or separate column to flag overpayment situations

**Indicators**:
- Same invoice number appears multiple times with different payments
- Total payment amount exceeds invoice amount
- Multiple payment dates for same invoice

**Handling**:
- Flag these cases prominently in the UI
- Finance team needs to manually review and process
- May require refund requests or invoice adjustments

---

## Business Rules

1. **Export Finality**: Once payments are exported, they cannot be returned to the default view (to maintain data integrity and audit trail)
2. **Status Filter Flexibility**: Users must be able to export any combination of matching statuses
3. **Default View Priority**: Default view only shows pending (non-exported) work to reduce cognitive load
4. **Overpayment Visibility**: Double payments must be immediately visible without requiring additional filtering

---

## Technical Considerations

### Data Flow
1. Import bank transactions → Import invoices → Run matching algorithm → Assign status
2. Present in default view → User reviews → User exports selected statuses
3. Move exported payments to historical view → Maintain audit trail

### Key Features
- Filter by matching status for export
- Automatic removal from default view post-export
- Historical export tracking
- Overpayment detection and flagging

---

## Dependencies

- **DATEV Unternehmen Online**: Source of bank transaction data
- **CaseForce**: Source of invoice data
- **Matching Algorithm**: Core logic for payment-to-invoice correlation

---

## Open Items

- Specific algorithm details for payment-to-invoice matching
- Export file format requirements (CSV, Excel, DATEV import format?)
- Retention policy for past exports
- User permissions for export functionality
- Notification/alert mechanism for double payments
- Handling of payment reversals or corrections
