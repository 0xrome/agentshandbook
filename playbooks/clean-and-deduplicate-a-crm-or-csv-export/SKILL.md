---
name: clean-and-deduplicate-a-crm-or-csv-export
description: "Clean and deduplicate a messy CRM or CSV export without losing real records. You get a clean file, a change log that explains every merge, and a short review sheet of possible duplicates for you to decide, with every original row accounted for."
---

# Clean and deduplicate a messy CRM or CSV export without losing real records

Source: https://agentshandbook.com/p/clean-and-deduplicate-a-crm-or-csv-export (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/clean-and-deduplicate-a-crm-or-csv-export.md

Ask a coding or data agent to write a script that profiles the file, normalises emails, phones, names and dates in new columns, and removes only exact duplicates on a strong key such as email. Near matches go to a review sheet for you, with a reason for each pair. Check that rows in equal rows out plus rows merged. Public tests show chat models merging distinct people and losing records when they dedupe by judgement.

## Stop and ask the user

- Approve the match rules before the agent removes any row.
- Decide every pair in the review sheet yourself.
- Approve the final file before it is imported or used to merge records in the CRM.

## Steps

1. **Export and copy.** Export the full list with record ids and update dates. Make a copy and keep the original untouched. Check: You have the original and a working copy with the same row count.
2. **Profile the file.** Run step 1. Read the blanks, the date formats and the encoding before any cleaning. Check: The profile row count matches the row count in your CRM export screen.
3. **Agree the match rules.** Choose the strong key (usually email for contacts and domain for companies) and which row wins in a merge. Check: You can say in one sentence when two rows are the same record.
4. **Normalise and remove exact duplicates.** The agent normalises in new columns and merges only exact matches on the strong key, with a change log. Check: The change log has one line per removed row and the reconciliation numbers match.
5. **Review possible duplicates.** Open review.csv and decide each pair. Look closely at people who share a first name or a company. Check: Every pair is marked merge or keep apart.
6. **Apply your decisions and import.** Ask the agent to apply only the pairs you marked merge, then re-run the reconciliation. Import into the CRM or merge there yourself. Check: The final row count equals the profile count minus the rows you chose to merge.

## Known failures

- The model merges different people who share a name or company and deletes real records. Fix: Merge automatically only on a strong key, block merges when strong identifiers differ, and send every other match to a review sheet.
- Rows go missing without a warning, or a tool processes only part of the file. Fix: Reconcile input rows against output rows plus removed rows in code on every run.
- Dates written in day-month and month-day order break matching and create months that do not exist. Fix: Flag ambiguous dates instead of guessing, and fix them with a rule you choose, such as the source system's locale.
- The agent fills blanks with guesses or averages without telling you. Fix: Tell it never to fill a blank except from another row of the same record, and to count blanks before and after.
- Duplicates come back after import because the CRM matches on a different key. Fix: Read your CRM's dedupe rules first. HubSpot's docs say it dedupes contacts by email and companies by domain on import.
- The client's data is not allowed in a cloud assistant. Fix: Ask the agent to write the script against a small fake sample, then run the script locally on the real file.

## Starting prompt

```text
Clean and deduplicate [path to export.csv], a [HubSpot / Salesforce / other] export of [contacts / companies], about [N] rows.
Work on a copy. Never change or delete the original file.

1. Profile the file with code: row count, columns, blanks per column, encoding, delimiter, date formats found, and the 10 most common values in [country, company, owner]. Show me the profile and stop.

After I confirm:
2. Normalise in NEW columns, keep the originals: email (trim, lowercase), phone (E.164 using default country [US]), first and last name (trim, fix case), company (trim, drop "Inc", "Ltd" only in the match column), dates (ISO). If a date is ambiguous, such as 05/07, do not guess. Flag it.
3. Exact duplicates: group rows with the same normalised [email]. Within a group keep [the most recently updated row] and fill its blank fields from the others. Never overwrite a non-blank value. Record every merge in a change log: kept row id, removed row ids, fields filled.
4. Possible duplicates: find pairs with the same normalised name and the same company or phone, or very similar emails. Do not merge these. Put them in a review sheet with both rows side by side and the reason.
5. Never treat two rows as duplicates when they have different non-blank emails or different non-blank [CRM ids], even if the names match.
6. Reconcile with code: input rows = output rows + rows removed as exact duplicates. Print the numbers. If they do not match, stop.
7. Save clean.csv, changelog.csv and review.csv next to the original. Do not import anything into the CRM.

Hard rules
- All work happens in code. Do not edit rows by hand in the chat.
- Do not delete any file. Do not write to the CRM. Stop and ask me before either.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"clean-and-deduplicate-a-crm-or-csv-export","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.