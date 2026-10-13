---
name: build-a-spending-dashboard-from-bank-csv-exports
description: "Build a private spending dashboard from your bank and card CSV exports. You get a local dashboard of spending by month and category that you can rebuild each month, with totals that match your statements."
---

# Build a private spending dashboard from your bank and card CSV exports

Source: https://agentshandbook.com/p/build-a-spending-dashboard-from-bank-csv-exports (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/build-a-spending-dashboard-from-bank-csv-exports.md

Download CSV exports from each bank and card account, put them in one local folder, and ask a coding agent to write a script that loads, cleans and categorises them and builds a dashboard file. Keep the categories in a rules file that you edit, and make every total come from code. Check the totals against your statements before you trust any chart. Public accounts report that the agent is good at matching and charting, but labels many lines wrongly until you give it your own payee rules.

## Stop and ask the user

- Approve the category rules file before the agent applies it to all transactions.
- Check that the dashboard totals match each statement before you rely on them.

## Steps

1. **Export the same months from every account.** Download CSV files for the same date range from every checking, savings and card account. Put them in one new folder. Note the total money in and out for each account and month from your statements. Check: One folder holds one CSV per account, and you have a short list of statement totals.
2. **Load the files with code and check the totals.** Paste the prompt. The agent writes a script and prints row counts, date ranges and sums for each file. Compare them with your statements. Different banks use different columns and sign rules (some show spending as negative numbers, some in a separate column), so this is where errors show up. Check: The printed sums for each file match your statements.
3. **Remove transfers and card payments.** A card payment from your checking account and the card purchases it pays for are the same money. Approve the list of lines that the agent marks as not spending. Check: The list holds only moves between your own accounts and refunds, and no real purchases.
4. **Write your own category rules.** Edit the rules file that the agent proposes. A payee to category map that you own works better than letting the model guess each line. One tester reports that without rules, the model put most lines under "other" and labelled bank fees as fuel. Check: The 30 biggest payees each have a category you agree with.
5. **Build the dashboard and read the uncategorised list.** The agent applies the rules and builds a local HTML file. Read the "Uncategorised" list and add rules for anything big. Ask the agent to rerun. Check: The dashboard opens in your browser, the check totals at the top match your statements, and uncategorised spending is small.
6. **Rerun it each month.** Drop next month's CSVs into the folder and run the script, or ask the agent to run it. Add rules for new payees. Check: The new month appears in the charts and the totals still match.

## Known failures

- The model labels most transactions as "other" or picks odd categories, such as fuel for bank fees. Fix: Give it a payee to category rules file that you edit, and make it list unmatched lines instead of guessing.
- Totals are wrong, or some rows are missing, but the answer sounds certain. Fix: Make every count and sum come from code, and compare the per-file sums with your statements before you look at charts.
- A long session drifts and the agent forgets earlier rules or repeats work. Fix: Keep the logic in a script and a rules file, not in the chat. Start a fresh session and point it at the files.

## Starting prompt

```text
Build me a private spending dashboard. Work only in this folder: [path]. Do not upload my data anywhere, and do not install anything without asking.

Inputs (read only, never edit these files):
- CSV exports: [bank-checking.csv, card-1.csv, card-2.csv], covering [months].
- Statement totals to check against: [account: total out, total in, for each month].

1. Write a script (Python or similar) that loads every CSV. Print, for each file, the column names, the row count, the first and last date, and the sums of money in and money out. Every number must come from the code, not from you.
2. STOP. Show me those numbers next to my statement totals and wait for me.
3. Mark lines that are not spending: transfers between my own accounts, credit card payments, refunds. List them and wait for my OK, so nothing is counted twice.
4. Propose a rules file, categories.csv, that maps payee text to a category from this list: [Housing, Groceries, Eating out, Transport, Subscriptions, Health, Shopping, Travel, Other]. Show me the 30 biggest payees and the rule for each. Wait for me to edit and approve it.
5. Apply the rules. Put anything without a rule under "Uncategorised" and list it. Do not guess.
6. Build one local HTML file with charts: spending by month, by category, top payees, and a table I can filter. Show the check totals at the top.
7. Write a short README that explains how to rerun it next month with new CSVs.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"build-a-spending-dashboard-from-bank-csv-exports","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.