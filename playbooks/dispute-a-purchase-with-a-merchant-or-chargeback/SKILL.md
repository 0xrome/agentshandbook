---
name: dispute-a-purchase-with-a-merchant-or-chargeback
description: "Get a refund from a merchant, then dispute the card charge if they refuse. You send the seller a clear refund request with evidence, and if that fails you file a card dispute on time with the same evidence."
---

# Get a refund from a merchant, then dispute the card charge if they refuse

Source: https://agentshandbook.com/p/dispute-a-purchase-with-a-merchant-or-chargeback (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/dispute-a-purchase-with-a-merchant-or-chargeback.md

Give a chat assistant your order, receipts, the seller's messages and their policy page, and ask it to build a timeline and a short, factual refund request that you send yourself. If the seller refuses or goes silent, have it draft a card dispute and check the deadline on your card issuer's page. Check every law or policy it cites before you send. People report refunds and a replaced item, and also drafts that suggested rules that did not fit the facts.

## Stop and ask the user

- Check every law, policy and deadline in the draft against the official or merchant page before you send it.
- Send the merchant letter yourself, from your own account.
- Submit the card dispute yourself on your card issuer's site or by mail.

## Steps

1. **Collect the evidence.** Put the order, receipts, photos, tracking, the policy page and every message with the seller in one folder. Note the date of the statement where the charge first appeared. Check: You have one folder and you know the date of the first statement that shows the charge.
2. **Build the timeline and pick a route.** Paste the prompt with your facts. The agent builds a timeline and lists your routes. For US credit cards, the FTC says a written billing error dispute must reach the issuer within 60 days after the first bill that shows the error. Check your issuer's page for the rules that apply to you. Check: You see a dated timeline and a route with a deadline that you checked on an official page.
3. **Check the draft line by line.** Read every claim in the draft. Delete any law or rule you cannot find on an official page. Rewrite parts in your own words. A UK consumer expert quoted by one writer says legalistic complaints get legalistic replies. Check: The letter states only facts you can prove and rules you have checked.
4. **Send the merchant request yourself.** Send it from your own email or the seller's contact form. Attach the evidence. Save a copy and the date. Check: You have a sent copy and, ideally, a ticket number or reply.
5. **Answer a refusal with their own reason.** If the seller refuses, paste the reply into the chat. Ask the agent to answer the reason they gave, point by point. One traveller says an airline refused, then agreed after a second letter that answered its stated reason. Check: Your reply addresses each reason in their refusal.
6. **File the card dispute yourself if they still refuse.** Ask the agent for the dispute text. Submit it on your card issuer's site or send it to the billing inquiries address, not the payment address. Keep paying the parts of the bill you do not dispute. Check: The issuer confirms that it received your dispute.

## Known failures

- The draft cites a law, a chargeback route or a deadline that does not fit your case. Fix: Ask the agent which facts each rule depends on, then check the rule on the official page. One writer found a draft that suggested a chargeback and a credit card law without checking how she had paid.
- The assistant backs your case even when it is weak. Fix: Ask it to argue the seller's side and list the weak points before you send anything.
- A long, formal AI letter gets a template reply. Fix: Keep the letter short and in your own words. Use the agent for the timeline and the evidence list.
- The seller ignores you or replies with copy-paste excuses. Fix: Set a clear deadline in the first letter. When it passes, move to the card dispute or payment platform claim before that deadline runs out.

## Starting prompt

```text
Help me get a refund. Act as a careful helper, not as my lawyer. Do not invent facts, laws or deadlines. If you need a fact, ask me.

Facts:
- What I bought: [item], from [merchant, website], on [date], for [amount and currency], paid with [credit card / debit card / PayPal / other].
- What went wrong: [not delivered / not as described / faulty / cancelled service / charged twice].
- What I already did: [dates and summary of each message to the merchant, and their replies].
- Their returns or refund policy: [paste the text or link].
- Where I live: [country and state].

Steps:
1. Build a dated timeline from my facts and messages. Mark any gaps.
2. Tell me the routes I have: merchant refund, card dispute, payment platform claim, or none. For each route, give the deadline and the official page where I can check it. Say where you are unsure.
3. STOP and wait for me to confirm the facts and the route.
4. Draft a short refund request to the merchant: under 200 words, polite and specific, citing their own policy, listing my evidence, asking for a refund by [date, for example 7 or 14 days]. Use plain words, not legal threats, unless I ask.
5. If I tell you the merchant refused, draft a card dispute letter or the text for my issuer's dispute form, with the timeline and the evidence list.
Do not send, submit or file anything.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"dispute-a-purchase-with-a-merchant-or-chargeback","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.