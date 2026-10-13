---
name: track-new-papers-or-releases-in-a-field-daily
description: "Track new papers and releases in your field with a daily agent digest. Each weekday you get one message with the few new papers and releases that match your interests, each with a link, a one-line reason it matters, and a clear note when nothing new appeared. "
---

# Track new papers and releases in your field with a daily agent digest

Source: https://agentshandbook.com/p/track-new-papers-or-releases-in-a-field-daily (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/track-new-papers-or-releases-in-a-field-daily.md

Set up a scheduled job that pulls new arXiv papers in your categories and new releases from the GitHub repositories you follow, has a model score each item against a written description of your interests, and sends you a short digest with links. Build it in n8n, as a Claude Code routine, or with an open-source GitHub Actions project. The common problems are silent: runs that succeed but send nothing, rate limits from the arXiv API, summaries that quietly fall back to the abstract, and schedules in the wrong time zone. Add a heartbeat and check the first week by hand.

## Stop and ask the user

- Approve the interest description, sources and recipient before the schedule goes live.
- Read the first week of digests next to the raw feed to check what it missed.
- Approve any change that sends the digest to anyone other than you.

## Steps

1. **Write your interest description.** Three to six sentences on topics, methods and things to skip. Add five recent papers you would have wanted, as examples. Check: Someone else could read it and pick the same papers you would.
2. **Choose sources and limits.** Pick arXiv categories and the GitHub repos to watch. Set a cap on items per day so the digest stays short. Check: You have a list of categories, repos, and a daily cap.
3. **Build the workflow.** Use the n8n outline, a Claude Code routine, or fork an open-source digest project. Store sent IDs so the same paper never arrives twice. Check: A manual run fetches items and stores their IDs.
4. **Make failures loud.** Send a message every run, with counts, even when nothing qualifies. Put errors at the top. Users of one open-source digest project report runs that succeed in the log but never send email. Check: A run with no new items still sends a message that says so.
5. **Fix the time zone and schedule.** Set the time zone explicitly and avoid weekends for arXiv. Pick a few minutes past the hour so it does not queue with other jobs. Check: The first scheduled run arrives at the local time you expect.
6. **Compare a week of digests against the raw feed.** For five days, skim the full category listing and note good papers the digest missed or bad ones it kept. Adjust the interest text and threshold. Check: Misses and false hits drop after your adjustments.
7. **Ask before sharing it wider.** If you want to send it to a team channel or list, run it to yourself for two weeks first, then approve the change yourself. Check: The recipient list is only what you approved.

## Known failures

- The run shows success, but no digest arrives. Fix: Send a heartbeat message every run and check the job log. In one digest project, a date-sorting bug meant scheduled runs never sent mail, and the run history looked normal.

- The arXiv API returns HTTP 429 Too Many Requests. Fix: Wait at least three seconds between requests, use one connection, and move the run off the busy hour. Users of a shared GitHub Actions project report 429 errors even after updates.

- The summary is just the abstract copied in, because the model call failed quietly. Fix: Make the job write "summary failed" instead of falling back to the abstract, and check your API key and model name in the logs.
- The digest arrives hours late or at the wrong time. Fix: Check which time zone the scheduler uses. One user's first run arrived about ten hours late because the schedule was in UTC.
- Weekend and holiday runs are empty. Fix: Schedule weekdays only for arXiv, as one n8n template does, or say "no new papers today" so you know it ran.
- Relevance drops after an update or over time. Fix: Re-read the interest description, add example papers, and compare against the raw feed again. Pin the version of any forked project.
- A cloud routine can write to every connected tool. Fix: Remove connectors the job does not need, and send only to yourself until you trust it.

## Starting prompt

```text
Build a daily research digest for me. Ask me before you send anything to anyone except [my email or my Slack DM].

Interests (score papers against this): [three to six sentences on what I work on, methods I care about, and what I do NOT want, for example "skip benchmark-only papers"].
Sources:
- arXiv categories: [cs.CL, cs.LG]. Use the arXiv API, newest first by submittedDate, and only items from the last [24] hours. Wait at least three seconds between requests.
- GitHub releases from: [owner/repo, owner/repo].
Schedule: weekdays at [08:10] in [Europe/Lisbon]. Say which time zone the scheduler actually uses.

For each run:
1. Fetch new items. Skip anything already sent (keep a list of sent IDs).
2. Score each item 1-10 against my interests with a one-line reason. Keep items scoring [7] or more, at most [8].
3. For each kept paper: title, authors, link to the arXiv abstract page, and a two-sentence summary written from the abstract. If summarising fails, say "summary failed", do not paste the abstract as if it were a summary.
4. For each release: repo, version, date, and the two most important changes from the release notes.
5. Always send a message, even when nothing qualifies, with counts: fetched, scored, kept, errors.
6. If any step fails, put the error at the top of the message.

Before going live, run it once by hand and show me the message. Do not post to any shared channel.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"track-new-papers-or-releases-in-a-field-daily","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.