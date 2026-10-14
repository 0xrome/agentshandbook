---
name: dispute-irs-cp2000-notice
description: "Dispute an IRS CP2000 notice and recover missed capital-loss carry-forwards. You understand what triggered the notice, have a draft disagreement letter, and know whether any capital-loss carry-forward applies to future returns."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/dispute-irs-cp2000-notice
  version: "2026-10-13"
---

# Dispute an IRS CP2000 notice and recover missed capital-loss carry-forwards

Source: https://agentshandbook.com/p/dispute-irs-cp2000-notice (trust: reported, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/dispute-irs-cp2000-notice.md

Upload your tax return and the IRS CP2000 notice to Claude or Gemini, then ask the model to identify what triggered the notice and whether the IRS calculation is correct. One technical writer blogger reports that this approach identified a missing cost basis as the root cause of a CP2000, helped produce a disagreement letter the IRS accepted, and uncovered a capital-loss carry-forward that produced a larger refund the following year. Have a licensed tax professional review every AI finding before you send anything to the IRS.

## Stop and ask the user

- Have a licensed tax professional review the AI analysis before you respond to the IRS.
- Confirm every number and form reference the AI produces against official IRS sources before including it in a filing.
- Decide yourself whether to agree or disagree with the IRS notice.
- Have a professional review any amended return before filing.

## Steps

1. **Note the response deadline before anything else.** The CP2000 notice states a deadline to respond. If fewer than two weeks remain, contact your accountant or call the IRS before continuing. Check: You know the exact deadline and have enough time to respond.
2. **Open a private AI session.** Start a new incognito or private-mode chat with Claude or Gemini. Do not use a session that saves history or stores your documents between sessions. Check: You are in a session that will not persist your documents after you close it.
3. **Upload the notice and return and ask for an analysis.** Paste the prompt. Attach the CP2000 notice, your tax return, and any 1099-B statements. Ask the model to identify the discrepancy and show its reasoning. Check: The model names the specific transactions or income items that differ between your return and the IRS notice.
4. **Ask about cost basis and carry-forwards.** If the notice involves stock sales, ask the model whether cost basis is correctly reported for every sale and whether any net capital loss can carry forward to the next year. Check: The model states any carry-forward amount with a step-by-step calculation you can verify line by line.
5. **Verify every form number on IRS.gov.** If the model cites a specific IRS form number, look it up in the IRS forms catalog before including it in any filing. AI models can hallucinate form numbers that do not exist or confuse forms with similar numbers. Check: Every form the model cited appears on IRS.gov with the correct name and purpose.
6. **Cross-check with a second model.** Repeat the upload and prompt in the other model (Claude or Gemini) and compare the answers. Note any disagreement between them. Check: Both models agree on the key findings, or you have recorded where they differ.
7. **Have a tax professional review the output.** Share the AI analysis with a CPA or enrolled agent. Ask them to confirm the root cause and review any draft disagreement letter before you send it. Check: A licensed professional has reviewed and confirmed the AI findings.
8. **Send your response before the deadline.** Mail or fax the disagreement letter with supporting documents. Keep a full copy and a mailing or fax confirmation. Check: You have proof of timely submission and a complete copy of everything you sent.
9. **File an amended return if a prior error is confirmed.** If a professional confirms an error such as a missed carry-forward, file Form 1040-X for the relevant year. Have the professional review it before filing. Check: The amended return has been reviewed and approved by a professional before submission.

## Known failures

- The AI cites an incorrect or nonexistent IRS form number. Fix: Verify every form name and number on IRS.gov before including it in any filing. The source for this playbook references a form number that does not correspond to a standard CP2000 response form, which illustrates this risk.
- The AI misreads scanned PDFs, especially tables of figures. Fix: Also paste the key numbers as plain text alongside any uploaded file so the model has clean data. Ask it to repeat the numbers back before drawing conclusions.
- The carry-forward calculation does not match your Schedule D. Fix: Ask the model to show every arithmetic step, then verify each line against your Schedule D by hand before relying on the total.
- You miss the response deadline while gathering documents or waiting for professional review. Fix: Mark the deadline the moment you open the notice. If fewer than two weeks remain, contact the IRS or an accountant before starting AI analysis.
- The AI gives confident-sounding advice that a professional later says is wrong. Fix: Treat AI output as a starting point for professional review, not a finished answer. Cross-checking Claude and Gemini against each other, as the source author did, helps surface disagreements before you commit to a position.

## Starting prompt

```text
I received an IRS CP2000 notice about my [year] tax return. I will share the notice and my return with you.

Please do the following:
1. Identify which income or transactions the IRS says I under-reported.
2. Compare that to my return and explain any difference.
3. Tell me whether the IRS calculation appears correct based on what I share.
4. If there is a discrepancy, explain what I would need to include in a written disagreement. If you cite a specific IRS form number, state it explicitly and note that I will verify it on IRS.gov before using it.
5. Check whether my capital gains and losses are complete for the year, and whether any net capital loss can carry forward to [next year]. Show every calculation step.

I will have a tax professional review your analysis before I respond to the IRS.

[Attach or paste: the CP2000 notice, your full tax return, and any brokerage 1099-B statements]
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"dispute-irs-cp2000-notice","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
