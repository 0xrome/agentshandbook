---
name: refresh-a-blog-post-that-lost-traffic
description: "Refresh a blog post that lost traffic with a gap analysis of the pages that outrank it. A refreshed post that covers what the top results cover and more, with the same URL and voice, and a plan you approved."
license: CC-BY-4.0
metadata:
  author: "Ilias Ism (seo-skills); Agents Handbook editors"
  source: https://agentshandbook.com/p/refresh-a-blog-post-that-lost-traffic
  version: "2026-10-13"
---

# Refresh a blog post that lost traffic with a gap analysis of the pages that outrank it

Source: https://agentshandbook.com/p/refresh-a-blog-post-that-lost-traffic (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/refresh-a-blog-post-that-lost-traffic.md

Find the posts that lose clicks by comparing two equal periods in Search Console. For one post, an agent reads the top five results for its main query, builds a table of what they cover and you lack, and proposes a new outline marked keep, change or new. You approve the plan before it writes. Keep the URL, the voice and the sections that already work, cite a source for every statistic, and change the visible date only when the content really changed.

## Stop and ask the user

- Approve the gap table and the new outline before the agent writes the new version.
- Check every new statistic, quote and example against its source before you publish.

## Steps

1. **Find posts that lose clicks.** In Search Console, compare the last three complete months with the three months before. Sort pages by lost clicks. Check the query impressions too. If people search less for the topic, a refresh will not fix it. Check: You have a short list of posts that lost clicks while demand held.
2. **Pick one post and its main query.** Start with the post that lost the most clicks on a query that matters to your business. Check: You know the post and the one query it should win.
3. **Let the agent read the results.** Paste the prompt. The agent searches the query and opens the top five pages. Ask it to list every URL it read. Check: The plan lists five competitor URLs it opened.
4. **Read the gap table.** Look for topics most competitors cover that your post lacks. Also look for an angle nobody covers, such as your own data or experience. Check: You can name the top three gaps.
5. **Approve the outline.** Check the keep, change and new marks. Protect sections that already bring traffic and any headings other pages link to. Check: You approved the outline, or edited it.
6. **Review the draft and check facts.** Read the refreshed post. Open the source for every number. Remove anything you cannot verify. Check: Every statistic has a working source and a year.
7. **Publish on the same URL.** Keep the URL. If you must change it, add a 301 redirect from the old one. Update the visible date only because the content changed. Check: The old URL loads the new post, or redirects to it.
8. **Measure after four weeks.** Compare clicks and positions for the post's queries over equal periods before and after. Check: You know if the refresh helped.

## Known failures

- The agent changes the date but little else. Fix: Google's guidance warns against changing dates to look fresh when the content did not change much. Change the date only after a real update.
- The agent describes the top results from memory. Fix: Require live search and a list of the URLs it opened.
- The agent adds statistics with no source, or with old sources. Fix: Require a source and a year for every number, and check each one.
- The new version copies the structure of the top result and loses your voice. Fix: Tell the agent to keep your voice and your strongest sections, and to add an angle the others do not have.
- Traffic fell because fewer people search the topic, not because of the post. Fix: Check the query impressions trend before you refresh. Compare complete periods of equal length.

## Starting prompt

```text
I want to refresh [https://example.com/blog/post] so it competes with the pages above it for [main query].

1. Read my post. Note its word count, headings, lists, tables, links, the date it shows, and its strong and weak sections.
2. Search [main query] now. Do not use memory. Note the top 10 titles, any featured snippet, the People Also Ask questions, and the main format of the results.
3. Open the top 5 results. For each one, record the headings, the topics, the data it uses, its examples, and its last updated date.
4. Build a gap table: one row per topic or element, one column per page, and a priority. High means 4 or more competitors cover it.
5. Propose 3 title options and a new outline. Mark each heading keep, change or new, and say why.
6. Stop and wait for my approval.
7. After I approve, write the refreshed post. Keep my URL, my voice and the sections that work. Put a direct answer near the top. Give every statistic a source and a year. Do not invent data, quotes or customers. Add an FAQ only for questions people really ask.
8. End with a note for me: new meta description, internal links to add, images needed, and the list of URLs you read.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"refresh-a-blog-post-that-lost-traffic","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
