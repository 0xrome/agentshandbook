---
name: fix-internal-links-and-orphan-pages
description: "Map your internal links, fix orphan pages and point each topic cluster at one hub page. Every important page gets links from related pages, orphan pages are linked or removed, and each topic has one hub page."
license: CC-BY-4.0
metadata:
  author: "Ilias Ism (seo-skills); Agents Handbook editors"
  source: https://agentshandbook.com/p/fix-internal-links-and-orphan-pages
  version: "2026-10-13"
---

# Map your internal links, fix orphan pages and point each topic cluster at one hub page

Source: https://agentshandbook.com/p/fix-internal-links-and-orphan-pages (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/fix-internal-links-and-orphan-pages.md

An agent crawls your site, counts how many internal links point at each page, and lists orphan pages and pages with only one or two links. You tag each page as money, supporting or low value. The agent groups pages by topic, picks one hub per group, and proposes new links with descriptive anchor text and the sentence where each one goes. Review every link in context before it ships, because too many links weaken each one.

## Stop and ask the user

- Approve the page tags (money, supporting, low value) and the hub for each topic.
- Review each proposed link in its sentence before the agent edits pages.
- Approve any merge, redirect or deletion of low-value pages yourself.

## Steps

1. **List every page.** Paste the prompt. The agent combines the sitemap with a crawl, because pages that nothing links to are often missing from one of them. Check: The list includes pages you forgot you published.
2. **Count links per page.** The agent counts the links that point at each page. Links in the main text matter most. A page linked only from the footer is close to an orphan. Check: You see a table of links in and links out per page.
3. **Tag the pages.** Confirm or change the agent's tags. Money pages sell or convert. Supporting pages answer related questions. Low-value pages may need a merge, a redirect or no action. Check: Every page has one tag that you approved.
4. **Choose one hub per topic.** For each group of related pages, pick the page that best covers the topic. Supporting pages link to it, and it links to the money page. Check: Each topic has one hub.
5. **Settle pages that compete.** If two pages target the same query, pick one to own it. Link the other one to it, or merge them with a redirect. Check: Each important query has one owner page.
6. **Review the proposed links in context.** Read each new link in its sentence. Reject links that interrupt the reader or point to a page the reader does not need next. Use anchor text that describes the target page. Check: Each approved link reads naturally.
7. **Apply, then crawl again.** The agent adds the approved links. Run the crawl again and compare the counts. Check: No important page is an orphan, and the hubs gained links.
8. **Set the rule for new posts.** Write a rule into your publishing checklist. For example, every new post links to its hub and to two related posts, and gets links from at least three existing pages. Check: The rule is written where you and your agent will see it.

## Known failures

- The agent adds so many links that each one carries little weight. Fix: Cap new links per page in each pass, and keep only links a reader would click.
- Every link to a page uses the same anchor text. Fix: Ask for varied, descriptive anchors that match the sentence.
- The links load with JavaScript and crawlers cannot follow them. Fix: Use normal anchor elements with an href. Google says it can only reliably follow links in that form.
- The agent links to URLs that redirect. Fix: Ask it to link to the final URL of each target.
- The audit counts menu and footer links and hides real orphans. Fix: Count links in the main content separately from navigation links.

## Starting prompt

```text
Map the internal links of [https://example.com]. The content is in [this repository / the CMS export at data/pages.csv].

1. List every published URL from the sitemap and from a crawl of internal links. Include pages that no other page links to.
2. For each URL, count the internal links that point to it, the links it sends out, and the anchor texts used. Count only links in the main content, and report menu and footer links separately.
3. List orphan pages (0 links in) and near-orphans (1 or 2 links in).
4. Propose a tag for each page: money (it sells or converts), supporting (it answers a question related to a money page), or low value. Wait for me to confirm the tags.
5. Group pages by topic. For each group, propose one hub page. Supporting pages link to the hub, and the hub links to the money page.
6. Find pairs of pages that target the same query. Say which one should own it.
7. Propose new links. For each one, give the source page, the target page, the anchor text and the exact sentence where it goes. Vary the anchor text. Add no more than [3] new links to any one page in this pass.
8. Write the plan to [seo/internal-links-YYYY-MM-DD.md] and wait for my approval before you edit anything.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"fix-internal-links-and-orphan-pages","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
