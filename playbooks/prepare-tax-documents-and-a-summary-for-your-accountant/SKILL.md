---
name: prepare-tax-documents-and-a-summary-for-your-accountant
description: "Gather your tax documents into one folder and write a checked summary for your accountant. Your accountant gets one tidy folder, a list of every form with its key figures and source, a list of missing documents, and your open questions."
---

# Gather your tax documents into one folder and write a checked summary for your accountant

Source: https://agentshandbook.com/p/prepare-tax-documents-and-a-summary-for-your-accountant (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/prepare-tax-documents-and-a-summary-for-your-accountant.md

Put every tax form you have in one isolated folder, with last year's return. Ask a coding agent to list each document, pull the key figures with the file and box they came from, compare against last year to find missing forms, and write a short summary and question list for your accountant. Do not let it file, and check every figure against the form. People who did this report real time savings and a found deduction, plus misread boxes, wrong tax rules and a self-check that used stale numbers.

## Stop and ask the user

- Choose which files go into the agent's folder. Leave out anything it does not need.
- Check every extracted figure against the original form before the summary goes to your accountant.
- Send the folder to your accountant yourself. The agent never files, pays or submits anything.

## Steps

1. **Make an isolated folder.** Copy this year's forms and last year's return into a new folder with nothing else in it, outside any project folder the agent has used before. Remove old notes or summary files that hold earlier numbers. Check: The folder holds only this year's documents and last year's return.
2. **Build the inventory with sources.** Paste the prompt. The agent lists each document with its key figures and the box each figure came from. Several writers split big jobs into smaller runs because long sessions ran out of context. Check: Every row in inventory.csv names a file and a box or line, and unclear values say UNREADABLE.
3. **Check figures against the forms.** Open each form and compare the main figures with the inventory. Writers report misread 1099 boxes and a K-1 abbreviation read as a charity gift, so look hardest at 1099s and K-1s. Check: You have ticked every figure, and corrected the ones that were wrong.
4. **Find missing documents.** Read missing.md. For each item from last year that has no form this year, either find the form or write a note for your accountant (for example, account closed). Check: Every missing item has a form or a note.
5. **Write the summary and questions.** The agent writes a one or two page summary for your accountant with your life changes, income by form type, deduction records and your questions. Ask it to recheck every number against the original files, not its own notes. Check: The summary fits on two pages and every number points to a file.
6. **Hand over the folder yourself.** Send the folder through your accountant's portal. If you file yourself instead, use proper tax software and still check every figure. Writers who prepared returns with an agent all had to enter or file the return by hand. Check: Your accountant confirms they have the folder and the question list.

## Known failures

- The agent misreads a form, such as a 1099 box or a K-1 footnote, and the number looks right. Fix: Make it cite the box for every figure, and check 1099s and K-1s yourself against the original.
- The agent says it checked its work, but it compared against an old note that held earlier numbers. Fix: Remove old notes and summaries from the folder, and ask for a recheck against the original files only.
- The agent applies a tax rule wrongly, for example passive losses or a retirement contribution limit. Fix: Keep the agent to organising. Leave tax treatment to your accountant, and send rule questions as questions, not answers.
- Long sessions run out of context and the agent loses track. Fix: Work in steps, save each step to a file (inventory, missing list, answers), and start a fresh session that reads those files.
- The agent can read files outside the tax folder. Fix: Use a folder outside your other projects, turn off memory if your agent has it, and give it only what it needs.

## Starting prompt

```text
Help me prepare my [tax year] tax documents for my accountant. You are an organiser, not a tax preparer. Do not calculate my tax, do not give tax advice, and do not file anything.

Work only inside this folder: [path]. Do not read, search or write outside it. Treat the files as read only: copy, never move or rename the originals.
Contents: my tax forms for [tax year] (W-2, 1099s, 1098, brokerage statements, receipts) and last year's return ([file name]).
Me: [filing status], [states lived or worked in], [new this year: job change, home purchase, side income, baby, move].

1. Make inventory.csv: one row per document, with file name, form type, issuer, and the key figures. For each figure, give the form box or line and the page. If you cannot read a value, write UNREADABLE. Never guess or fill a value from memory.
2. Compare with last year's return. List every income source, account or deduction that appeared last year but has no document this year. Put them in missing.md.
3. STOP and show me the inventory and the missing list. Wait while I check the figures and add files.
4. Write summary.md for my accountant: life changes, income sources with totals by form type, deduction records I have, and a numbered list of questions. Mark every number with the file it came from.
5. Before you finish, recheck each figure in summary.md against the original file, not against your earlier notes. List any mismatch.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"prepare-tax-documents-and-a-summary-for-your-accountant","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.