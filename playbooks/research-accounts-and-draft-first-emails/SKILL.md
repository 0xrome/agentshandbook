---
name: research-accounts-and-draft-first-emails
description: "Research a list of target accounts and draft first emails for you to review and send. You get a table of researched accounts with a fit score, sources and one draft email each, and nothing is sent until you approve it."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/research-accounts-and-draft-first-emails
  version: "2026-10-13"
---

# Research a list of target accounts and draft first emails for you to review and send

Source: https://agentshandbook.com/p/research-accounts-and-draft-first-emails (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/research-accounts-and-draft-first-emails.md

Give an agent your ideal customer profile and a short list of accounts. It researches each one, scores the fit, cites where every fact came from, and writes a short first email into a review sheet or your drafts folder. You read, fix and send each email yourself. Public accounts show the research saves time, but unchecked emails read as generic, contain wrong details, and hurt your sending domain when they go out in bulk.

## Stop and ask the user

- Approve the account list and the ideal customer profile before the agent researches anyone.
- Check every personal fact in a draft against its cited source before you send it.
- Send each email yourself. The agent only writes drafts.
- Confirm each email has your real name, postal address and a clear way to opt out.

## Steps

1. **Write the profile and fact sheet.** Write your ideal customer profile and a short list of true claims about your product with links. The agent may only use these claims. This stops it from inventing features, prices or customers. Check: You have one page you would be happy for a buyer to read.
2. **Pick a small batch of accounts.** Start with 20 or fewer accounts you already believe fit. Anthropic's BDR describes researching accounts against curated ICP criteria, with a person approving every send. Check: A list of company names and domains, no guessed email addresses.
3. **Run the prompt and stop at five.** Paste the prompt. The agent researches five accounts and stops. Read every row. Check: Each row has a fit score, a reason and a source URL for the hook fact.
4. **Check the facts and the tone.** Open each source URL and confirm the fact. Ask yourself if the email would still make sense sent to a thousand other companies. If yes, it is generic. Tell the agent what to change and let it finish the batch. Check: Every hook fact matches its source, and no two emails open the same way.
5. **Verify addresses yourself.** Get addresses from a verification tool or the person's public page. One author who let an agent guess address formats said it was not a reliable way to build a list. Another sent mail to invalid addresses because he skipped screening. Check: Every address is verified or removed.
6. **Send by hand in small batches.** Copy each approved draft into your mail client and send it yourself. Keep volume low on a new domain. Watch replies and spam complaints for the first days before you send more. Check: You sent only emails you read in full, and each one has your address and an opt-out line.

## Known failures

- The emails read as generic. The hook fact would fit any company, so the buyer ignores it. Fix: Require one specific fact tied to a problem your offer solves, with a source. Reject drafts that would still make sense for another account.

- The agent picks a shallow detail and pitches a product that does not fit the reader. Fix: Make the agent score fit first and write nothing for low-fit accounts. In one public case, a blogger got an AI email that named his web framework but pitched a CMS he had no use for.

- The agent states facts that are wrong or invents details about the prospect or your product. Fix: Allow only facts with a source URL, and only product claims from your fact sheet. Check each hook fact yourself. TechCrunch reported customers of one AI SDR product who described hallucinations and manual correction.

- Emails go to invalid addresses or land in spam, and the domain's reputation drops. Fix: Never let the agent guess addresses. Verify them, send in small batches, and set up SPF and DKIM. Google says to keep the spam rate in Postmaster Tools below 0.3%.

- The setup drifts into auto-send because sending looks faster. Fix: Keep send tools out of the agent's reach. The account that auto-sent about 970 emails reports spam placement, flagged volume and recipients asking how he got their address.


## Starting prompt

```text
You are my research assistant for outbound sales. You research and draft. You never send.

My company: [company name], which sells [one-line offer] to [who buys it].
Ideal customer profile: [industry, company size, region, buyer role, signals such as hiring for X or using Y].
Accounts to research: [paste a list of company names and domains, max 20 per batch].
My sender details for the footer: [your name, company, postal address, how to opt out].

For each account:
1. Read the company's own website and up to two recent public sources (news, a blog post, a job post). Do not use more than one source that you could not open.
2. Score the fit from 1 to 5 against my profile. Give one sentence of reasons. If the fit is 1 or 2, stop and write no email.
3. Name the most likely buyer role. Only name a person if a public page lists them in that role today. Do not guess email addresses.
4. Write one first email of under 120 words. Use exactly one specific fact about the account that ties to a problem my offer solves. Put the source URL for that fact in a separate column. Do not use flattery, fake familiarity ("loved your post"), or claims about my product that are not in [link to product page or facts doc].
5. Add the footer with my sender details.

Output a table with columns: company, domain, fit score, reason, buyer role, person (or blank), hook fact, source URL, subject line, email body, confidence (high, medium, low).

Rules:
- If you cannot verify a fact, leave it out. Never fill a gap with a guess.
- Do not reuse the same opening line across accounts.
- STOP after the first 5 accounts and show me the table. Wait for my feedback before you do the rest.
- Never send, schedule or queue any email. If a tool offers to send, do not use it.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"research-accounts-and-draft-first-emails","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
