---
name: build-a-weekly-kpi-report-for-approval
description: "Build a weekly KPI report from your spreadsheets and send the draft for approval. Every Monday you get a draft report with this week's KPIs, the change from last week, a data check section and three lines of commentary, ready for one person to approve and send."
---

# Build a weekly KPI report from your spreadsheets and send the draft for approval

Source: https://agentshandbook.com/p/build-a-weekly-kpi-report-for-approval (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/build-a-weekly-kpi-report-for-approval.md

Have an agent write a small script that pulls last week's numbers from your spreadsheets or exports, computes each KPI from a written definition, and checks row counts and totals. The model writes the short commentary only after the numbers exist. The draft goes to one approver, and a person sends it to the team. Public tests show chat assistants inventing counts and dropping rows when they do the maths themselves.

## Stop and ask the user

- Approve the written KPI definitions and the week boundary before the first run.
- Check the data section and approve the draft before it is sent to anyone.
- Approve any change the agent proposes to a source spreadsheet. The default prompt makes none.

## Steps

1. **Write the KPI definitions.** Agree each KPI in one line with the column, filter and week boundary. Pick the time zone on purpose. Check: Two people read the definitions and compute the same number for last week.
2. **Build the script and checks.** Paste the prompt. The agent writes code that loads sources, computes KPIs and prints data checks. Check: The script prints rows loaded, rows dropped with reasons, and the KPI table.
3. **Test against a week you already know.** Run it on a past week where you have trusted numbers. Fix definitions until they match. Check: Every KPI matches your trusted numbers, or you know why it differs.
4. **Review the commentary.** Read the three sentences. Remove any cause the data does not show. Check: Every claim in the commentary points to a number in the table.
5. **Schedule the run and the draft.** Run it weekly and save the result as a draft to the approver. Do not wire it to send. Check: On Monday a draft is waiting with the right week dates in the title.
6. **Approve and send.** The approver reads the data checks first, then the numbers, then sends. Check: The sent report has no DO NOT SEND flag and matches the draft.

## Known failures

- The assistant states counts that are not in the data, or shows code it never ran. Fix: Make every number come from code output, and tell the agent to remove any number it cannot trace to that output.
- Rows drop out silently, for example blanks removed by the analysis library, or a tool reads only part of the file. Fix: Print rows loaded and rows dropped with reasons in every run, and stop when the drop rate is above your limit.
- The report computes a different metric from the one you meant, and an AI review pass approves it. Fix: Write definitions down and test against a week you already know. Do not rely on the model to review its own logic.
- Week boundaries shift because the time zone defaults to UTC or month length is hard-coded. Fix: Set the time zone and week start in the definitions and in the scheduler, and print the date range in the data checks.
- A recent trend looks like progress but comes from records that are not complete yet, such as orders still in transit. Fix: Ask the agent to report how many records in each week are still open, and treat the latest week with care.
- Numbers stored as text in a spreadsheet break the sums. Fix: Have the script convert and count values it could not convert, and show that count in the data checks.
- Different models catch different problems in the same workbook. Fix: Keep the deterministic checks as the main safety net, and use the strongest model you have for the review pass.

## Starting prompt

```text
Build a weekly KPI report for [team or company].

Sources (read only)
- [Google Sheet "Sales log", tab "Deals"], [Stripe export CSV at path], [GA4 export at path].

KPI definitions (use exactly these; ask me if one is unclear)
- [New MRR] = sum of [amount] where [status = won] and [close date] in the week.
- [Active customers] = count of distinct [customer id] with [status = active] at the end of the week.
- [Add up to 8 more.]
- Week = Monday 00:00 to Sunday 23:59 in [time zone]. Report the most recent complete week and the week before.

1. Write a script ([Python / Apps Script]) that loads each source, applies the definitions and outputs a table: KPI, this week, last week, change, change %.
2. Data checks in the same script: rows loaded per source, rows in the week, rows dropped and why (blank, bad date, duplicate id), and the date range found. If any source has zero rows for the week, or more than [5%] of rows were dropped, mark the report "DO NOT SEND" at the top.
3. Run the script and show me its raw output. Do not type any number yourself. Every number in the report must come from the script output.
4. Write the report: the KPI table, a "Data checks" section, and three short sentences on the biggest changes. Say "not explained by the data" if you do not know why a number moved. Do not guess causes.
5. Save the draft as [Google Doc / email draft to approver@company.com / Slack draft]. Stop.

Hard rules
- Do not send the report to anyone. A person approves and sends it.
- Do not edit, sort or delete anything in the source files.
- If a definition does not fit the data (a column is missing or renamed), stop and ask me.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"build-a-weekly-kpi-report-for-approval","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.