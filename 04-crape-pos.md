# Crape POS: Thai-first shop operations on a phone

**Status:** Built  
**Platform:** Google Apps Script + Google Sheets  
**Scope:** Sales, purchases, cash position, estimated profit, menu, and reporting

## The problem

A small food shop does not need a heavyweight retail suite. It needs to record an
order quickly, understand what cash came in and went out, and answer practical
questions such as:

- Which fillings and combinations sell most often?
- How much was spent on ingredients and packaging?
- What is the difference between cash position and estimated product profit?
- Which menu shortcuts should be available during a busy selling period?

The interface also has to work in Thai, on a phone, with large touch targets.

## The system

Crape POS connects four operational views:

1. **Sell** — choose fillings, sauces, packaging, quantity, and common combinations
2. **Buy** — record ingredient and packaging purchases
3. **Performance** — review orders, revenue, cash position, estimated profit,
   best-selling fillings, and frequent combinations
4. **Setup** — manage menu choices, pricing by filling count, shortcuts, and cost assumptions

Sales and purchases are stored in Google Sheets. A local fallback keeps the interface
usable for preview and recovery scenarios.

## Design decisions that mattered

**Cash and estimated profit are separate.** Cash is sales minus actual purchases.
Estimated profit allocates ingredient, packaging, sauce, and batter cost to what was
sold. Showing both prevents one number from pretending to answer two questions.

**The selling screen is the shortest path.** The most common combinations become
quick actions, while less common options remain available without crowding the flow.

**Thai is the product language.** Labels, explanations, errors, and report language
were written for the operator rather than translated after the interface was built.

**Mobile first means touch first.** Navigation stays at the bottom, controls remain
large, and totals update close to the action that changed them.

## What this demonstrates

- Turning an informal business process into a lightweight operating tool
- Designing financial explanations for a non-technical operator
- Mobile-first Thai UX
- Building useful reporting without a separate analytics platform

The public write-up contains no real sales records.

