# Payout Logic

## Overview

Every month, Legalhero runs a payout process to pay out partner lawyers for completed mandates. The payout is written as a SEPA file and sent to the bank.

## How the Payout Is Calculated

The payout is calculated per **legal field (Rechtsgebiet)**. Each lawyer's total payout is the sum of all invoice amounts across all their legal fields.

## Negative Invoices (Gutschriften)

It can happen that an advance invoice in a case is higher than the final invoice. In this situation:

1. A **negative invoice** (Gutschrift) is created for the difference.
2. An **accounting task** is created for the finance team.
3. Accounting pays back the difference to the insurance (RSV) and **checks off the task**.
4. Once the task is checked off, the negative invoice is **included in the next payout cycle**.

## Known Issue & Fix (Sprint 33 — OS-3133)

**Problem:** The payout validation previously checked negativity at the **per-legal-field level**. If a single negative invoice was the only entry in a legal field (e.g., only a Gutschrift in "Arbeitsrecht"), the total for that field would be negative — causing the entire SEPA file generation to fail and blocking the complete monthly payout.

**Fix:** The negativity check is moved to the **total payout level**. As long as the lawyer's overall payout total (sum across all legal fields) is not negative, the payout proceeds. Only a negative overall total blocks the SEPA generation.
