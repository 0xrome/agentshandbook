---
name: turn-scattered-travel-records-into-a-mapped-diary
description: "Turn scattered travel records into an interactive mapped diary. You get a single HTML file that maps your destinations, totals your nights and mileage, and splits personal from business travel, covering as much of your history as your records allow."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/turn-scattered-travel-records-into-a-mapped-diary
  version: "2026-10-13"
---

# Turn scattered travel records into an interactive mapped diary

Source: https://agentshandbook.com/p/turn-scattered-travel-records-into-a-mapped-diary (trust: reported, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/turn-scattered-travel-records-into-a-mapped-diary.md

Gather every piece of travel evidence you can find, including spreadsheets, hotel loyalty histories, airline booking records, calendar exports, and written notes from memory, then paste the combined data into ChatGPT in one session. Ask it to identify every trip, estimate totals, and produce a static HTML page with an interactive map, a sorted trip list, and a summary table for nights, distance, cost, and carbon footprint. Andrew Blumhardt reports doing this in about 30 minutes and recovering roughly 85 percent of his reconstructible travel history, with gaps only where records never existed.

## Steps

1. **Collect every record source you can find.** Pull together spreadsheets, hotel loyalty histories, airline booking pages, calendar exports, credit card statements, and notes written from memory. Blumhardt found that financial records, photos with location data, social media posts, and calendar entries can fill surprising gaps even when dedicated travel apps run out of history. Check: You have at least one document or file covering each period you want to reconstruct.
2. **Consolidate into a single paste.** Copy all your records into one text document or a simple spreadsheet. Remove sensitive account numbers but keep dates, destinations, durations, and trip types. PDFs can be pasted as plain text. Check: Your records are in one place and ready to paste.
3. **Open a new ChatGPT chat and paste the prompt with your records.** Start a fresh conversation, paste the prompt above, and replace the placeholder with your records. For very large sets, paste in batches and ask ChatGPT to build a running trip list after each batch before moving on. Check: ChatGPT acknowledges the data and begins listing identified trips.
4. **Review the trip list for errors before asking for HTML.** Read through the identified trips carefully. Correct any dates or destinations that look wrong, clarify which trips were personal versus business, and point out any obvious missing trips. This is your only chance to fix the data before the output is generated. Check: The trip list matches your memory for the trips you can verify.
5. **Ask for the HTML page.** Once the trip list looks right, ask ChatGPT to generate the full HTML file with the map, sorted trip list, and summary table. Copy the entire HTML output and save it as a file ending in .html. Open it in any web browser. Check: The file opens, the map shows your destinations, and the summary table has totals for nights, distance, cost, and carbon.
6. **Note gaps and decide whether to fill them.** ChatGPT will flag periods with thin data. Decide whether to do another pass with more records or accept the coverage you have. Blumhardt estimates the ceiling is about 85 percent of reconstructible history when all the sources above are combined. Check: You know which periods are well covered and which remain incomplete.

## Known failures

- Travel app exports only go back a few years and miss older trips. Fix: Supplement with financial records, photos with location data, social media posts, and hotel or airline loyalty account histories, which sometimes hold longer records. Memory notes are also valid inputs.
- A large record set exceeds the context window and some trips are dropped silently. Fix: Paste records in batches of a few hundred lines at a time, ask ChatGPT to maintain a running trip list after each batch, and do a final pass asking it to check for duplicates and missing periods.
- The generated HTML map does not display because the mapping library needs an internet connection or an API key you do not have. Fix: Ask ChatGPT to rewrite the map section using a library that works without an API key, such as Leaflet with OpenStreetMap tiles, or export just the coordinates and paste them into a free mapping tool separately.
- Personal and business trips are split incorrectly. Fix: Add a column to your source data marking trip type before you paste, or tell ChatGPT your employer name and common business destinations so it can make a better-informed split.

## Starting prompt

```text
I want to reconstruct my travel history from the records I will paste below.

Records:
[Paste your spreadsheets, hotel stays, flight records, calendar entries, and any other travel data here. Paste in batches if the total is large.]

Please do the following:
1. Parse every trip you can identify: destination, approximate dates, duration in nights, and whether it was personal or business.
2. Estimate total nights away, total distance traveled in [kilometers or miles], and rough total cost in [your currency] if you can infer it from the data.
3. Estimate a rough carbon footprint for flights, using average economy-class figures.
4. Flag any gaps, conflicts, or periods where the data is thin.
5. Produce a static HTML page that includes:
   - An interactive map of all destinations
   - A trip list sorted by date with personal/business label
   - A summary table with totals for nights, distance, cost estimate, and carbon estimate

Do not invent dates, destinations, or figures I did not provide. Mark estimates clearly as approximate.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"turn-scattered-travel-records-into-a-mapped-diary","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
