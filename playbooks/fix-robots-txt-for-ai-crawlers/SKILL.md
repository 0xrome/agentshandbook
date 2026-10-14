---
name: fix-robots-txt-for-ai-crawlers
description: "Fix robots.txt so AI search crawlers can read your site. Your robots.txt allows the AI search crawlers you choose, keeps private paths blocked, and you have checked the live result."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/fix-robots-txt-for-ai-crawlers
  version: "2026-10-13"
---

# Fix robots.txt so AI search crawlers can read your site

Source: https://agentshandbook.com/p/fix-robots-txt-for-ai-crawlers (trust: reported, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/fix-robots-txt-for-ai-crawlers.md

Ask a coding agent to read your live robots.txt, list which AI crawlers it blocks, and edit the robots file in your repository. The most common bug is a named crawler group that has only "Allow: /". A crawler follows one group only, so that group must repeat every Disallow rule. Check the live file again after you deploy.

## Stop and ask the user

- Choose which crawlers to allow and which paths stay private before the agent edits anything.
- Review the diff before you deploy.

## Steps

1. **Decide what you want.** List the crawlers you want to allow and the paths that must stay private. Most sites allow the search crawlers (OAI-SearchBot, Claude-SearchBot, PerplexityBot) and decide about training crawlers (GPTBot, ClaudeBot) as a separate choice. Check: You have a short list of crawlers and private paths.
2. **Let the agent audit the live file.** Paste the prompt. The agent fetches the live robots.txt, finds the file that generates it (for example public/robots.txt or app/robots.ts in Next.js) and builds the table. Check: The table quotes the group each crawler follows.
3. **Review the proposed diff.** Check that every named group repeats the Disallow lines of the * group. A named group that says only "Allow: /" opens your private paths to that crawler. Check: Every group that you allow still blocks your private paths.
4. **Deploy and check the live file again.** After the deploy, ask the agent to fetch the live robots.txt and rebuild the table. Crawlers can take about a day to notice the change. Check: The new table matches what you decided in step 1.

## Known failures

- A named crawler group allows everything, including private paths. Fix: Copy every Disallow line from the * group into each named group. A crawler never merges groups.
- You block GPTBot and expect to leave ChatGPT search. Fix: OpenAI documents OAI-SearchBot as the crawler for ChatGPT search. GPTBot is the training crawler. Treat them as two decisions.
- You block Google-Extended to keep out of AI Overviews. Fix: Google says Google-Extended has no effect on Google Search. AI Overviews follow the Googlebot rules.
- robots.txt allows a crawler but it still gets no content. Fix: Check your CDN or firewall bot settings. Some hosts block AI crawlers by default even when robots.txt allows them.

## Starting prompt

```text
Read the live robots.txt at [https://yourdomain.com/robots.txt] and the file in this repository that generates it.
1. Make a table of these crawlers: GPTBot, OAI-SearchBot, ChatGPT-User, ClaudeBot, Claude-SearchBot, Claude-User, PerplexityBot, Googlebot, Bingbot. For each one, quote the group it follows and say if it may fetch [/, /pricing, /docs].
2. Propose the smallest change so that [the crawlers I want] are allowed and [/admin, /api] stay blocked for every crawler. Remember that a crawler obeys only its most specific User-agent group, so every named group must repeat the Disallow lines.
3. Show me the diff and wait for my approval before you change the file.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"fix-robots-txt-for-ai-crawlers","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
