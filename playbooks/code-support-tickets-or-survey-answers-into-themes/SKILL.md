---
name: code-support-tickets-or-survey-answers-into-themes
description: "Sort support tickets or survey answers into themes with counts you can check. You get a spreadsheet with every ticket or answer labelled, a theme table with counts and example quotes, and an agreement check that shows how far to trust it."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/code-support-tickets-or-survey-answers-into-themes
  version: "2026-10-13"
---

# Sort support tickets or survey answers into themes with counts you can check

Source: https://agentshandbook.com/p/code-support-tickets-or-survey-answers-into-themes (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/code-support-tickets-or-survey-answers-into-themes.md

Do it in two passes. First, the agent drafts a codebook of themes from a sample, and you edit it. Then it labels every row against that codebook, one label per row, and counts the labels in code. You check a random sample against your own labels before you trust the counts. Studies and practitioners report that one-shot theme summaries miscount, shift between runs, and silently skip data.

## Stop and ask the user

- Edit and approve the codebook before the agent labels the full set.
- Label a random sample yourself and compare before you share any counts.

## Steps

1. **Export and clean the text.** Export the tickets or answers with ids. Remove signatures, quoted email threads and personal details. Check: The file has one row per item and no customer names or emails.
2. **Draft the codebook from a sample.** Run pass 1. The agent proposes themes with definitions and examples. Check: You get 8 to 15 themes, each with include and exclude rules.
3. **Edit the codebook.** Merge overlapping themes, split vague ones, and rename themes in your team's words. Clear definitions matter. One public project reports that adding category descriptions cut run-to-run variance a lot. Check: You could give the codebook to a colleague and they would label the same way.
4. **Label every row.** Run pass 2. The agent labels in batches and checks that every id has a label. Check: The coverage check shows zero missing ids.
5. **Check agreement on a sample.** Take 50 random rows, label them yourself without looking, and compare with the agent's labels. Note which themes it confuses. Check: You know the share of rows where you agree, and which themes are weak.
6. **Re-run on a second seed or model.** Label the same sample again in a fresh session and compare. Large swings mean the codebook is still too vague. Check: Theme shares change only a little between the two runs.
7. **Share the theme table.** Share counts with the agreement result and example quotes. Say which themes are less reliable. Check: Every number in the summary traces to labels.csv.

## Known failures

- Theme percentages add up to more than 100 percent, or counts look random. Fix: Allow one primary theme per row and count in code over a labels file. Ipsos researchers saw totals over 100 percent when their prompt did not ask for one code per case.
- The same prompt gives different themes and shares on different days or models. Fix: Fix the codebook with definitions and examples, and label against it. Compare two runs before you report.
- The agent reads only part of the data, or says information is not in the file. Fix: Label in batches with a coverage check that lists missing ids, and ask the agent to print columns before answering.
- The model creates fewer, broader themes than people would, and small issues disappear. Fix: Ask for an "Other" list with the most common misfits, and review it for small but important problems.
- Long, wordy answers get more weight than short ones. Fix: Count rows, not mentions, and check a sample of short answers in your agreement test.

## Starting prompt

```text
Analyse [file.csv], [N] rows of [support tickets / survey answers to "question text"]. The text is in column [text], the row id in [id].
Before you start, remove or mask names, emails, phone numbers and account numbers.

Pass 1: codebook (stop after this pass)
1. With code, take a random sample of [150] rows (fixed seed). Read them and draft a codebook of [8 to 15] themes. For each theme give: short name, one-sentence definition, include and exclude rules, and two example row ids.
2. Add the codes "Other" and "Unclear".
3. Show me the codebook and stop. I will edit it.

Pass 2: labelling (only after I approve the codebook)
4. Label every row in batches of [50] with code. For each row output: id, primary theme, secondary theme (optional, only if clearly present), sentiment [positive / neutral / negative], and a quote under 20 words from that row.
5. Coverage check in code: every input id has exactly one primary theme. Print input rows, labelled rows and missing ids. If any id is missing, label it before you go on.
6. Count in code: rows per primary theme, share of total (must sum to 100%), and the same split by [plan / month / channel].
7. Write labels.csv and a summary with the theme table and three example quotes per theme with their ids.

Hard rules
- Never count by reading. Every number comes from code over labels.csv.
- Do not invent themes that are not in the approved codebook. Put misfits in "Other" and list the 10 most common kinds of "Other" at the end.
- Do not upload, share or email the results. Ask me first.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"code-support-tickets-or-survey-answers-into-themes","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
