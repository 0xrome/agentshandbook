---
name: move-pages-from-page-two-onto-page-one
description: "Move pages that rank on page two of Google onto page one with Search Console data. A short list of pages close to page one, each with changes you approved and a date to check the result."
license: CC-BY-4.0
metadata:
  author: "Ilias Ism (seo-skills); Agents Handbook editors"
  source: https://agentshandbook.com/p/move-pages-from-page-two-onto-page-one
  version: "2026-10-13"
---

# Move pages that rank on page two of Google onto page one with Search Console data

Source: https://agentshandbook.com/p/move-pages-from-page-two-onto-page-one (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/move-pages-from-page-two-onto-page-one.md

Ask an agent to pull the queries where your pages rank in positions 8 to 20 and get real impressions. For each query, it reads the top three results, explains why they rank above you, and proposes changes to your page: answer the query early, add the missing section, and add links to the page from your strongest related pages. You approve each change. Expect movement to take weeks, and measure the same queries over equal periods.

## Stop and ask the user

- Approve the plan for each page before the agent writes anything.
- Check every new fact and number against a source before you publish.

## Steps

1. **Pull the page-two queries.** Paste the prompt. Work with query and page pairs, not page averages. One page can rank third for one query and thirtieth for another. Check: You have a list of pairs in positions 8 to 20, sorted by impressions.
2. **Read the pages that beat you.** The agent searches each query and opens the top three results. It writes down what they cover, how they answer, and how fresh they are. Check: Each pair has a short note on why the top results win.
3. **Check for two pages on one query.** If two of your pages rank for the same query, they compete. Pick one to own the query. Link the other one to it, or merge them. Check: Each query has one owner page.
4. **Approve the plan.** Read the proposed changes. Cut anything that adds length without answering the searcher. Check: Each page has a short, approved list of changes.
5. **Make the changes.** The agent puts the answer near the top, adds the missing section with sources, and adjusts the title and H1 where it reads well. Check: The page answers the query in its first two sentences.
6. **Add internal links.** Add links from your strongest related pages with anchor text that describes the target page. Read each link in its sentence. Check: The page has at least three new, relevant internal links.
7. **Measure after three to four weeks.** Compare position, impressions and clicks for the same query and page over two equal periods. Rankings often move up and down in the first days. Check: You know which pages moved, and you plan the next batch.

## Known failures

- The agent pads the page with generic text to match the length of competitors. Fix: Add only what the searcher needs. Google's guidance says adding content only to look fresh or long does not help.
- Two of your pages compete for the same query and neither one moves. Fix: Pick one page to own the query, link the other to it, or merge them and redirect the weaker one.
- The agent describes the search results from memory. Fix: Make it search and open the pages, and list the URLs it read in the plan.
- The agent adds a statistic or a quote with no source. Fix: Require a source link for every number, and check it before you publish.
- You judge the result after a few days. Fix: Wait three to four weeks and compare equal periods.

## Starting prompt

```text
Use Search Console data for [https://example.com] for the last [28] days, by query and page.

1. List query and page pairs with an average position between [8] and [20] and at least [200] impressions. Sort by impressions.
2. For the top [10] pairs, search the query and open the top three results. For each pair, explain why those pages rank above mine. Look at how well they match what the searcher wants, sections I lack, fresher data, and links.
3. Check if another page on my site also ranks for the same query. If so, say which page should own the query.
4. For each pair, propose specific changes:
   - Answer the query in the first two sentences of the page.
   - Add the missing section, using only facts from sources you name.
   - Put the query in the title and H1 if it reads naturally.
   - List [3] pages on my site that should link to this page, with the anchor text and the sentence where the link goes.
5. Write the plan to [seo/page-two-YYYY-MM-DD.md] and wait for my approval. Do not invent statistics, quotes or customer stories.
6. After I approve, make the changes and log the date per page in [seo/log.md].
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"move-pages-from-page-two-onto-page-one","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
