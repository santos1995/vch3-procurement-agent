# VCH3 Procurement Agent

AI-assisted procurement: from site requirement to vendor comparative.

Built at Vibe Coders Hackathon Edition 3 (Kolkata, 21 Nov 2026) for the Vinayak Group problem statement. All code in this repo was written during the hackathon.

**Live app:** https://santos1995.github.io/vch3-procurement-agent/
**Repo:** https://github.com/santos1995/vch3-procurement-agent

## What it does

A procurement assistant for a construction site workflow:

1. **Site requirement in.** Describe the requirement in plain words (for example, a waterproofing BOQ with items in SQFT / RMT) or paste an indent note.
2. **Parse to a structured BOQ.** The requirement is turned into line items with quantities and units. The current parser is deterministic and rule-based; it is labeled as such in the UI and is not presented as an LLM.
3. **Vendor quotes in.** Add vendor quotes in different layouts (per-item rate tables, lump-sum lines, scanned-PDF style text). The parser handles the supported formats and says plainly when a format is not understood instead of guessing.
4. **Comparative statement.** Quotes are normalized into a side-by-side comparative: item-wise lowest rate, line totals, taxes (GST), freight and payment terms where present. Unknown units or missing fields are flagged, never silently converted or invented.
5. **Recommendation with reasons.** The agent ranks vendors and gives a plain-words reason for every ranking (rate advantage, terms, completeness of quote). It recommends; it never selects, orders or pays. Past-performance scores shown in the demo are SIMULATED and labeled as such; no real vendor performance records exist.
6. **Draft output for approval.** The output is a draft comparative and recommendation for a human (HOD) to review and approve. Changing the requirement invalidates an earlier approval so stale drafts cannot be signed off.

## What is real and what is synthetic

- The problem statement, the site name and the BOQ structure come from the hackathon's public Vinayak Group brief.
- All vendor names, rates, quote values and performance scores in the app are invented demo data. They do not come from any real commercial document and must not be treated as real prices.
- No real vendor is ever contacted by this app.

## Boundaries

- The agent recommends and drafts. It never selects a vendor, places an order, sends email to a vendor, or makes a payment.
- Every ranking carries a plain-words reason.
- Deterministic logic is labeled rule-based; nothing rule-based is claimed to be AI.

## Tech

- Single static page (HTML/JS), hosted on GitHub Pages. No login required.
- Rule-based parsing and ranking engine in the page.
- AI drafting layer (Sarvam 105B via a hardened Cloudflare Worker proxy with per-call caps and a persistent budget counter) is being integrated with an honest UI badge; the rule-based engine remains the fallback. The README will be updated when that layer is verified live end-to-end.

## Repo layout

- `index.html` - the whole app (UI + rule-based engine + demo data).
