---
name: audit-draft-folder-and-surface-the-most-ready-post
description: "Audit your draft folder and surface the post closest to ready. You get a short list of genuinely unpublished drafts ranked by how close they are to done, with the top pick named and a brief reason why."
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/audit-draft-folder-and-surface-the-most-ready-post
  version: "2026-10-13"
---

# Audit your draft folder and surface the post closest to ready

Source: https://agentshandbook.com/p/audit-draft-folder-and-surface-the-most-ready-post (trust: reported, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/audit-draft-folder-and-surface-the-most-ready-post.md

Grant Claude Cowork access to your drafts folder and ask it to cross-check each file against your live site. The agent searches your site to confirm which drafts have not been published, then reads each unpublished file and ranks them by completeness. One blogger reports the agent worked through 46 draft files and ran 44 site searches without step-by-step prompting, then named a specific file as the most publication-ready.

## Steps

1. **Grant Cowork access to your drafts folder.** In Cowork, connect only the folder that holds your drafts. Do not grant access to your whole file system. Check: Cowork can list the files in the folder.
2. **Paste the prompt with your site URL and date range.** Replace the placeholders with your site domain and the date range you want to check, such as the last three months. Check: Cowork begins listing files in the folder.
3. **Wait for the agent to finish the cross-check.** The agent searches your site for each draft title or key phrase to confirm it has not been published. Simon Willison reports the agent ran 44 individual site searches for 46 draft files without needing any prompting between steps. Check: The agent reports how many drafts it examined, how many are already published, and which remain unpublished.
4. **Review the ranked suggestions.** Read the agent's list of unpublished drafts and its reasons for ranking each one. The top pick is the file the agent judged closest to ready. Check: You have a short list with a named top pick and a brief reason for each entry.

## Known failures

- The agent marks a draft as unpublished when it is already live, because the site search missed a match. Fix: Check the top few suggestions yourself by searching your site before acting on the list.
- The agent ranks a draft highly that is actually very rough. Fix: Open the top pick yourself before you publish. The agent estimates completeness from file size and structure, not from reading quality.

## Starting prompt

```text
Look at my drafts in [path to your drafts folder] that were started or updated within the last [three months] and check that I did not publish them on [your-site.com] using a search against content on that site. Then suggest the ones that are most close to being ready to publish, with a brief reason for each.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"audit-draft-folder-and-surface-the-most-ready-post","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
