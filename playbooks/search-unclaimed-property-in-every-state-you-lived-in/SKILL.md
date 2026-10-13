---
name: search-unclaimed-property-in-every-state-you-lived-in
description: "Search for unclaimed money under every name and in every state you have lived in. You get a table of real matching records from official state sites, each with a link, and you file the claims you choose on those sites yourself."
---

# Search for unclaimed money under every name and in every state you have lived in

Source: https://agentshandbook.com/p/search-unclaimed-property-in-every-state-you-lived-in (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/search-unclaimed-property-in-every-state-you-lived-in.md

List every name you have used and every state you have lived or worked in. Have a browser agent open only the official state programs linked from unclaimed.org, run each search, and copy every matching record with its source link into a table. You solve any CAPTCHA, enter your SSN and file each claim yourself. Public accounts report one $500 find, and also people who got only website names instead of real records.

## Stop and ask the user

- Approve the list of official state sites before the agent searches.
- Solve any CAPTCHA and type your SSN or ID details yourself.
- Review each record and file each claim yourself on the official site.

## Steps

1. **List your names and places.** Write every name you have used and every state and city where you lived, worked or had a bank account. Add businesses you owned. Ask relatives for old addresses if you are unsure. Check: You have one list of names and one list of places with years.
2. **Get the official sites only.** Have the agent build the list from the unclaimed.org state map and MissingMoney.com. NAUPA says searching and claiming are free through the official state program. Any site that asks for a fee or a bank login is not the official program. Check: Every site on the list is linked from unclaimed.org.
3. **Run the searches and collect real records.** The agent searches each site under each name and copies the matches with their page links. Some sites cap results for common names or hide exact amounts, so narrow by city. One commenter warns that an agent must cite the exact record, or it may describe a site it never opened. Check: Every row in the table has a record ID and a link that opens the record.
4. **Check the gaps yourself.** Look at the "could not check" list and search those sites by hand. Some states hide small amounts online. Bridge Michigan reports that Michigan lists only properties of $50 or more online, and smaller ones need a phone call. Check: Every state on your list is either searched or marked for a call.
5. **File each claim yourself.** Open each record on the official site, solve any CAPTCHA, and enter your details yourself. Keep a copy of each claim number. Check: You have a claim number or confirmation for each record you filed.

## Known failures

- The agent names the websites to check but does not return real records. Fix: Require a record ID and page URL for every row, and a separate list of sites it could not search.
- A shared prompt does not work in another assistant, or does nothing at all. Fix: Use an agent that can browse, such as Claude in Chrome or ChatGPT agent, and give it the official links directly.
- A CAPTCHA blocks the claim step, or the site asks for an SSN. Fix: That step is yours. Solve the check and type identity details yourself. Do not ask the agent to get around it.
- A common name returns too many results, or the amount shows only as a range. Fix: Narrow by city or ZIP, and treat range amounts as text, not numbers.
- Small amounts do not appear online in some states. Fix: Call the state program for amounts below its online limit.

## Starting prompt

```text
Help me find unclaimed property held by US states. Search only. Do not file claims.

Names to search: [current full name], [former or maiden names], [common misspellings]
Places I have lived or worked: [state, city, years] for each place
Businesses I owned, if any: [business names]

1. Start at https://unclaimed.org/ and use its map to get the official program link for each of my states. Also note MissingMoney.com, which searches many states at once. Use only these official sites. Ignore ads and any site that asks for a fee.
2. STOP and show me the list of sites. Wait for my OK.
3. For each site and each name, run the search and narrow by city if there are many results. Copy every possible match into a table: state, name on record, last known address, holder (company), property type, amount exactly as shown (for example "UNDER $100"), record ID, and the page URL.
4. Only include records you actually saw on the page. If a site blocks you, shows a CAPTCHA or caps the results, say so in a "could not check" list. Never guess.
5. Stop before any "file claim" step. Never type my SSN, date of birth or ID numbers.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"search-unclaimed-property-in-every-state-you-lived-in","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.