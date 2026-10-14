---
name: run-a-technical-seo-audit-of-your-site
description: "Run a technical SEO audit of your site and fix what stops Google from crawling it. You get a ranked list of crawl and index problems, the file that causes each one, and fixes that you reviewed and deployed."
license: CC-BY-4.0
metadata:
  author: "Ilias Ism (seo-skills); Agents Handbook editors"
  source: https://agentshandbook.com/p/run-a-technical-seo-audit-of-your-site
  version: "2026-10-13"
---

# Run a technical SEO audit of your site and fix what stops Google from crawling it

Source: https://agentshandbook.com/p/run-a-technical-seo-audit-of-your-site (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/run-a-technical-seo-audit-of-your-site.md

Ask a coding agent to fetch your sitemap, request every URL, and check status codes, redirects, canonicals, noindex rules, robots.txt and internal links against the code that produces them. Make it sort the findings by what stops pages from being crawled or indexed, and tell it to skip health scores. Review each fix as a diff before you deploy. One founder reports that the agent found a robots rule that had blocked his whole site for weeks.

## Stop and ask the user

- Approve the list of fixes before the agent edits any file.
- Review every diff to robots.txt, canonicals, redirects and noindex rules before you deploy.
- Confirm that a redirect or a noindex rule is a mistake before the agent removes it. Some are on purpose.

## Steps

1. **Point the agent at the site and the code.** Open the agent in the repository that serves the site. Ask it to find the files that make the sitemap, robots.txt, titles, canonicals and redirects before it crawls anything. In Next.js these are often app/sitemap.ts, app/robots.ts and generateMetadata. Check: The agent names the file for each of these five items.
2. **Crawl the sitemap and the internal links.** Paste the prompt. The agent requests each URL and saves one row per URL. Keep the request rate low so your host or CDN does not block it. Check: You have one row per URL with a status code, a canonical and a count of inbound links.
3. **Check the host and protocol redirects.** Ask the agent to request the http and www versions of your home page and two deep pages. Each one must reach the same final URL with one 301. Check: Every version ends on one host with one hop.
4. **Compare raw HTML with the rendered page.** Some sites load the menu or the main text with JavaScript. A crawler that does not run scripts then sees an empty page. Ask the agent to diff the raw HTML against the rendered page for each template. Check: The main text and the navigation links appear in the raw HTML.
5. **Add Google's view from Search Console.** If you connected Search Console, ask for the pages that Google reports as not indexed and the reason for each. This catches problems a crawl cannot see, such as duplicate pages where Google chose a different canonical. Check: Each page that is not indexed has a reason next to it.
6. **Rank the findings by impact.** Read the report. Move anything that blocks crawling or indexing to the top. A missing file is not always a problem. For example, a small site with good internal links can rank without an XML sitemap. Ask the agent to explain the impact of each item on your site, not in general. Check: The top five items each block or confuse Google on real pages.
7. **Approve and apply the fixes.** Approve the fixes one group at a time. The agent edits the files and shows you a diff. Read every change to robots rules, canonicals, redirects and noindex tags. Check: You approved each diff, and the build passes.
8. **Deploy and crawl again.** After the deploy, ask the agent to run the same crawl and diff it against the first report. Check: The new report shows the fixed items as resolved and no new errors.

## Known failures

- The agent gives a health score and marks every missing file as critical. Fix: Tell it not to score the site. Ask it to rank each finding by its effect on crawling and indexing of real pages on your site. One SEO who tested a popular audit skill found most of its critical items had low impact.
- The audit misses pages with only one or two internal links, or a menu that loads with JavaScript. Fix: Ask for a count of inbound internal links per URL, and a raw versus rendered HTML diff per template. The same tester hid his menu on purpose and the skill did not notice.
- The agent removes a redirect or a noindex rule that was on purpose. Fix: Ask it to list the redirects and noindex rules it wants to change, with the reason, and approve each one before it edits a file.
- The crawl reports many 403 or 429 errors that real visitors never see. Fix: Slow the crawl down, give it a clear user agent, and allow it in your CDN or firewall settings. Or run the crawl from your own machine.
- The crawl is clean but Google still does not index some pages. Fix: Use URL Inspection in Search Console. Google states the reason, for example a duplicate where it chose another canonical, or a page it crawled but did not index.

## Starting prompt

```text
Audit [https://example.com] for technical SEO. The code that serves the site is in this repository.

1. Fetch [https://example.com/sitemap.xml] and /robots.txt. Request every URL in the sitemap, and every internal link you find on those pages. Send no more than [2] requests per second.
2. For each URL, record: status code, final URL after redirects, number of redirect hops, canonical tag, meta robots tag, X-Robots-Tag header, title, meta description, H1, and the number of internal links that point to it.
3. Check the host rules: http must 301 to https, and www and non-www must 301 to one host. Check that the trailing-slash rule is the same on every page.
4. For [3] page templates, compare the raw HTML with the rendered page. Flag any main content or navigation that only appears after JavaScript runs.
5. Group the findings in this order:
   a. Blocks crawling or indexing (robots rules, noindex on real pages, 4xx or 5xx pages that get links).
   b. Sends Google conflicting signals (a canonical that points to a redirect or a noindex page, sitemap URLs that redirect or return 404).
   c. Weak pages (missing or duplicate titles, pages with 0 to 2 internal links).
   d. Minor items.
   Do not give a health score.
6. For each finding, name the file or setting that causes it and propose the smallest fix.
7. Write everything to [seo/audit-YYYY-MM-DD.md]. Then stop and wait for my approval before you change any file.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"run-a-technical-seo-audit-of-your-site","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
