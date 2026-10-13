---
name: turn-meeting-transcripts-into-tracker-tasks
description: "Turn meeting transcripts into tasks in your tracker, with a quote behind each one. Every real commitment from the meeting is a task in your tracker with the right owner, a due date and a quote from the transcript, and nothing is invented or duplicated."
---

# Turn meeting transcripts into tasks in your tracker, with a quote behind each one

Source: https://agentshandbook.com/p/turn-meeting-transcripts-into-tracker-tasks (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/turn-meeting-transcripts-into-tracker-tasks.md

Point an agent at the raw transcript from Granola, Otter, Fireflies or Zoom, not at the AI summary. Ask it for action items, each with an owner, a due date and the exact words that created it. Have it check your tracker for duplicates, show you a preview table, and create tasks in Linear, Asana, Jira or Notion only after you approve. A public test found that extracting from a summary drops items and invents owners.

## Stop and ask the user

- Approve the preview table before the agent creates any task.
- Confirm every task where the owner or the due date was not said out loud.
- Approve any change to an existing task. The default prompt never edits or closes tasks.

## Steps

1. **Make sure you can reach the raw transcript.** Connect your meeting tool. Check that the agent reads the full transcript, not only the summary. Granola's docs say transcript access through MCP is on paid plans only. Check: The agent can quote a sentence from the middle of the meeting with its timestamp.
2. **Write the owner table.** List each regular attendee with the email or user ID they use in the tracker. Add it to the prompt. Check: Every name from your last meeting maps to one tracker user.
3. **Run the extraction and read the preview.** Paste the prompt. Read every row. Compare it with what you remember, and look for conditional promises and small items, which tests show are the first to go missing. Check: Every row has a quote, and you cannot think of a commitment that is missing.
4. **Fix owners and dates.** Change any owner the agent guessed. Remove items that are discussion, not commitments. Mark which rows to create. Check: No row is UNMAPPED or has an owner nobody named.
5. **Approve and create.** Reply with the approved rows. The agent creates one task per row with the quote in the description. Check: The tracker shows the new tasks in the right project with the [from-meeting] label.
6. **Send follow-ups yourself.** Tell owners about their tasks in your own words, or let the tracker notify them. Check: Each owner has acknowledged their task.

## Known failures

- The agent works from the meeting summary and drops items, especially conditional promises, small items and specific numbers. Fix: Always extract from the raw transcript. In a public test, asking the model to keep commitments word for word also raised recall.
- The agent assigns a task to the wrong person, or invents an owner nobody named. Fix: Require a quote per task and write UNASSIGNED when nobody took it. Map names with a fixed table.
- All action items land in one task, or tasks go to the wrong workspace or project. Fix: Loop over items so each becomes its own task, and name the exact project, not only the workspace.
- Meeting display names do not match tracker accounts, so tasks are unassigned or assigned to the wrong account. Fix: Keep a name-to-user table in the prompt and have the agent mark unknown names as UNMAPPED.
- The same task gets created twice across meetings. Fix: Search the tracker for similar open tasks before creating, and show possible duplicates in the preview.
- A one-shot pipeline creates tasks with no review step. Fix: Use the step-by-step mode or add an approval node. One open-source MCP server has a full-pipeline mode that skips confirmation.

## Starting prompt

```text
Turn the meeting "[meeting title]" on [date] into tasks in [Linear team / Asana project / Jira project / Notion database].

Source
- Read the full raw transcript from [Granola / Otter / Fireflies / a file at path]. Do not work from the AI summary. If you can only get a summary, stop and tell me.

1. Extract every action item: something a named person agreed to do, or something the group agreed must happen. Include conditional promises ("if X, I will do Y") and small items.
2. For each item give: task title (start with a verb), owner, due date, the exact quote from the transcript with its timestamp, and confidence (high / low).
   - Owner: only the person who said they would do it, or who was asked and agreed. If nobody owns it, write "UNASSIGNED". Never guess an owner.
   - Due date: only if someone said one. Otherwise write "none said".
3. Map owners to tracker users with this table: [Priya = priya@company.com, Marcus = marcus@company.com]. If a name is not in the table, mark it "UNMAPPED".
4. Search [the tracker] for open tasks from the last [30] days with similar titles. Mark likely duplicates and link them.
5. Show me a preview table: title, owner, due, quote, confidence, duplicate link. Then stop and wait.

After I reply "approved" (or approve a subset):
6. Create only the approved tasks in [project], one task per item, with the quote and a link to the meeting notes in the description. Add the label [from-meeting].
7. Reply with links to the created tasks and a list of anything you skipped.

Hard rules
- Never create, edit, assign, comment on or close a task before I approve the preview.
- Never invent an action item that has no quote.
- Never send messages to the owners. I will do that.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"turn-meeting-transcripts-into-tracker-tasks","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.