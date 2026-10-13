---
name: write-and-ab-test-landing-page-copy
description: "Write landing page copy variants with an agent and A/B test them properly. You get 3-5 copy variants tied to a written hypothesis, one live A/B test with a fixed sample size, and a result you can trust or a clear \"no difference\"."
---

# Write landing page copy variants with an agent and A/B test them properly

Source: https://agentshandbook.com/p/write-and-ab-test-landing-page-copy (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/write-and-ab-test-landing-page-copy.md

Use an assistant to write a few headline and call-to-action variants grounded in your customers' own words, then test one change at a time with a sample size you fix before the test starts. Public tests of AI-written copy show some wins, some losses and many inconclusive results. The writing is the easy part. The traps are small samples, peeking at results and changing several things at once.

## Stop and ask the user

- Approve each variant's claims against what your product really does before it goes live.
- Fix the sample size and stop rule before the test starts, and do not stop early.

## Steps

1. **Collect customer words.** Pull 10-30 quotes from reviews, calls and tickets. Copy built only from your own description of the product tends to sound generic. Check: You have real quotes, not your own summary of them.
2. **Generate variants with hypotheses.** Paste the prompt. Read each hypothesis and the claims list. Check: Each variant has a hypothesis and every claim maps to a real fact.
3. **Pick one change to test.** Test the headline first and leave layout and form alone. Two public tests of AI-made pages changed copy and layout together, so the authors could not say which change caused the result. Check: The variant differs from the control in one element only.
4. **Fix the sample size and the stop rule.** Calculate the sample size before you start and write it down. Run for at least one full week. Evan Miller shows that stopping when a result first looks significant gives many false winners. Check: You wrote the sample size and the end date before launch.
5. **Set the test up so search engines are not confused.** Follow Google's testing guidance: show Googlebot the same content as users, use rel="canonical" on variant URLs, use 302 redirects, and remove the test when it ends. Check: A variant URL points its canonical tag to the original page.
6. **Read the result at the end, not before.** When you reach the planned sample, check the result. If there is no clear difference, write that down and keep the simpler copy. In VWO's own report of 18 AI copy tests, half were inconclusive. Check: You recorded winner, loser or no difference, with the sample size.

## Known failures

- The test is called a win on a small number of visitors. Fix: Fix the sample size before launch. Crazy Egg's AI page test reported a large lift from about 300 visitors on the tested page, and the author said it could be a fluke.
- Results are checked daily and the test stops at the first significant reading. Fix: Do not peek and stop. Evan Miller's analysis shows this inflates false positives. Use a fixed sample or a sequential method built for monitoring.
- Copy and layout change together, so you cannot tell what worked. Fix: Change one element per test.
- The AI copy loses or makes no difference. Fix: Expect it. VWO reported a human-written CTA beating the AI one at Booking.com, and an agency reported no significant change from one AI headline and form test. Keep testing new hypotheses.

- The variant states wrong product details. Fix: Ask for a claims list per variant and check it. Crazy Egg's team had to fix wrong product details before launch.
- Copy is judged by a model's score or a quick read instead of real traffic. Fix: Only live traffic tells you which copy converts. HN commenters on a GPT-3 title tool pointed out the author never showed the new titles performed better.

## Starting prompt

```text
Help me write landing page copy variants for [page URL], which sells [product] to [audience].

Inputs:
- Current page copy: [paste]
- What customers say, in their own words: [paste 10-30 quotes from reviews, sales calls, support tickets or surveys]
- True product facts and proof points I can use: [list, with links]
- Primary conversion: [signup, demo request, purchase]

Do this:
1. Read the customer quotes. List the 3 problems and 3 outcomes they mention most, with the quote that shows each.
2. Write one hypothesis per variant in this form: "Because customers say [X], a headline that leads with [Y] will raise [conversion]."
3. Write [3] variants of the headline and subheadline only. Keep the rest of the page the same. Each variant tests a different hypothesis. Use the customers' words where you can.
4. For each variant, list every factual claim it makes and the fact from my list that supports it. If a claim has no support, remove it.
5. Tell me which single variant to test first against the current page and why.

Rules:
- Do not invent numbers, customer names, awards or features.
- Avoid filler words such as "best-in-class", "next-level" or "all-in-one".
- Do not change the live page. Give me the copy and STOP.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"write-and-ab-test-landing-page-copy","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.