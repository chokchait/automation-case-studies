# Campaign auto-setup: from hours to minutes

**System:** marketing campaign generator for push, EDM, in-app popups, and home banners across 7 markets (TH, MY, HK, PH, TW, SG, JP)

> **Scope note:** This case study documents the historical seven-market setup,
> including Japan. My current group scope covers six APAC markets:
> Thailand, Taiwan, Malaysia, Singapore, the Philippines, and Hong Kong.
**Stack:** n8n · CleverTap API · LLM APIs · APITemplate.io
**Status:** live for push and EDM; social automation in progress

## The problem

Running lifecycle marketing for two brands across seven markets means a lot of campaigns. At minimum two push campaigns a day per market, before counting email, in-app popups, and banners. Roughly 400 push sends a month.

Setting one up by hand takes a chain of small steps: name the campaign to convention, pick the segment, set the schedule in the right timezone, paste the copy for each locale, attach the creative, configure the trigger, test, launch. None of the steps is hard. All of them are manual, and each one is a chance to typo a market code at 6pm on a Friday.

We measured it: about 12 hours of manual setup per market per month. Across seven markets, about 84 hours. Call it four working hours handed back every single day.

## How it works

The whole thing collapses into one form.

A marketer fills in the campaign brief: market, objective, segment, schedule window, and the content angle. From there the workflow takes over:

1. **Naming.** Campaign names are generated to convention automatically. Nobody types `TH_push_reactivation_2026-07_v2` by hand anymore, which also means the analytics dashboards stopped filling up with almost-matching name variants.
2. **Copy.** An LLM drafts the message per locale. Humans review and edit; the draft is a starting point, not the final word.
3. **Payload.** The workflow assembles the full campaign payload (segment reference, schedule, creative slots) and calls the CleverTap API to create the campaign, with every call logged.
4. **Creative.** Banner-style assets come from templates through APITemplate.io, so a campaign that needs an image doesn't need a designer for the routine cases.

Setup time per campaign went from hours to minutes. The 84 hours a month the team gets back go into the parts machines are bad at: deciding what the campaign should say, and whether it should exist at all.

## Design decisions that mattered

**One form, not one tool per channel.** The temptation was a push tool, then an EDM tool, then a banner tool. One brief that fans out per channel keeps the mental model flat: the marketer describes the campaign once.

**Logging on every API call.** When a campaign looks wrong in CleverTap, the first question is always "what did we actually send?" The log answers it in seconds. This was retrofitted after a confusing week; build it in from day one.

**AI drafts, humans approve.** Same rule as our lead-gen system. The LLM produces the first draft and the localisation; a person signs off. Marketing copy across seven locales is exactly the kind of surface where silent AI mistakes get expensive.

**Convention as code.** The naming convention used to live in a wiki page nobody read. Now it lives in the workflow, so it's simply impossible to name a campaign wrong.

## What I'd do differently

Start with fewer channels. The first version tried to cover push, EDM, and in-app at once, and debugging three integrations at the same time slowed the whole rollout. Shipping push alone first would have put real value in front of the team a month earlier.

## Results

- Campaign setup: hours to minutes
- About 84 hours of manual work returned to the team monthly, roughly 12 hours per market
- 2+ push campaigns a day per market run through the pipeline
- Naming and structure are consistent by construction, which quietly fixed reporting too

---

*Questions or building something similar? Contacts in the [profile](https://github.com/chokchait).*
