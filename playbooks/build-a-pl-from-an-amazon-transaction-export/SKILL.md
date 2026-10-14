---
name: build-a-pl-from-an-amazon-transaction-export
description: "Build a profit-and-loss statement from a raw Amazon transaction export. You get a structured P&L with each transaction classified, totals calculated with formulas, and a clear view of gross margin."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/build-a-pl-from-an-amazon-transaction-export
  version: "2026-10-13"
---

# Build a profit-and-loss statement from a raw Amazon transaction export

Source: https://agentshandbook.com/p/build-a-pl-from-an-amazon-transaction-export (trust: reported, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/build-a-pl-from-an-amazon-transaction-export.md

Upload a raw Amazon seller transaction export to a spreadsheet agent such as Shortcut.ai and ask it to classify each line item and produce a structured profit-and-loss statement. One user reports the task completed on the first try, with the agent classifying every transaction and producing formula-based totals. Review every category assignment before you use the result for any financial or tax decision.

## Stop and ask the user

- Review the agent's transaction category mapping before accepting the final P&L.

## Steps

1. **Export your transaction report from Seller Central.** In Amazon Seller Central, go to Reports, then Payments, then Transaction View. Choose your date range and download as a spreadsheet file. Check: You have a file with individual transaction rows, each with a type, description, and amount.
2. **Upload the file and request a transaction type inventory.** Attach the file to the agent and ask it to list every distinct transaction type before doing anything else. This step surfaces unusual types that need a custom category before any classification runs. Check: The agent returns a list of transaction types and no P&L has been built yet.
3. **Confirm the category mapping.** Check that each type maps to a sensible P&L line. Correct any that are wrong, for example a storage surcharge mapped to Revenue instead of Amazon Fees. Check: You have approved a mapping with no obvious errors.
4. **Generate the P&L.** Tell the agent to build the full P&L using the approved mapping. Require formulas and ask it to flag any row it cannot classify with confidence. Check: Total cells contain formulas, not hardcoded numbers. The row count matches the source file.
5. **Handle flagged rows and spot-check the result.** Assign any flagged rows yourself. Cross-check two or three line items against the original file before you use the P&L for any decision. Check: No flagged rows remain unassigned and spot checks match the source data.

## Known failures

- The agent misclassifies unusual Amazon fee types such as storage surcharges, reimbursements, or co-op charges. Fix: Ask the agent to list every distinct transaction type before building the P&L, then confirm or correct each mapping before it proceeds.
- Totals appear as hardcoded numbers rather than formulas, making the file hard to audit or update. Fix: Include "use formulas, not hardcoded numbers" in your prompt and spot-check a sample of total cells after the agent finishes.
- Free daily credits run out before a large export is fully processed. Fix: Split the export into smaller date ranges and process each in a separate session, or upgrade to a paid plan.

## Starting prompt

```text
I have a raw Amazon seller transaction export. Each row is a single transaction with a type, description, and amount.

Step 1. Read the file and list every distinct transaction type you find. Do not build the P&L yet.
STOP and wait for my approval of the category mapping.

Step 2. Map each transaction type to one of these P&L categories: [Revenue, Refunds, Amazon Fees, Advertising, Shipping, Other Costs]. Show me the full mapping.
STOP and wait for my confirmation before continuing.

Step 3. Build the full P&L summary using the approved mapping. Use formulas for all totals, no hardcoded numbers. Flag any row you are unsure how to classify.

Step 4. Report: total rows processed, totals by category, and a list of any flagged rows with the reason for each flag.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"build-a-pl-from-an-amazon-transaction-export","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
