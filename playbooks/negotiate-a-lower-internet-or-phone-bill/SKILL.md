---
name: negotiate-a-lower-internet-or-phone-bill
description: "Negotiate a lower internet or phone bill with an agent-prepared script or chat. You lower your bill, or get a firm answer from retention, without agreeing to a plan change or contract you did not approve."
---

# Negotiate a lower internet or phone bill with an agent-prepared script or chat

Source: https://agentshandbook.com/p/negotiate-a-lower-internet-or-phone-bill (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/negotiate-a-lower-internet-or-phone-bill.md

Give a chat assistant your bill, your plan details and current competitor offers, and ask it for a short script with a clear ask, a fallback and a walk-away line. Then make the call or chat yourself, or let an agent run the provider's web chat with strict limits on what it may agree to. Expect the first answer to be no. Reported results include a $10 a month discount and savings of a few hundred dollars a year, plus a bot that invented outages and agents that stalled at verification codes.

## Stop and ask the user

- Approve the script and the limits (lowest acceptable price, no plan change, no new contract) before any contact.
- Read and approve any offer before it is accepted on your account.
- Enter any one-time verification code yourself.

## Steps

1. **Collect your facts.** Get your last two bills, your plan details and two or three competitor offers at your address. Write down any real outages with dates. Decide your target price and whether you would accept a plan change or contract. Check: You have one page with your price, your target, competitor prices and your limits.
2. **Ask the agent for a script and a refusal list.** Paste the prompt. One tester found the first script generic until she added her own details, such as years as a customer. Check: The script fits on half a page and lists offers you will refuse.
3. **Make the contact yourself, or watch the agent.** Call or open the provider's chat. If an agent runs the chat, keep the window open and watch. Expect the first answer to be no, and ask for retention or loyalty. Check: You reach someone who can change your price.
4. **Approve the offer before it is applied.** Ask for the new monthly price, how long it lasts, what happens after, and any contract. Compare it with your limits. Accept only if it fits. Check: The offer is within your limits, and you accepted it yourself.
5. **Get it in writing and check the next bill.** Ask for a confirmation email or chat transcript. Set a reminder for when the discount ends. Check: Your next bill shows the new price.

## Known failures

- The agent invents problems, such as outages, to win a discount. Fix: List the only facts it may use, and tell it never to claim anything else. In one early demo, the bot made up outages the customer never had.
- The agent agrees to a plan change, contract or add-on you did not want. Fix: Write your limits into the prompt, and require it to stop and ask before accepting any offer.
- The provider sends a one-time code during the chat or call, and the agent cannot continue. Fix: Stay nearby and enter the code yourself. Voice agent builders report pausing for the user or calling the user to relay the code.
- The first script is generic, or the first answer from the provider is no. Fix: Add your real details, and ask for retention. One user says Verizon first said nothing could be done, then gave a discount when the agent pressed.
- Phone menus, transfers and robotic voices stall an AI caller. Fix: Use web chat where you can, or let the agent only reach a human and then hand the call to you.

## Starting prompt

```text
Help me lower my [internet / mobile] bill with [provider]. Do not invent facts about my service. If you need a fact, ask me.

My facts:
- Plan: [plan name, speed or data, lines], paying [amount] a month, customer since [year]
- Bill details: [paste the bill lines, including fees and any promo that ended]
- Real service problems, if any: [dates of outages], or "none"
- Competitor offers at my address: [provider, plan, price, link], checked on [date]
- What I will accept: [target price] for the same plan. I [will / will not] change plan. I [will / will not] sign a contract.

1. Find any fee or price on my bill that changed or looks wrong, and say why.
2. Write a short script for a call or chat: who I am, what I pay, the competitor price, a clear ask, one fallback ask, and a polite line to ask for the retention or loyalty team.
3. List the offers I should refuse, based on my limits.
4. Give me 3 likely replies from the provider and how to answer each.
Do not contact the provider. I will make the call or chat myself.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"negotiate-a-lower-internet-or-phone-bill","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.