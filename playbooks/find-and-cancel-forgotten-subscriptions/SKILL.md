---
name: find-and-cancel-forgotten-subscriptions
description: "Find forgotten subscriptions in your email and statements, then cancel the ones you choose. You get a list of every recurring charge with its price and renewal date, and you cancel the ones you choose with a confirmation for each."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/find-and-cancel-forgotten-subscriptions
  version: "2026-10-13"
---

# Find forgotten subscriptions in your email and statements, then cancel the ones you choose

Source: https://agentshandbook.com/p/find-and-cancel-forgotten-subscriptions (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/find-and-cancel-forgotten-subscriptions.md

First build the list: let an agent search your email for renewal notices and read your bank and card exports for repeat charges, then check app store subscriptions yourself. Pick what to cancel. Then let a browser agent walk each cancellation page while you sign in and confirm. Testers report working cancellations for streaming services, and also logins they had to do themselves, cryptic charge names, and Amazon blocking agents.

## Stop and ask the user

- Approve the list of subscriptions to cancel before the agent opens any account.
- Sign in yourself and confirm each cancellation on the provider's page.

## Steps

1. **Collect the sources.** Export 12 to 13 months of transactions from every card and bank account, so yearly renewals show up. Note any card you rarely use. Check: You have one export per account covering at least a year.
2. **Build the subscription list.** Paste Part 1 of the prompt. The agent searches your email for renewal notices and reads the exports for repeat charges. It returns one table and a list of charge names it cannot match. Check: You see a table with one row per service, and a short list of unknown charge names.
3. **Check app stores and unknown charges yourself.** Open the subscriptions page on your iPhone or Android. Apple says to check your bank statement and contact the billing company for subscriptions that are not from Apple. Google says uninstalling an app does not cancel its subscription. Search each unknown charge name. Check: Every row is matched to a service, and every app store subscription is on the list.
4. **Mark keep, cancel or check.** Decide each row yourself. For streaming, one writer asked the assistant which services to pause and rotate based on her viewing. Check: Every row has a decision.
5. **Cancel one service at a time.** Paste Part 2. The agent opens each billing page and walks to the cancel step. You sign in, decline offers, and press the final confirm yourself. Check: Each service shows a cancellation confirmation and an end date.
6. **Keep the proof.** Save each confirmation email or screenshot in one folder. Check next month's statement for any charge that came back. Check: Next month's statement shows none of the cancelled charges.

## Known failures

- The agent cannot get into Amazon, Google One or another big site, or gets flagged as a bot. Fix: Cancel those by hand. Ask the agent for the direct link and steps instead.
- The agent cannot sign in or finish the cancellation on its own. Fix: Expect to sign in and confirm yourself. Writers report that the agent mostly navigated and you still had to log in and confirm.
- Charge names on the statement are cryptic, so the agent cannot tell what they are. Fix: Have the agent list unknown names instead of guessing, then search them yourself or check the card's merchant details.
- Subscriptions billed through Apple, Google Play or PayPal are missed or hidden under one name. Fix: Check the subscription settings on each phone and your PayPal automatic payments page yourself.
- Giving an agent your email or bank data feels risky. Fix: Use exported statements in a local folder for the finding step, and keep email access to a read-only search session you watch.

## Starting prompt

```text
Help me find and cancel subscriptions I no longer use.

Part 1: build the list. Do not cancel anything yet.
1. Search my email ([Gmail / Outlook]) for the last [13] months for: receipt, renewal, subscription, auto-renew, your plan, trial ending, membership. Also search for receipts from Apple, Google Play, PayPal and Amazon.
2. Read these card and bank exports: [file names]. Find charges that repeat monthly, yearly or every few months with a similar amount.
3. Make one table: service, amount, how often, next renewal date, card or account billed, where you found it (email subject and date, or statement line). Merge duplicates. List charge names you cannot match to a service, exactly as they appear on the statement.
4. STOP. Show me the table and wait. I will mark each row keep, cancel or check.

Part 2: cancel only what I mark.
5. For each service I mark cancel, open its account or billing page. Let me sign in myself. Click through to the cancel step, decline retention offers, and stop at the final confirm button so I can press it.
6. After each one, save the confirmation (screenshot or email) and the date access ends.
If a site blocks you or shows a CAPTCHA, stop and tell me. Never type passwords, card numbers or codes.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"find-and-cancel-forgotten-subscriptions","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
