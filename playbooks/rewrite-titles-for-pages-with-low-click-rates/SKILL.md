---
name: rewrite-titles-for-pages-with-low-click-rates
description: "Rewrite title tags and meta descriptions for pages that get impressions but few clicks. Your weakest pages get titles and descriptions that match the queries people type, and you have a dated log to measure the change."
license: CC-BY-4.0
metadata:
  author: "Ilias Ism (seo-skills); Agents Handbook editors"
  source: https://agentshandbook.com/p/rewrite-titles-for-pages-with-low-click-rates
  version: "2026-10-13"
---

# Rewrite title tags and meta descriptions for pages that get impressions but few clicks

Source: https://agentshandbook.com/p/rewrite-titles-for-pages-with-low-click-rates (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/rewrite-titles-for-pages-with-low-click-rates.md

Give an agent your Search Console data by page and query. Ask it to list pages with many impressions and a low click rate for their position. For each page it compares the title with the queries people type, drafts three title options and a new description, and shows you a before and after table. Change only the rows you approve, leave a few similar pages alone as a holdout, and compare clicks after three to four weeks. A rewrite can lower clicks too, so measure it.

## Stop and ask the user

- Approve the before and after table, row by row, before the agent edits any file.
- Review the diff before you deploy.

## Steps

1. **Get the data.** Connect a Search Console MCP server, or export the Performance report by page and by query for the last 28 days. Use complete days only. Check: The agent can list your top pages with impressions, clicks and average position.
2. **Find pages that lose clicks.** Paste the prompt. The agent lists pages that show up often but get few clicks for their position. These pages already rank, so a better title can help without new content. Check: You have a short list sorted by lost clicks.
3. **Read the queries for each page.** For each page, look at the queries that bring the impressions. The title often answers a different question. In one report, a guide titled for trading got its impressions from queries about investing. Check: Each page has a short note on what searchers want.
4. **Check that the page keeps the promise.** A title that promises more than the page delivers can earn a click and then lose the visitor. Ask the agent to compare each new title with the page content. Check: Every new title describes something the page really has.
5. **Approve the table.** Read the before and after table. Reject titles that are too long, stuffed with keywords, or vague. Check the character counts. Check: Each row is approved, edited or rejected.
6. **Fix shared templates once.** If many pages share one description template, fix the template so it uses real data from each page, such as a name, a price or a count. This changes many pages with one edit. Check: Two pages from the same template now show different, specific descriptions.
7. **Apply, deploy and log.** The agent edits the approved pages and leaves the holdout pages alone. It adds the date and the old and new titles to the log. Check: The log has one line per changed page.
8. **Measure after three to four weeks.** Compare clicks and click rate for the same queries over two equal periods, before and after. Compare the changed pages with the holdout pages. Search the main query to see which title Google shows. Check: You know which changes helped, and you revert the ones that did not.

## Known failures

- The agent writes titles that break its own length rule. Fix: Ask for a character count in the table and reject anything over your limit. In one published case study, the new titles ran far past the 60-character rule the authors set.
- You change every title at once and cannot tell what worked. Fix: Change pages in batches, keep a holdout group, and log the date of each change.
- Google shows a different title than the one you wrote. Fix: Google builds title links from several sources. Keep each title unique, descriptive and short, and keep it close to the H1.
- Many pages share one generic description. Fix: Fix the template so each page fills in its own specific details.
- The new title wins clicks but visitors leave at once. Fix: The title promises more than the page gives. Rewrite the title to match the page, or improve the page.

## Starting prompt

```text
Use Search Console data for [https://example.com] for the last [28] days, by page and by query. [Use the connected Search Console MCP server. / Use the exports in data/gsc-pages.csv and data/gsc-queries.csv.]

1. List pages with at least [500] impressions and an average position between [1] and [15] whose click rate is low for that position. Sort them by the clicks they lose.
2. For the top [20] pages, show the queries that bring the impressions, the current title, the H1, the meta description, and what the page content actually delivers.
3. Name the mismatch for each page. For example: the title says one thing and the queries ask for another, the main query word is missing, the title gets cut off, the brand appears twice, or many pages share one template description.
4. Write 3 title options per page. Put the main query near the front. Aim for 40 to 60 characters. Promise only what the page delivers. Pick the best one, and write a meta description of 140 to 155 characters that names something specific from the page.
5. Show me one table: page, top queries, current title, new title with character count, new description, reason. Do not change any file yet.
6. When I approve rows, edit only those pages, in the way this repository sets metadata. Leave [5] similar pages unchanged as a holdout. Add a dated line per change to [seo/log.md].
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"rewrite-titles-for-pages-with-low-click-rates","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
