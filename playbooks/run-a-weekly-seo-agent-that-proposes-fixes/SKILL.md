---
name: run-a-weekly-seo-agent-that-proposes-fixes
description: "Run a weekly SEO agent that checks your site and opens fixes for you to review. Each week you get a short report with numbers and their sources, and one or more pull requests that fix real SEO problems on your site."
license: CC-BY-4.0
metadata:
  author: "Ilias Ism (seo-skills); Agents Handbook editors"
  source: https://agentshandbook.com/p/run-a-weekly-seo-agent-that-proposes-fixes
  version: "2026-10-13"
---

# Run a weekly SEO agent that checks your site and opens fixes for you to review

Source: https://agentshandbook.com/p/run-a-weekly-seo-agent-that-proposes-fixes (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/run-a-weekly-seo-agent-that-proposes-fixes.md

Give a coding agent an seo folder in your site's repository to hold its memory: product facts, a keyword map, a backlog and a log. Each week it checks site health, pulls Search Console changes, ships one fix from the top of the backlog as a pull request, and writes a short report. You merge what you approve. It never sends email, posts, creates accounts or publishes without you.

## Stop and ask the user

- Review and merge every pull request yourself.
- Read every new article before it goes live.
- Approve any redirect or deletion of a page that gets traffic or has links.
- Send any outreach, directory listing or social post yourself. The agent only drafts them.

## Steps

1. **Run the setup once by hand.** Start the agent in your site's repository with the prompt. On the first run it builds the seo folder, the product facts, the keyword map and the backlog, and then stops. Check: The seo folder exists, and every fact in context.md has a source.
2. **Correct the product facts.** Read context.md. Fix any wrong price, feature or claim. The agent repeats these facts on your pages, so they must be right. Check: You would sign off on every line in context.md.
3. **Reorder the backlog.** Move the items closest to sales to the top. Remove ideas you do not want. Check: The top three items are ones you want done.
4. **Schedule the weekly run.** Run the same prompt once a week from a scheduler. Give it read access to Search Console and the right to open pull requests, but not to merge or deploy. Check: The first scheduled run opens a pull request and writes a report.
5. **Review the pull request and the report.** Read the diff and the report. Check that every number in the report names its source. Check: You merged, edited or closed the pull request.
6. **Read new articles before they go live.** If the agent drafts an article, read it in full and check its facts before you merge. Unchecked, scaled content can break Google's spam policies. Check: Every live article had a human read.
7. **Review the trend every month.** Look at four weekly reports together. Keep the routines that moved clicks or conversions, and drop the rest. Check: You know which part of the routine earns its time.

## Known failures

- The agent forgets earlier decisions and redoes work. Fix: Keep all state in the seo folder, and make the first instruction of every run to read it.
- The agent states an old price or a feature you removed. Fix: Build context.md from the code and the live pricing page, and fact-check the pages after every commit that changes them.
- The agent publishes many thin pages. Fix: Google treats mass-produced pages with little value as spam. Allow at most one shipped item per run, and read every new page.
- The report claims pages are indexed or ranked without checking. Fix: Require a source for every number, and the words "not verified" when there is none.
- You credit the agent for a gain it did not cause. Fix: AI assistants often cite brands because of third-party coverage built over years. Compare against pages the agent did not touch before you credit it.

## Starting prompt

```text
You run SEO for [https://example.com] in this repository. Product: [one sentence]. Conversion: [signup, demo booked]. Competitors: [names, or "find them"]. Ship mode: open a pull request for review. Never merge.

You keep no memory between runs. All state lives in the seo/ folder. Read it at the start of each run and update it before you finish:
- seo/context.md: product facts, prices, features and claims, each with the file or URL it came from. Build it from the code and the live pricing page, never from memory.
- seo/keyword-map.csv, seo/backlog.md (ordered by expected conversions per hour of work), seo/log.md (one dated line per change).

Each run:
1. If seo/ does not exist, set it up: read the repository, write context.md, build the keyword map, crawl the site, write the backlog, and stop.
2. Health check: request every sitemap URL. Flag non-200 pages, redirect chains, wrong canonicals, stray noindex rules, broken internal links, orphan pages, and missing or duplicate titles.
3. Fact check: read the commits since the last run. If a price, plan, limit or feature changed, fix every page that states the old fact.
4. Search Console: pull the queries in positions 8 to 20 and pages that lost clicks against the previous period. Add the best items to the backlog.
5. Ship one item from the top of the backlog as a pull request. Run the lint, type check and build first.
6. Write seo/reports/YYYY-MM-DD.md in under 300 words: what shipped, what moved (each number with its source), what is broken, and up to three things you need from me.

Rules: never invent a statistic, quote, customer, review or price. Say "not verified" when you cannot check something. Do not send email, submit listings, create accounts or post anywhere: draft these in seo/ for me. Do not delete or redirect a page with traffic or links without flagging it first. If the same fix fails twice, stop and report it.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"run-a-weekly-seo-agent-that-proposes-fixes","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
