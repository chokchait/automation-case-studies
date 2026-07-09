# The lead-gen agent: scrape, dedupe, outreach, CRM

**System:** B2B merchant acquisition pipeline across 6 APAC markets (TH, SG, MY, HK, TW, PH)
**Stack:** n8n · Google Maps API · Zoho CRM · LLM APIs · Google Sheets · Slack
**Status:** in production, used daily by BD teams

## The problem

Our BD teams acquire restaurant merchants. Before this system, the top of the funnel was a person with a spreadsheet: search for restaurants in a district, copy names and phone numbers into a sheet, check one by one whether we already work with them, then start messaging. Every market did this its own way, and every market did it slowly.

The wasteful part wasn't any single step. It was that the whole chain lived in someone's head, so it only ran when that someone had a free afternoon.

## How it works

The pipeline has five stages, all in n8n:

1. **Scrape.** A request comes in through Slack ("lead gen for Bangkok, cafe segment"). The workflow pulls candidate businesses from the Google Maps API for that region and segment.
2. **Dedupe.** Every candidate is checked against the existing book of business in Zoho. Anything we already work with, or already contacted, drops out here. This stage is the one that bought the most trust: BD stopped worrying the system would embarrass them by cold-messaging an existing partner.
3. **Enrich and draft.** An LLM fills the gaps (category, size guess, talking points) and drafts personalised outreach per lead.
4. **Approve.** A human looks at the batch before anything sends. BD approves in the sheet; nothing goes out without that.
5. **Outreach and log.** Approved leads get email or WhatsApp sequences. Once a merchant responds, the workflow creates the Zoho Account, Contact, and Deal, logs the activity, and pulls email replies back into the sheet. Deal stage moves from Cold to Warm on reply.

From the BD side the whole thing is three steps: request, approve, follow up on the warm ones.

## Design decisions that mattered

**Slack as the front door.** BD lives in Slack, so the request interface is a bot, not a form on some internal page they'd have to remember. Adoption came almost entirely from this choice.

**Dedupe before enrich.** Enrichment costs money per lead and approval costs attention per lead. Filtering against the CRM first keeps both bills down and keeps the approval batch short enough that people actually read it.

**Per-market sub-workflows, one central writer.** Each market has its own sub-workflow (different languages, different segments, different quirks) but they all write to one place with one schema. When something breaks, there is exactly one sheet to look at.

**Human approval stays.** It would be easy to remove the approval step and call the system fully automated. We kept it. Outreach carries the brand, and a person who spends thirty seconds scanning a batch catches the weird cases a pipeline can't.

## What I'd do differently

The reply-handling loop grew organically and it shows: replies land in a sheet before they land in the CRM, which made sense when the sheet was the source of truth and makes less sense now. If I rebuilt it, replies would flow straight into the CRM and the sheet would just be a view.

I'd also add dead-letter handling earlier. The first version silently skipped leads that failed enrichment. Nobody noticed for weeks because the pipeline still produced plenty of output. Now failures go to their own channel.

## Results

- BD runs the entire flow in three steps, on their phone if they want
- One pipeline serves 6 markets with per-market behaviour
- The funnel runs on schedule instead of on spare afternoons

---

*The workflow JSON stays internal, but if you're building something similar and want to compare notes, my contacts are in the [profile](https://github.com/chokchait).*
