---
name: do-a-literature-review-of-papers-on-a-topic
description: "Do a literature review with an agent that finds, screens and summarises real papers. You get a screening log, an evidence table with one row per included paper, a synthesis that cites only papers you hold, and a reference list where every entry resolves to a real record. "
---

# Do a literature review with an agent that finds, screens and summarises real papers

Source: https://agentshandbook.com/p/do-a-literature-review-of-papers-on-a-topic (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/do-a-literature-review-of-papers-on-a-topic.md

Ground the agent in real paper records before it writes anything: a Zotero library, a folder of PDFs, or a scholarly search tool such as a paper search MCP. Have it screen papers against inclusion criteria you wrote, with a reason for each decision, and extract findings into a table that names the page or section. Then check that every reference resolves to a real DOI or arXiv ID. Studies of chatbot-written reviews found many fabricated or wrong references, so the reference check is not optional.

## Stop and ask the user

- Write and approve the research question and inclusion criteria before the agent screens anything.
- Check a sample of include and exclude decisions against the papers.
- Confirm every reference resolves and read the papers behind your main claims before you submit or publish.

## Steps

1. **Write the question and criteria.** Write the research question and include and exclude rules in a file such as criteria.md. The agent screens against this, so make each rule checkable. Check: Someone else could screen a paper with your criteria and reach the same decision.
2. **Ground the agent in real records.** Connect Zotero, put PDFs in a folder, or use a paper search tool. Do not ask a chat model to list papers from memory. Check: Every candidate has a DOI, arXiv ID or a PDF you hold.
3. **Run and log the searches.** Approve the search terms. Have the agent log each query, source and hit count so you can report your method. Check: You have a search log with dates and counts.
4. **Screen in batches with reasons.** Review the first batch closely. Correct the agent's reading of your criteria, then let it continue. Spot-check excludes as well as includes. Check: You agree with at least the sample of decisions you checked, and each decision names a criterion.
5. **Extract findings with page references.** Have the agent fill the evidence table from the full text, with the page or section for each finding. Check: Opening a random row's paper at the given page shows the stated finding.
6. **Synthesise from the table only.** Ask for a synthesis by theme that cites only rows in the evidence table and marks conflicts and gaps. Check: Every citation in the synthesis maps to a row in the table.
7. **Verify every reference.** Resolve each DOI or arXiv ID and compare title, authors, venue and year. Fix wrong details and remove anything that does not resolve. Check: All references resolve and match. None were added from memory.
8. **Read the papers behind your main claims.** Read the key papers yourself before you submit, publish or send the review. Check: You can defend each main claim from the paper itself.

## Known failures

- The agent cites papers that do not exist or mixes real titles with wrong authors. Fix: Ground it in records you hold and check every DOI or arXiv ID against a metadata API.
- A real paper is cited for a finding it does not report. Fix: Require the page or section for each finding and spot-check rows against the PDF.
- Asked to summarise a citation it cannot find, the model writes a plausible study anyway. Fix: Tell it to answer "not found" and only summarise papers you have given it.
- Paywalled papers are skipped, so the review leans on open access work. Fix: Download paywalled papers through your library and add them to the folder or Zotero.
- Fields such as sample size or effect size get filled in when the paper does not report them. Fix: Tell the agent to leave unreported fields blank, and check a sample of rows.
- The paper search API rate-limits the agent. Fix: Slow the requests down. arXiv's terms ask for one request every three seconds on one connection.

## Starting prompt

```text
You are helping me with a literature review. Work only from papers you can actually open. Never cite a paper from memory.

Question: [research question]
Inclusion criteria: [population or system, methods, years 2019-2026, peer-reviewed or preprint, language]
Exclusion criteria: [e.g. opinion pieces, studies without evaluation]
Sources: [my Zotero collection "X" / the PDFs in ./papers / search with the paper search tool in arXiv, Semantic Scholar and OpenAlex]

Step 1, search: run [3-5] searches with the terms I approve: [terms]. Log each query, the source and the number of results.
Step 2, screen: for each candidate, decide include, exclude or unsure from the title and abstract, and give a one-line reason tied to a criterion. Work in batches of [20] and show me the first batch before you continue.
Step 3, extract: for each included paper, fill a table with: citation, DOI or arXiv ID, design, sample or dataset, main finding, limitation, and the section or page where you found the finding.
Step 4, synthesise: write [800] words grouped by theme. Cite only papers in the table. Mark where findings conflict and where evidence is thin.
Step 5, verify: for every reference, check that the DOI or arXiv ID resolves and the title and authors match. List any that do not.

Do not invent page numbers, sample sizes or results. If a detail is not in the paper text you read, leave it blank. Do not submit, email or upload anything.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"do-a-literature-review-of-papers-on-a-topic","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.