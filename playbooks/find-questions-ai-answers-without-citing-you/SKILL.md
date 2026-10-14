---
name: find-questions-ai-answers-without-citing-you
description: "Find the questions AI assistants answer without naming your brand, and plan content to fix it. You get a table of buyer questions with your mention rate, competitors' mention rates and cited sources per assistant, plus a short content plan for the biggest gaps that you approve."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/find-questions-ai-answers-without-citing-you
  version: "2026-10-13"
---

# Find the questions AI assistants answer without naming your brand, and plan content to fix it

Source: https://agentshandbook.com/p/find-questions-ai-answers-without-citing-you (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/find-questions-ai-answers-without-citing-you.md

Write the questions your buyers ask, run each one many times across several AI assistants, and record how often your brand and your competitors appear and which pages get cited. Gaps are questions where competitors show up and you do not. Plan one useful page or fix per gap. A large SparkToro study found AI brand lists change from run to run, so one check proves nothing. Measure presence over many runs, not rank.

## Stop and ask the user

- Approve the list of buyer questions before the agent runs them.
- Approve the content plan before anything is written.
- Review and publish each page yourself.

## Steps

1. **Collect buyer questions.** Pull questions from sales calls, support tickets, Search Console and community threads. Keep the buyer's words. Check: You have 15-40 questions that a buyer would really type.
2. **Run each question many times.** Run each question at least five times per assistant in fresh, logged-out sessions. SparkToro's study found brand lists almost never repeat exactly between runs, and commenters report location and account history change answers too. Check: Every question has several runs per assistant with the date recorded.
3. **Compute mention rates and find gaps.** Let the agent compute your mention rate and each competitor's rate, and flag gaps. Ignore position in the list. Check: The table shows rates per question and per assistant.
4. **Read the cited pages.** For each gap, open the pages the assistants cite. Look for what they explain that you do not, and for third-party sites (directories, reviews, Wikipedia-style profiles) that name competitors but not you. Check: Each gap has a short note on why competitors get cited.
5. **Approve a small plan.** Pick a few actions that cover the most gaps. Prefer fixing wrong facts and improving pages people already use. Google says no special optimisation is needed for its AI features beyond normal search best practice. Check: You have at most five approved actions, each tied to named gap questions.
6. **Re-measure after a month.** Run the same questions the same way after the changes are live. Compare rates, and expect some movement from normal drift. Check: You have before and after rates for the same questions.

## Known failures

- Someone checks one answer, sees no brand mention and declares a gap. Fix: Run each question many times and use the mention rate. SparkToro suggests 60-100 runs per prompt for tracking, and one HN poster's single-check claim could not be reproduced by commenters.

- Answers change week to week, so a gain or a loss may be drift. Fix: Re-measure with the same method and compare against competitors' rates in the same runs, not against last month alone.
- Personalisation, location and account history change the answers. Fix: Use fresh, logged-out sessions or APIs, and record the setup with the results.
- The assistant confuses your brand with another entity or repeats outdated facts. Fix: Record the exact wrong text. Make sure your site and your third-party profiles state the facts plainly and link to each other. One agency found ChatGPT and Google's AI Overview resolved the same brand in different ways.

- The plan turns into many thin pages written to chase AI answers. Fix: Publish fewer, useful pages. Google's spam policies name AI-generated pages at scale without value as scaled content abuse.
- Cited links in answers are broken or point to copies of the real source. Fix: Open every cited URL before you draw conclusions. The Tow Center found AI search tools often cited wrong or broken links.

## Starting prompt

```text
Help me find questions where AI assistants mention my competitors but not my brand.

My brand: [brand], website [domain], which sells [offer] to [buyer].
Competitors: [3-6 names and domains].
Buyer questions: [paste 15-40 real questions from sales calls, support tickets, search console queries or forums. If I have none, draft 30 and STOP so I can edit them.]
Assistants to check: [ChatGPT with search, Perplexity, Gemini, Claude with web search, Google AI Overviews].

Do this:
1. Run each question [5] or more times on each assistant, in fresh chats, logged out or in a clean profile where possible. Record the date, assistant, run number, whether my brand is named, which competitors are named, and every cited URL.
2. Build a table per question: my mention rate (runs where I appear / total runs), each competitor's mention rate, and the domains cited most.
3. Mark a gap where a competitor appears in at least [40%] of runs and I appear in fewer than [10%].
4. For each gap, open the top cited pages and say in two sentences what they cover that my site does not. Check my site for an existing page on the topic.
5. Propose at most [5] actions, ranked by how many gap questions each one covers. An action can be a new page, an update to an existing page, a fix to a wrong fact about us, or a listing on a third-party site the assistants cite.

Rules:
- Report rates, not single answers. Do not call a question a gap from one run.
- Note any answer that states something wrong about my brand, with the exact text.
- Never suggest hidden text, prompt injection, fake reviews or mass-produced pages.
- STOP after the table and the plan. Do not write or publish content until I approve.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"find-questions-ai-answers-without-citing-you","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
