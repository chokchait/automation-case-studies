# Bloom: a hotel sales workspace from proposal to performance review

**Status:** Built and iterated  
**Platform:** Google Apps Script + Google Sheets  
**Scope:** Proposals, quotations, invoices, pipeline, reporting, and PDF export

## The problem

Hotel sales work rarely ends at creating a quotation. A salesperson needs to keep
customer and hotel context together, follow proposal status, produce documents,
understand what was won or lost, and explain performance to management.

When those steps live in separate spreadsheets and documents, the team spends time
reconciling versions instead of moving a deal forward.

## The system

Bloom is a single sales workspace backed by Google Sheets. It connects:

1. Customer, contact, hotel, stay, and commercial details
2. Proposal stages and follow-up dates
3. Quotation and invoice PDF generation
4. Won revenue, open pipeline, win rate, average deal, and room-night metrics
5. Monthly, quarterly, and annual periods with year-on-year comparison
6. Executive and detailed management reports

The screen and PDF outputs read from the same report model. That prevents a metric
from meaning one thing in the app and another thing in a management document.

## Design decisions that mattered

**The salesperson is the primary user.** Management receives the report, but the
workflow must remain fast for the person entering and following each proposal.

**Check-in date defines the reporting period.** One explicit date rule keeps month,
quarter, year, and prior-year comparisons consistent.

**Deterministic management signals.** Risks such as below-target performance,
customer concentration, low win rate, and overdue pipeline come from transparent
rules rather than generated narrative.

**Documents are part of the product.** Quotations, invoices, executive summaries,
and detailed appendices use the same source data as the working screens.

## What this demonstrates

- Translating a real sales process into a usable data model
- Building operational software inside a familiar Google Workspace environment
- Designing reports around management decisions, not decorative dashboards
- Handling empty periods, missing targets, long names, and print constraints

No customer records or production spreadsheet data are included in this repository.

