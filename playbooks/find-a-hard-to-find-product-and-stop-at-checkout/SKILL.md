---
name: find-a-hard-to-find-product-and-stop-at-checkout
description: "Track down a specific product in stock and stop at checkout for you to pay. You see a short list of real offers for the exact item, and you pay for the one you chose on a site you trust."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/find-a-hard-to-find-product-and-stop-at-checkout
  version: "2026-10-13"
---

# Track down a specific product in stock and stop at checkout for you to pay

Source: https://agentshandbook.com/p/find-a-hard-to-find-product-and-stop-at-checkout (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/find-a-hard-to-find-product-and-stop-at-checkout.md

Describe the exact product, the most you will pay and the shops you trust, and ask a browser agent to check stock across those shops and report back with links. Pick one offer yourself, let the agent add it to the cart, and take over for shipping and payment. Testers report agents that found an item quickly and stopped at payment, and also big shops that blocked the agent.

## Stop and ask the user

- Approve the offer (shop, seller, exact item, total with shipping) before the agent adds anything to a cart.
- Enter shipping and payment details yourself on the final page.

## Steps

1. **Describe the exact item.** Write the full product name with model, size and colour, your price limit including shipping, your delivery deadline and the shops you trust. Check: Someone else could find the same item from your description.
2. **Let the agent check stock.** Paste the prompt. Watch the first few minutes. If a shop blocks the agent, let it move on. Check: You get a table of offers with links and exact item titles.
3. **Check the offers yourself.** Open the link for your top offer. Compare the item title, seller and total with the table. Check: The listing you opened matches the agent's table.
4. **Approve one offer.** Tell the agent which offer to buy and the quantity. Check: The agent puts exactly that item and quantity in the cart.
5. **Take over and pay.** When the agent stops at shipping or payment, take control, enter your details and pay. Check: You get an order confirmation with the right item, seller and total.

## Known failures

- A large shop blocks the agent again and again. Fix: Put several shops in your list and tell the agent to note a block and move on. Check the blocked shop yourself.
- The agent cannot finish checkout without your address, login or card. Fix: This is expected. Take over at that step and pay yourself.

## Starting prompt

```text
Find [exact product name, model or variant, size, colour] for delivery to [ZIP code / city] by [date]. Maximum total including shipping and tax: [USD 60]. Only buy from these shops or the brand's own store: [list]. Skip marketplace sellers with fewer than [100] ratings, and skip anything described as used, open box, bundle or "similar".

Step 1. Check stock at each shop. For each offer give: shop, seller name, exact item title as listed, price, shipping, delivery estimate, return policy, and the link. If a shop blocks you or asks for a login, note it and move on.
STOP and show me the offers. Do not add anything to a cart yet.
Step 2. When I pick an offer, add exactly [1] of that item to the cart and go to checkout. Use guest checkout unless I log in myself.
STOP at the shipping and payment step. Read back the item title, seller, quantity and total from the page. Do not enter my address or card details. I will take over and pay.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"find-a-hard-to-find-product-and-stop-at-checkout","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
