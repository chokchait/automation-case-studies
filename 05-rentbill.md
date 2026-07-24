# RentBill: recurring apartment billing with two kinds of history

**Status:** Work in progress  
**Platform:** Google Apps Script + Google Sheets  
**Target scope:** One landlord, one building, up to 50 rooms

## The problem

Monthly apartment billing looks simple until meter readings, unpaid balances, and
tenant changes interact.

Two histories follow different objects:

- Electricity and water meters belong to the **room** and keep moving when a tenant changes.
- Unpaid debt belongs to the **tenancy** and must never be transferred to a new tenant.

A spreadsheet can store both, but it does not naturally enforce the distinction.

## The system

RentBill is being built around a five-step monthly workflow:

1. Enter electricity and water readings for occupied rooms
2. Generate the missing bills for the selected month
3. Add optional late fees
4. Print one combined PDF or export separate room files
5. Mark paid bills and issue receipts

Room records, bills, and settings live in three Sheets tabs. Each bill snapshots the
tenant name, rent, fixed fees, meter readings, rates, carried debt, due date, and
payment status so later master-data edits cannot rewrite history.

## Design decisions that matter

**Meter history is room-scoped.** A new bill starts from the latest reading for that
physical room, regardless of who occupied it.

**Debt history is tenancy-scoped.** A tenant sequence separates the previous tenant's
unpaid bills from the next tenant while preserving the old debt for follow-up.

**Generation is idempotent.** Running the same month again creates bills only for rooms
that are missing one instead of overwriting existing records.

**Paid bills lock.** Corrections are allowed while a bill is unpaid. Marking it paid
freezes the financial record.

**Thai documents are first-class output.** The product includes Thai invoices,
receipts, PromptPay details, combined printing, and per-room PDF export.

## Current progress

- Domain rules and server operations are implemented and covered by automated tests
- Room management and responsive application shell are implemented
- Meter entry, bill management, document styling, and live Apps Script verification
  remain in progress

This is intentionally labelled work in progress. No production outcome is claimed yet.

