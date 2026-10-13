---
name: claim-flight-delay-compensation
description: "Claim compensation for a delayed or cancelled flight under EU261, UK261 or US refund rules. You know which rule applies and what you can claim, and you have sent a claim with your evidence attached and a plan for the next step if the airline refuses."
---

# Claim compensation for a delayed or cancelled flight under EU261, UK261 or US refund rules

Source: https://agentshandbook.com/p/claim-flight-delay-compensation (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/claim-flight-delay-compensation.md

Give a chat assistant your booking, the airline's emails and your receipts, and ask it to check which rule covers your trip before it drafts anything. Then let it write separate claims for compensation and for expenses, and check each legal point on the official EU, UK or US page. You send every message and submit every form yourself. Expect weeks or months of waiting, and a first refusal you may need to answer.

## Stop and ask the user

- Confirm which rule applies on the official EU, UK or US page before any claim is drafted.
- Read and approve every claim, email and form before you send it yourself.
- Decide yourself whether to accept any offer, voucher or settlement.

## Steps

1. **Collect the facts and the evidence.** Put the booking, every airline email, your boarding passes and your receipts in one folder. Write down the scheduled and actual arrival time at your final destination. Note when the airline told you about the change. Check: You have one folder with every document and a short timeline of what happened.
2. **Ask the agent which rule applies.** Paste the prompt with your facts. Ask the agent to go flight by flight. The EU rules depend on where the flight departs and whether the airline is an EU carrier. A schedule change made more than 14 days before departure gives no compensation under EU rules. US rules give a refund, not compensation, when a flight is cancelled or changed by 3 hours or more on a domestic trip or 6 hours or more on an international trip. Check: The agent names one rule, explains why, and lists what it is unsure about.
3. **Check the rule yourself on the official page.** Read the EU Your Europe passenger rights page, the UK CAA pages or the US DOT rules. Compare the agent's answer with the page. If they disagree, trust the official page and tell the agent. Check: The official page confirms that your trip is covered and gives the amount.
4. **Draft separate claims.** Ask for one letter for the fixed compensation and one for expenses such as meals and a hotel. One claimant in the evidence says the agent told him to file them separately. Attach the receipts to the expenses claim. Check: Each letter names the rule, the flight, the amount and the evidence, and nothing in it is invented.
5. **Send the claim yourself.** Use the airline's own claim form or complaint address. If you use a browser agent to fill the form, it must stop before Submit. Save a copy of what you sent and the date. Check: You get an acknowledgement or case number from the airline.
6. **Answer a refusal with the next step.** If the airline refuses or does not reply, paste its answer into the chat and ask the agent to check the reason against the rule. Under EU rules, technical faults are not extraordinary circumstances, and the airline must prove its case. The Your Europe page says you can go to the national enforcement body after two months with no reply. Check: You have a reply, or a complaint to the enforcement body or court, ready for your approval.

## Known failures

- The agent says EU rules apply when they do not, for example to a non-EU airline flying into the EU, or to a schedule change announced weeks ahead. Fix: Make the agent reason flight by flight, then check its answer on the official page before you draft anything.
- The agent defaults to EU law when UK law (UK261) is the one that applies. Fix: Tell the agent the departure country and ask it to name the law for that country. One poster says he had to point the agent to UK law directly.
- The airline ignores the claim or sends a template refusal. Fix: Keep every date. Escalate to the national enforcement body, an alternative dispute body or small claims court, and ask the agent to draft that complaint for you to send.
- A settlement offer quietly drops part of what you are owed, such as interest or costs. Fix: Ask the agent to compare the offer with your claim line by line before you accept anything.
- The airline's web form fails, for example it will not accept uploads. Fix: Ask the airline which other channel it accepts. Do not rely on a channel that only the agent suggests.

## Starting prompt

```text
Help me claim compensation for a disrupted flight. Act as a careful researcher, not as my lawyer.

My facts:
- Booking: [airline, booking reference, one ticket or separate tickets]
- Every flight on the ticket: [flight number, from, to, operating airline, scheduled and actual times]
- What happened: [delay / cancellation / missed connection / denied boarding], reason the airline gave: [reason]
- When the airline told me: [date and time of the notice]
- What I paid for myself: [meals, hotel, new ticket], with receipts: [yes/no]
- Where I live: [country]

Steps:
1. Tell me which rule could apply: EU 261/2004, UK261, US DOT refund rules, or none. Explain your reasoning flight by flight. Say where you are unsure, and give me the official page I should read to check it.
2. STOP and wait for me to confirm that I checked the rule.
3. List what I can claim: fixed compensation, refund, and my expenses. Treat each one as a separate claim. Use only amounts from the official page.
4. Draft each claim as a short, polite letter. Cite the rule and article, include my evidence list, and ask for payment by bank transfer, not vouchers.
5. Tell me where to send it (the airline's own claim form or address) and the next step if the airline refuses or does not reply.
Do not send, submit or file anything. Do not invent facts, case names or amounts. If you need a fact, ask me.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"claim-flight-delay-compensation","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.