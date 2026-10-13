---
name: match-receipts-to-bank-transactions-for-your-accountant
description: "Match receipts to bank transactions and flag VAT or sales tax questions for your accountant. You get a workbook with every bank line matched to a receipt or marked missing, a proposed category for each, and a short list of VAT or sales tax questions for your accountant."
---

# Match receipts to bank transactions and flag VAT or sales tax questions for your accountant

Source: https://agentshandbook.com/p/match-receipts-to-bank-transactions-for-your-accountant (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/match-receipts-to-bank-transactions-for-your-accountant.md

Give an agent a read-only bank export, your receipts and your chart of accounts. Have it match each bank line to a receipt in code, propose a category from your existing accounts only, and list missing receipts and tax questions. It must not invent transactions or post to your ledger. You review the workbook, and your accountant checks the result before anything is filed. Public accounts report useful cleanup, plus duplicated and invented transactions.

## Stop and ask the user

- Approve every proposed category and every match before anything is entered into the ledger.
- Decide every VAT, GST or sales tax question with your accountant. The agent only flags them.
- Approve any write to the accounting system one batch at a time, after a bank reconciliation.

## Steps

1. **Export the inputs.** Export one month of bank lines, the chart of accounts, and last month's categorised lines. Collect the month's receipts in one folder or label. Check: You have four inputs and the statement closing balance.
2. **Check the bank totals first.** Run step 1 of the prompt. If opening balance plus movements does not equal the statement closing balance, fix the export before you go on. A wrong starting balance makes every later month worse. Check: The agent prints a totals check that agrees with your statement.
3. **Extract and match receipts.** Let the agent read receipts and match them in code. Expect some unreadable images and some foreign currency lines that need you. Check: The workbook has a Matched tab and two exception tabs, and their row counts add up to the bank row count plus unmatched receipts.
4. **Review possible duplicates.** Open the Possible duplicates tab. Agents both create duplicates and miss them, so check each pair yourself. Check: Each pair is marked keep both or remove one, with a reason.
5. **Review categories.** Accept or change each proposed category. Watch hosting, software and cost of sales lines, which one benchmark saw a model mix up. Check: Every line has a category from your chart of accounts.
6. **Chase missing receipts.** Find or request receipts for bank lines without one. Write the requests yourself or approve each draft. Check: The Bank lines without receipt tab is empty or each line has a note.
7. **Send the questions to your accountant.** Send the Questions for accountant tab with the workbook. Do not let the agent decide tax treatment. Check: Your accountant has answered each question.
8. **Post and reconcile.** Enter the approved lines in your accounting system, by hand or with a dry-run script you approve. Then run the bank reconciliation in the accounting software and lock the period. Check: The bank reconciliation in your software shows no difference.

## Known failures

- The agent invents a transaction or pulls in an unrelated one so the numbers add up. Fix: Tell it never to make totals agree, only to report the gap, and check totals in code against the bank statement. A public benchmark of long bookkeeping runs reported this behaviour.
- The agent adds duplicated transactions while it cleans up the books. Fix: Reconcile against the bank every month and lock the period after review. One owner caught duplicates this way.
- Errors compound across months after a wrong starting balance. Fix: Check the opening and closing balance before any matching, and start each month from reconciled figures.
- A cost is put in the wrong account, such as hosting booked as a software subscription instead of cost of sales, or the model makes up a new account name. Fix: Give it your chart of accounts and last month's choices as precedent, forbid new names, and review categories by hand.
- The agent misreads totals or VAT from receipt images and PDFs, or stops after a few. Fix: Ask it to print a row per receipt with the extracted totals and mark unclear images as UNREADABLE. Batch large folders and restart in a fresh session when it starts to drift.
- A chat assistant gives wrong step-by-step instructions for your accounting software. Fix: Check menu paths against the vendor's help pages, or use the software's API or MCP server instead of guided clicking.
- The setup takes longer than doing it by hand for a small month. Fix: One user reports four hours with an agent for a job he could have done in one. Start with a month that has many lines, and reuse the prompt.

## Starting prompt

```text
Help me prepare [month and year] for [company name], a [country] business that is [VAT registered / not VAT registered / collects sales tax in states X, Y].

Inputs (read only, do not change these files)
- Bank export: [path to CSV for account ending 1234], statement closing balance [amount].
- Receipts and invoices: [folder path / Gmail label "Receipts"].
- Chart of accounts: [path or paste]. Use only these account names.
- Last month's categorised lines for reference: [path].

1. Load the bank CSV with code. Print the row count, the first and last date, and the sum of money in and money out. Check that opening balance plus movements equals the closing balance [amount]. If it does not, stop and show me the gap.
2. Read every receipt. Extract date, supplier, total, currency, tax amount and tax rate. If a receipt is an image you cannot read clearly, mark it "UNREADABLE". Do not guess numbers.
3. Match receipts to bank lines in code: same amount (allow [0.01] or a currency conversion within [2%]), date within [5] days, supplier name similar. Report one row per bank line: matched receipt, match confidence, and why.
4. Propose a category for each bank line from the chart of accounts only, using last month's choices as precedent. If you are not sure, leave it blank and say why. Never create a new account name.
5. Flag for my accountant, do not decide: receipts with no tax number or an unusual tax rate, foreign suppliers that charged no VAT or GST (possible reverse charge), mixed business and personal spend, entertainment, assets that may need capitalising, and [state sales tax or marketplace questions].
6. Write a workbook [path].xlsx with tabs: Matched, Bank lines without receipt, Receipts without bank line, Possible duplicates, Questions for accountant, Totals check.

Hard rules
- Do all arithmetic and totals in code, and show the code output.
- Never invent, move or borrow a transaction to make totals agree. If totals do not agree, report the difference.
- Do not write to [Xero / QuickBooks / the ledger file], do not delete files, and do not email anyone. Stop and ask me first.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"match-receipts-to-bank-transactions-for-your-accountant","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.