---
name: draft-weekly-newsletter-from-reading-list
description: "Draft your weekly newsletter from the links you saved, in your own voice. You get a draft issue with a short, sourced summary of each link you saved, grouped by theme, plus a list of links the agent could not read."
---

# Draft your weekly newsletter from the links you saved, in your own voice

Source: https://agentshandbook.com/p/draft-weekly-newsletter-from-reading-list (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/draft-weekly-newsletter-from-reading-list.md

Save links during the week. At the end of the week an agent opens each link, confirms it could read the page, summarises it, groups items into themes and drafts the issue in your voice. You check each summary against its link, edit, and send it yourself. The main reported risk is a confident summary of a page the agent never read, so the agent must say which links failed.

## Stop and ask the user

- Review the list of links the agent could not read before it writes.
- Check every summary, quote and number against its source.
- Send or schedule the issue yourself in your email tool.

## Steps

1. **Save links in one place all week.** Use one list so the agent finds every item. Add a short note to a link if you already know why it matters. Check: The list has this week's links and nothing older.
2. **Let the agent read and report.** Paste the prompt. The agent opens each link and reports which pages it could read. Replace or drop links it could not read, or paste their text in yourself. Check: Every link is marked yes, partly or no.
3. **Get the themed draft.** The agent summarises readable links, groups them and writes the issue in your format. Check: Each item has a link, and the draft follows your usual structure.
4. **Check every item against its source.** Open each link and compare. Look hard at titles, author names, numbers and quotes. Large studies of AI assistants by the BBC and the EBU found altered quotes and sourcing errors in a large share of news answers. Check: Every summary matches its page, and every quote is exact.
5. **Add your own take.** Fill each marked spot with your view. This is the part readers subscribe for. Check: No placeholder text is left.
6. **Send it yourself.** Paste the draft into your newsletter tool, send a test to yourself, read it on your phone, then send or schedule it. Check: The test email looks right and every link works.

## Known failures

- The agent summarises a page it never read, from the URL or from memory. Fix: Make the agent report read status for each link before writing, and never summarise a "no". Test once with a broken link to confirm it admits the failure.

- The draft includes a book, title or fact that does not exist. Fix: Allow only items from your list. In 2025 a newspaper printed an AI-made summer reading list with books that do not exist, as 404 Media reported.

- Paywalled or HTML-less pages get only a link, or a thin summary. Fix: Paste the text of those pages yourself, or move them to the short "also worth a look" list.
- The prompt drifts. Small changes give different output each week. Fix: Keep the prompt in one versioned file. One writer says prompt changes behaved unpredictably until he added version control.
- The voice is generic. Fix: Include past issues as samples and leave marked spaces for your own opinion.

## Starting prompt

```text
Draft this week's issue of my newsletter, [newsletter name], for [audience].

Links I saved this week: [paste links, or point to the file, bookmark folder or read-later list].
Three past issues, so you can match my voice: [paste or link].
Format: [intro of 2-4 sentences], then [3-5] themed sections, then [a short "also worth a look" list].

Step 1. Open every link. For each one, record: title, author, publish date, and whether you could read the full text (yes, partly, no). If a page is paywalled, blocked, or you only saw the URL, mark it "no". Do not summarise any page marked "no". STOP and show me this list before you write.

Step 2. After I reply, for each readable link write a summary of 2-3 sentences with one concrete detail from the page. Keep numbers exactly as the page states them. If you quote, copy the words exactly and keep the quote under 20 words.

Step 3. Group the items into themes. Drop items that do not fit the audience and tell me which ones you dropped and why.

Step 4. Write the issue in my voice. Use short sentences. Do not add opinions I have not given you. Mark any place you want my own take with [MY TAKE: add your view here].

Rules:
- Every item links to its source.
- Never invent a title, author, book or statistic. If you are unsure, leave it out and tell me.
- Do not send, schedule or publish anything.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"draft-weekly-newsletter-from-reading-list","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.