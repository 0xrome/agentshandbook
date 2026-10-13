---
name: plan-weekly-meals-and-fill-a-grocery-cart
description: "Plan a week of dinners and fill a grocery cart that you check and pay for. You have a week of dinner recipes, one shopping list grouped by aisle, and a reviewed cart at your store that you paid for yourself."
---

# Plan a week of dinners and fill a grocery cart that you check and pay for

Source: https://agentshandbook.com/p/plan-weekly-meals-and-fill-a-grocery-cart (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/plan-weekly-meals-and-fill-a-grocery-cart.md

Give an assistant your household, diet rules, budget and what is already in your kitchen, and ask for a week of dinners and one combined shopping list. Then let it load the list into a grocery cart, through the Instacart app in ChatGPT or a browser agent on your store's site. Review every item, quantity and substitution in the cart and pay yourself. Reviewers report good plans and lists, and say you still need to remove items you already have and fix quantities.

## Stop and ask the user

- Approve the meal plan before the agent builds the list.
- Review every cart line (item, size, quantity, substitution setting) before checkout.
- Pay yourself, and check the delivery slot and address on the final page.

## Steps

1. **Write your rules and pantry list.** Note who you cook for, diet rules, time limits, budget, store and ZIP code, and the staples you already have. Check: You have one short list of rules and a pantry list.
2. **Approve the dinners.** Paste the prompt. Swap any dinner you will not cook. Ask for shared ingredients so less food goes to waste. Check: You have five dinners you will actually cook.
3. **Approve the shopping list.** Check that pantry items are gone and that pack sizes make sense for the recipes. Fix quantities now, before anything goes in the cart. Check: The list shows only what you need to buy, with sensible pack sizes.
4. **Let the agent fill the cart.** The agent adds the approved list to your cart at your store. If it asks you to sign in, do that yourself. If it shops as a guest, give it your ZIP code so it sees your store's stock. Check: The agent shows a cart table and a comparison with the list.
5. **Review the cart line by line.** Check item, brand, size, quantity and the substitution setting for each line. Remove doubles and anything you already have. Check: The cart matches the approved list and the total fits your budget.
6. **Check out yourself.** Pick the delivery slot, confirm the address and pay. Save the plan and recipes where you will see them during the week. Check: You receive an order confirmation with the right slot and total.

## Known failures

- The cart includes things you already have, or quantities that are too large. Fix: Give a pantry list, ask for pack sizes against recipe amounts, and review the cart line by line. One reviewer advises removing what you already have and swapping brands before you order.
- The first meal plan is too narrow or repetitive. Fix: Ask for changes before the list is built. One reviewer had to ask a second time for more variety.
- The agent shops as a guest and does not know your store or ZIP code. Fix: Give your store and ZIP code in the prompt, or sign in yourself when the agent asks.
- Prices in the plan differ from the checkout total. Fix: Ask the agent to mark prices it did not see on the store's site as estimates, and trust only the cart total.
- The agent picks substitutes you would not choose. Fix: Tell it to list out-of-stock items for you instead of substituting, and set your store's substitution preference yourself.

## Starting prompt

```text
Plan [5] dinners for [2 adults and 1 child] for the week of [date]. Rules: [no pork, no fish, one vegetarian night, each dinner under 45 minutes on weekdays]. Budget for the whole shop: [USD 120]. Store: [my local store name and ZIP code].

Already in my kitchen (do not buy): [rice, olive oil, salt, pepper, garlic, eggs, pasta].

Step 1. Give me the 5 dinners in a table: name, main ingredients, cooking time, and which ingredients are shared with other nights. Reuse ingredients across nights to cut waste.
STOP and wait for me to approve or swap dinners.
Step 2. Make one combined shopping list grouped by aisle. For each line give the amount the recipes need and the pack size you plan to buy. Leave out everything I already have. Show an estimated total, and mark any price you did not see on the store's site as "estimate".
STOP and wait for me to approve the list.
Step 3. Add the approved list to my cart at [store]. Use my store and ZIP code. Choose the closest match in the pack size I approved. If an item is out of stock, do not pick a substitute yourself: list it for me. Set substitutions to [ask me / do not substitute].
Step 4. Show me the full cart as a table (item, size, quantity, price) and the cart total, and compare it with the approved list. Point out anything added, missing or doubled.
STOP before checkout. Do not choose a delivery slot, enter an address or pay. I will do that myself.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"plan-weekly-meals-and-fill-a-grocery-cart","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.