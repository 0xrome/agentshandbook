---
name: run-a-deep-research-report-and-verify-its-citations
description: "Run a deep research report and check that every citation supports its claim. You get a report where every factual claim links to a source that loads and says what the report claims, plus a table of the claims you cut or changed. "
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/run-a-deep-research-report-and-verify-its-citations
  version: "2026-10-13"
---

# Run a deep research report and check that every citation supports its claim

Source: https://agentshandbook.com/p/run-a-deep-research-report-and-verify-its-citations (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/run-a-deep-research-report-and-verify-its-citations.md

Scope the question tightly, then run a deep research mode such as Claude Research, ChatGPT deep research, Gemini Deep Research or Perplexity. Ask for a claim-by-claim source list with the passage that supports each claim. Then run a separate check in a fresh session that opens every link and marks each claim as supported, partly supported or not supported. Studies and news reports show AI research tools cite broken links, real pages that do not say what is claimed, and papers that do not exist, so nothing goes out until a person has read the key sources.

## Stop and ask the user

- Approve the research plan and scope before the long run starts.
- Read the sources behind every key claim yourself before you share or publish the report.

## Steps

1. **Write one precise question.** Name the decision, the time range and the kinds of sources that count. Vague questions get broad, shallow reports. Check: The question fits in two sentences and names the source types you trust.
2. **Approve the research plan.** Ask the agent to show its plan before the long run. Remove off-topic branches and add sources you know matter. Check: The plan covers your sub-questions and names real places to search.
3. **Run the research with a source table.** Use the prompt so the report ends with claim, URL, date and the supporting sentence for each claim. Check: Every claim in the report has a row in the source table.
4. **Check every link in a fresh session.** Paste the report into a new chat or a coding agent and run the check prompt. A fresh session has not seen the drafting and is less likely to defend it. Check: You have a table with load status and supported, partly or not for every row.
5. **Read the key sources yourself.** Read every source behind a claim you will act on or publish, and a sample of the rest. Check the date and that the page is the original, not a copy. Check: You read the passage behind each key claim and it says what the report says.
6. **Fix or cut unsupported claims.** Remove claims with dead or fabricated sources, soften partly supported ones, and record each change. Check: No claim in the final report rests on a source marked not supported or dead.
7. **Share it yourself.** Add a short note on method and limits, such as paywalled sources you could not read. Then send or publish it yourself. Check: The report states its limits and you are the one who sends it.

## Known failures

- A citation is a real page that does not support the claim, or a page that does not exist. Fix: Ask for the supporting sentence for each claim and check each one in a fresh session. Read the key sources yourself.
- Links return errors or point to a home page instead of the article. Fix: Check that each link loads and points to a specific page. Rao, Wong and Callison-Burch report that giving models a link-checking tool cut broken citation links sharply.

- The report cites a syndicated or scraped copy instead of the original source. Fix: Ask for original publishers and check the domain of each citation.
- The tool cannot read paywalled papers and books, so the report leans on whatever is free. Fix: Say in the prompt which paywalled sources matter, read them yourself, and note the gap in the report.
- The report states things with confidence that no source supports. Fix: Require labels for inference and a rule that missing numbers stay missing. Cut any number you cannot trace to a source.

## Starting prompt

```text
Research question: [one precise question, for example "What does published evidence say about X for Y between 2022 and 2026?"]
Audience and use: [who will read it and what decision it supports]
Scope: [time range, regions, types of sources]. Prefer primary sources: [official docs, peer-reviewed papers, filings, datasets]. Avoid [SEO listicles, vendor marketing, AI-generated summaries] unless you label them.

Write the report with these rules:
1. Every factual claim gets an inline citation to a specific page, not a home page.
2. After the report, add a source table: claim, source title, URL, publication date, and the exact sentence from the source that supports the claim (under 30 words).
3. If you could not open a source, or it is paywalled, say so. Do not cite what you did not read.
4. Separate what sources say from your own inference. Label inference as inference.
5. List open questions and where the evidence conflicts.
6. Do not invent statistics. If you have no number, say there is no number.

First, show me your research plan and the sources you intend to search. Wait for my approval before you run the full research.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"run-a-deep-research-report-and-verify-its-citations","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
