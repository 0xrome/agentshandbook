---
name: monitor-competitor-pricing-pages-weekly
description: "Watch competitors' pricing and product pages and get a weekly briefing of real changes. Every week you get a short briefing of meaningful changes to competitors' pricing and product pages, each with the before text, the after text and a link to the saved snapshot."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/monitor-competitor-pricing-pages-weekly
  version: "2026-10-13"
---

# Watch competitors' pricing and product pages and get a weekly briefing of real changes

Source: https://agentshandbook.com/p/monitor-competitor-pricing-pages-weekly (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/monitor-competitor-pricing-pages-weekly.md

Keep a short list of competitor pages. A scheduled job saves a copy of each page, compares it with last week's copy, and asks a model to classify each change and write a short briefing. Keep the old snapshots so you can check every claim. Builders report that most raw changes are noise (banners, A/B tests, error pages), that text extraction can mangle prices, and that AI filters can fail silently, so the briefing must show the before and after for every change.

## Stop and ask the user

- Approve the list of pages and the run frequency before the first run.
- Check the saved before and after snapshot before you act on any pricing change.

## Steps

1. **Pick the pages and the ignore list.** Start with 5-15 pages. Write down what counts as a real change and what to ignore. Builders report that rotating banners, currency toggles and A/B tests cause most false alerts. Check: You have a watchlist and an ignore list on one page.
2. **Run once by hand.** Paste the prompt and let the agent take the first snapshots. Look at the screenshots to confirm it saw the real page, not a bot check. Check: Every page has a saved text file and a screenshot that matches what you see in your browser.
3. **Test the failure path.** Add a URL that returns an error. The run must list it as a failed fetch, not as a change. One builder reports phantom changes from error pages until they treated them as a separate state. Check: The error URL shows under "failed to fetch".
4. **Schedule it weekly.** Set the job to run once a week. Weekly keeps cost and request volume low. Check: The scheduler shows the next run date.
5. **Review three briefings before sharing.** For each change in the briefing, open the before and after snapshots. Check prices against the screenshot. Tune the ignore list. Check: Three briefings in a row have no false changes.
6. **Share the briefing.** Turn on posting to your team channel. Keep reading the "failed to fetch" list, because a silent failure looks like a quiet week. Check: Your team gets the briefing and each change links to its snapshot.

## Known failures

- The briefing is full of noise such as banners, A/B tests and edits that are not product changes. Fix: Keep an ignore list, strip those parts before the diff, and ask the model to classify each change with the before and after text shown.
- Error pages or bot checks show up as big changes. Fix: Detect failed fetches and never diff them against the last good copy.
- Text extraction mangles prices. Fix: Save a screenshot and check every price against it. One builder now verifies price detections against screenshots for this reason.
- The AI filter fails silently, so alerts flood in or real changes are hidden. Fix: Treat an AI error as "unknown" and send the raw diff. Users of an open-source change monitor filed issues where model errors made every change look important, or hid a change for good.

- Sites that rely on JavaScript or block headless browsers return empty pages. Fix: Render pages in a real browser and log a fetch failure when the visible text is empty or a bot check appears.
- A run costs far more than expected. Fix: Run weekly, only send changed pages to the model, and set a spending cap. One self-hosted agent user warned that a misconfigured job can burn through 200 dollars of credits in a few hours.


## Starting prompt

```text
Set up a weekly competitor watch for me. Read only. Do not log in to any site, fill in forms or contact anyone.

Pages to watch: [list of URLs, for example competitor-a.com/pricing, competitor-a.com/changelog, competitor-b.com/pricing].
What I care about: [prices and plan limits, new features, positioning and headline changes, new integrations].
What to ignore: [cookie banners, promo banners, testimonials rotating, dates in footers, currency toggles].

Each run:
1. Fetch each page with a real browser render if the page needs JavaScript. Save the visible text and a screenshot to [folder]/[site]/[YYYY-MM-DD]/.
2. If a fetch fails, returns an error page, a login wall or a bot check, record it as FETCH FAILED. Never compare a failed fetch with last week's copy.
3. Compare the text with the last good snapshot. Skip the page if nothing changed after removing the ignore list.
4. For each real change, write: page, category (pricing, feature, positioning, other), the exact before text, the exact after text, and one sentence on why it may matter to [my company]. For any price, quote the number from the page and confirm it against the screenshot.
5. Write a briefing of at most [one page]: real changes first, grouped by competitor, then a list of pages that failed to fetch.

Rules:
- Never invent a change. If you are unsure, show the diff and mark it "check".
- Keep every old snapshot. Do not overwrite the baseline.
- Show me the briefing. Do not post it to [Slack or email] until I approve the first three runs.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"monitor-competitor-pricing-pages-weekly","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
