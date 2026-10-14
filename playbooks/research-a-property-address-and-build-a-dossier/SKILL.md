---
name: research-a-property-address-and-build-a-dossier
description: "Research a specific property address and compile a dossier on sales, zoning, and risk. You get a structured dossier covering the key data points for a specific property, with sources for each claim, ready to cross-check before you rely on it."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/research-a-property-address-and-build-a-dossier
  version: "2026-10-13"
---

# Research a specific property address and compile a dossier on sales, zoning, and risk

Source: https://agentshandbook.com/p/research-a-property-address-and-build-a-dossier (trust: reported, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/research-a-property-address-and-build-a-dossier.md

Give an AI agent a specific property address and ask it to produce a dossier covering comparable sales, zoning, schools, walkability, and risk. In a published four-way test, Perplexity Computer ranked first for accuracy and cited primary sources throughout. Claude Code and Claude Cowork each produced partial results with zoning errors or hedged values, and Manus hallucinated comparables and returned broken links. Always verify zoning and legal data against the official primary source before using the output professionally.

## Stop and ask the user

- Review all zoning data and comparable sales against primary sources before sharing with a client or using in a legal or financial context.

## Steps

1. **List the data points you need before you start.** Decide what your dossier must cover. The default prompt covers comparable sales, zoning, schools, walkability, and risk. Add or remove items for your use case before you paste it. Check: You have a complete list of data points and the full property address ready.
2. **Paste the prompt and let the agent run.** Give the agent the address and the full prompt. In a published four-way comparison, Perplexity Computer ranked first for accuracy and granularity, citing primary sources throughout. Check: The agent returns a structured response with sections for each data point and source links for most claims.
3. **Check every source link the agent provides.** Click each URL. Verify that the linked page actually says what the agent claims. In the same comparison, Manus returned broken links and invented comparables that did not match the address. Check: Each cited URL loads and confirms the fact attributed to it.
4. **Cross-check zoning data on the official planning portal.** Look up the address on your city's official zoning map. Claude Code contained zoning errors and Claude Cowork labelled a zoning class as "Likely" in the published test. Do not use an agent-supplied zoning code in a legal context without this step. Check: The zoning code on the official map matches what the agent reported.
5. **Verify comparable sales in a listing database.** Search Zillow, Redfin, or your MLS for recent sales near the address. Confirm that each comparable the agent listed is a real transaction with the price it reported. Check: You can find each comparable in a known listing database at the price the agent stated.
6. **Compile a verified dossier with honest gaps.** Keep only facts you confirmed. Flag any data point the agent could not source, or that you could not verify. A dossier with clear gaps is more useful than one filled with unverified guesses. Check: Every fact in your final dossier has either a primary-source link or an explicit "unverified" note.

## Known failures

- The agent invents comparable sales or returns broken links to listings. Fix: Cross-check every comparable against Zillow, Redfin, or your MLS. Manus hallucinated irrelevant comparables in a published four-way test on this exact task.
- The agent hedges on zoning with words like "Likely" or "approximately" instead of giving the confirmed code. Fix: Always look up the zoning code on the official city planning portal. Claude Cowork labelled a zoning class as "Likely" in the same test, which the author flagged as a professional risk.
- The agent gives a plausible but wrong legal or zoning detail with no source. Fix: Treat any unsourced zoning or legal claim as unverified. Ask the agent to provide the primary-source URL. If it cannot, verify manually before using the claim.

## Starting prompt

```text
Produce a comprehensive property research dossier for [409 Eastern Parkway, Brooklyn, NY 11225].

Include:
1. Comparable sales in the last 12 months within a 0.5-mile radius, with addresses and prices
2. Current zoning code and what it permits, with a direct link to the official zoning source
3. Ratings for the nearest public schools
4. Walk score, transit score, and bike score
5. Risk factors: flood zone, environmental hazards, noise

For every fact that has a primary source (city records, official databases), include the URL. If you cannot find a primary source for a fact, say so explicitly. Do not guess or estimate any zoning or legal detail. Mark uncertain claims as uncertain.

End with a one-paragraph risk summary for a prospective buyer.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"research-a-property-address-and-build-a-dossier","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
