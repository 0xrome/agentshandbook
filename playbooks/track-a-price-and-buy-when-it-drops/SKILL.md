---
name: track-a-price-and-buy-when-it-drops
description: "Track a product's price and buy when it drops below your target, with you approving the purchase. You buy the exact product you chose at or below your target price, and you pay for it yourself after checking the final total."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/track-a-price-and-buy-when-it-drops
  version: "2026-10-13"
---

# Track a product's price and buy when it drops below your target, with you approving the purchase

Source: https://agentshandbook.com/p/track-a-price-and-buy-when-it-drops (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/track-a-price-and-buy-when-it-drops.md

Pin down the exact product, seller and target price first. Then pick a way to watch it: a weekly check-in with a chat assistant, or a small tracker that a coding agent builds for you. When the price looks right, check the real price, variant and stock on the shop's own page, let a browser agent fill the cart, and pay yourself. Testers report wrong prices read from pages, a wrong brand picked because the site said it was almost sold out, and Amazon blocking agents.

## Stop and ask the user

- Approve the exact product, variant, seller and target price before tracking starts.
- Check the final price, variant, seller and stock on the shop's own page when an alert fires.
- Enter payment and press the final buy button yourself.

## Steps

1. **Define the exact product and your target.** Write the model number, variant, condition, the shops and sellers you accept, and the most you will pay including shipping and tax. A wrong variant or a marketplace seller can look like a price drop. Check: You have one line that a stranger could use to buy the right item.
2. **Choose how to watch the price.** For one or two items, a weekly check-in with a chat assistant is enough. One writer pastes the product link and the shop's price history screenshot each week and asks whether the price looks low, average or high. For many items, ask a coding agent to build a tracker that saves every reading. Check: You have a check-in reminder or a tracker that records a first reading.
3. **Check each reading against the page.** When a price looks good, open the shop's page yourself. Trackers can read a savings amount, a pre-discount price, the wrong currency, or "out of stock" by mistake. Some discounts only show in the cart. Check: The price you see on the page matches the reported price, for the right variant and seller.
4. **Approve one offer.** Tell the agent which single offer you accept. Do not ask it to "buy the cheapest", which lets it pick a different product or seller. Check: The agent repeats back one link, one variant, one seller and one price.
5. **Let the agent fill the cart, then pay yourself.** Use a browser agent to add the item and reach checkout, or do it yourself. Read the final total, then enter payment and press the buy button yourself. Check: Your order confirmation shows the right item, seller and a total at or below your target.

## Known failures

- The agent cannot open Amazon or another big shop at all. Fix: Do that shop by hand, or track it with the shop's own price alerts. Let the agent handle smaller shops.
- The tracker reads the wrong number, such as a savings amount, the price before a cart discount, or the wrong currency. Fix: Prefer structured price data, store the method used, and flag big jumps for review. Always confirm on the page before you buy.
- The agent adds a different brand or variant because the page says it is almost sold out. Fix: Approve one exact offer by link and variant, and tell the agent to ignore urgency messages.
- The assistant "predicts" a price drop. Fix: Ask only whether the current price is low compared with the history you give it. One writer notes that it cannot predict the future.
- Prices shown inside AI shopping answers can differ from the shop. Fix: Check the price on the shop's own page. One study found AI Mode in Google showed higher prices than normal search for the same products.

## Starting prompt

```text
Help me buy one product when its price drops.

Product: [brand, model, model number, size or colour, new or used]
Shops I trust: [shop 1 URL, shop 2 URL]
Target: [price] or less, including shipping and tax, delivered to [city or ZIP] by [date].
Current price I see: [price, date]

1. Confirm that each link points to exactly this product and variant. List anything that differs (seller, condition, bundle, size).
2. Each time I ask, check each link and report: price, any discount that only applies in the cart or with a code, shipping, seller, stock, and the time you checked. Quote the price as the page shows it. If a page blocks you or you cannot see the price, say so. Do not guess.
3. Tell me if any offer meets my target. Do not tell me a price will drop. You cannot know that.
4. STOP. Do not add to cart or buy anything until I say "go" for one specific offer.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"track-a-price-and-buy-when-it-drops","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
