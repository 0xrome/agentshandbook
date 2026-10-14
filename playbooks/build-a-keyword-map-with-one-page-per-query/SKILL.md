---
name: build-a-keyword-map-with-one-page-per-query
description: "Build a keyword map that gives every page on your site one search query to own. One table that maps each query to one page, with intent and status, plus a backlog of gaps sorted by value."
license: CC-BY-4.0
metadata:
  author: "Ilias Ism (seo-skills); Agents Handbook editors"
  source: https://agentshandbook.com/p/build-a-keyword-map-with-one-page-per-query
  version: "2026-10-13"
---

# Build a keyword map that gives every page on your site one search query to own

Source: https://agentshandbook.com/p/build-a-keyword-map-with-one-page-per-query (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/build-a-keyword-map-with-one-page-per-query.md

Start from your buyers' problems, not from search volume. An agent lists the questions buyers ask at each stage, from first noticing the problem to comparing products, then joins them with your Search Console queries and your pages. Each page gets one main query. Two pages that chase one query get merged, and queries with no page become your content backlog. Take volumes from a real keyword tool, because agents guess numbers.

## Stop and ask the user

- Confirm the buyer, the product facts and the competitor list before the agent maps queries.
- Approve every merge or redirect of an existing page.

## Steps

1. **Write down the buyer and the product.** Give the agent one sentence on what you sell and who buys it, and your competitors. Correct its summary of your product before you go on. Check: The agent describes your product the way your best customer would.
2. **List buyer questions by stage.** The agent writes the questions people ask from the moment they notice the problem to the moment they buy. These often differ from the terms with the highest volume. Check: You have about 25 questions that sound like real people.
3. **Add your real query data.** The agent adds your Search Console queries. These show what Google already connects to your site. Check: Your top queries are in the list.
4. **Group by intent and assign one page.** Each group of queries with the same intent gets one target page. This step shows pages that compete with each other and topics you never covered. Check: Every group has one target page or a gap mark.
5. **Add real volumes.** Fill volume and difficulty from a keyword tool. Leave them empty where you have no data. Check: No number in the map is an estimate from the agent.
6. **Fix pages that compete.** For two pages on one query, pick the winner. Merge the weaker page into it with a redirect, or change its focus. Approve each change. Check: No query has two target pages.
7. **Turn gaps into a backlog.** Sort the gaps by closeness to a buying decision, then by volume. Comparison and alternative queries often come before broad guides. Check: You have a short, ordered list of pages to write.
8. **Update the map every month.** Add new queries, update positions and statuses, and remove dead ends. Check: The map has a last-updated date that is less than a month old.

## Known failures

- The agent invents search volumes or gives its own opportunity score. Fix: Leave volume and difficulty empty unless a keyword tool supplies them.
- The map chases big head terms you cannot win. Fix: Prefer specific, longer queries with clear intent. One team found a single brand word too competitive and moved to longer queries.
- Two pages keep targeting the same query. Fix: One query, one page. Merge the weaker page, redirect it, or give it a different focus.
- The map lists topics buyers never search. Fix: Start from buyer questions and check each group against real query data.
- The map goes stale after a month. Fix: Keep it in a file the agent updates, with a date column.

## Starting prompt

```text
Build a keyword map for [https://example.com]. Product: [one sentence on what it does and who buys it]. Competitors: [3 to 8 names, or "find them"].

1. Write the questions a buyer asks at each stage: unaware of the problem, aware of the problem, comparing kinds of solution, comparing products, and ready to buy. Write them the way a person types them into Google or an AI assistant. Give 5 per stage.
2. Add the search terms for the category, competitor names, "alternative to" and "vs" queries, integrations and use cases.
3. Add my real queries from [Search Console MCP / data/gsc-queries.csv] for the last [3] months.
4. Group the queries by intent. Give each group one main query.
5. Match each group to one existing page. If two pages target one group, flag it and say which page should win. If no page fits, mark it as a gap.
6. Output [seo/keyword-map.csv] with these columns: query, intent, stage, monthly volume, difficulty, target URL, status (live, planned, gap), current position.
7. Leave volume and difficulty empty unless they come from [keyword tool or export]. Never estimate them.
8. List the gaps as a backlog sorted by how close each one is to a buying decision. Wait for my review before you plan any content.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"build-a-keyword-map-with-one-page-per-query","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
