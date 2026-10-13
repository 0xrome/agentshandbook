---
name: triage-support-inbox-with-approved-replies
description: "Triage your support inbox and draft replies that a person approves before sending. Every new support email gets a label, a priority and a draft reply grounded in your docs, and a person sends each reply after reading it."
---

# Triage your support inbox and draft replies that a person approves before sending

Source: https://agentshandbook.com/p/triage-support-inbox-with-approved-replies (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/triage-support-inbox-with-approved-replies.md

An agent reads each new support email, labels it by type and urgency, finds the answer in your help docs and writes a draft reply with the source it used. A person reads and sends every reply. Do not let the agent send on its own. Public cases at Air Canada and Cursor show support bots inventing policies that customers acted on, and a tribunal held the company responsible for what its chatbot said.

## Stop and ask the user

- Approve the label set, the escalation rules and the help docs the agent may use.
- Read and send every reply yourself. The agent only writes drafts.
- Handle refunds, discounts, legal, security and angry customers yourself.

## Steps

1. **Write the rules and gather the docs.** List your labels, what counts as urgent and what must go to a person. Collect help docs and policies into one place. Remove old policy pages, because the agent will quote them. Check: Every label and escalation rule fits on one page, and old policies are gone.
2. **Run on past tickets first.** Run the prompt on [20] resolved tickets and compare the drafts with what your team actually sent. Look for any promise not in the docs. Check: No draft promises anything your docs do not say.
3. **Connect the inbox in draft-only mode.** Connect the agent so it can read the inbox and create drafts but not send. Several builders who sell draft tools describe this split as the design: the AI drafts, a person submits. Check: A test email gets a draft in its thread and nothing is sent.
4. **Review and send each draft.** Read each draft and its source. Edit, then send. Track how many drafts you send unchanged, changed or discarded. Check: You sent every reply yourself and logged the outcome.
5. **Handle escalations fast.** Answer escalated emails yourself the same day. In the Cursor case, the correction came hours after the wrong answer had spread online. Check: Every escalated email has a human reply.
6. **Update the docs from what you fix.** When you correct a draft because the docs were missing or wrong, fix the doc. The agent can only be as right as its sources. Check: Each repeated correction becomes a doc change.

## Known failures

- The bot invents a policy, such as a login rule or a refund window, and customers act on it. Fix: Allow answers only from written sources, block promises not in them, and keep a person on every send. A Cursor co-founder said AI replies were their first filter for email support when its bot invented a device policy.

- The company argues the bot's answer is not its responsibility. Fix: Assume it is. The BC tribunal in Moffatt v. Air Canada held the airline responsible for all information on its website, chatbot included.

- Customers do not know a bot answered, and feel deceived when it goes wrong. Fix: Do not sign AI drafts with a made-up human name. Critics of the Cursor case faulted the lack of disclosure.
- The bot gives different answers to the same question. Fix: Ground every draft in a source and show the source to the reviewer. The Markup found New York City's business chatbot gave conflicting answers to the same housing question.

- Drafts quote outdated help docs. Fix: Keep one current source of truth and remove old pages before you connect the agent.

## Starting prompt

```text
You help me run support for [company], which sells [product]. You triage and draft. You never send.

Sources you may use: [help center URL], [policy doc: refunds, cancellations, SLAs], [known issues list]. If the answer is not in these sources, do not answer from general knowledge.

For each unread email in [inbox or label]:
1. Label it with one type: [billing, bug, how-to, account access, feature request, cancellation, other]. Set priority: urgent if [the customer cannot use the product, a payment failed, a security or data issue, legal threat], otherwise normal.
2. Escalate, and write no draft, if the email asks for a refund, discount, contract change, legal or security answer, or if the customer is very upset. Write one line on why.
3. Otherwise, write a draft reply of under [150] words in [tone]. Answer only from the sources above. Under the draft, list the source URL or section you used.
4. If you are not sure, write a draft that asks the customer one clear question, and mark it "low confidence".
5. Never promise a refund, credit, deadline, new feature or policy that is not written in the sources. Do not say a human wrote the reply.

Output a table: sender, subject, type, priority, escalate (yes or no), reason, draft reply, source, confidence.

Save drafts as replies in the original thread only. Do not send. STOP after [10] emails and show me the table.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"triage-support-inbox-with-approved-replies","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.