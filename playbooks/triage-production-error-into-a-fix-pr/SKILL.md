---
name: triage-production-error-into-a-fix-pr
description: "Triage a production error from Sentry or logs into a tested fix pull request. You get a short root cause note backed by the stack trace and code, a failing test that reproduces the error, a small fix that makes it pass, and a local branch ready for your review. "
---

# Triage a production error from Sentry or logs into a tested fix pull request

Source: https://agentshandbook.com/p/triage-production-error-into-a-fix-pr (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/triage-production-error-into-a-fix-pr.md

Give a coding agent the exact error: a Sentry issue ID through the Sentry MCP server, or a pasted stack trace, the release, and the relevant log lines. Ask it to explain the root cause from the code first, without editing. Then it writes a test that reproduces the error, makes the smallest fix, and stops before it pushes. Agents miss causes that sit in another service or in infrastructure, so ask for the evidence behind each claim and check whether the error is a code bug at all.

## Stop and ask the user

- Confirm the root cause note before the agent edits any code.
- Review the fix and the new test before anything is pushed or merged.
- Deploy through your usual pipeline, never from the agent session.

## Steps

1. **Collect the exact error and its context.** Get the issue ID or stack trace, the release where it started, how often it happens, and the deploys around that time. Remove tokens and personal data from any logs you paste. Check: You have one specific error, not a vague bug report.
2. **Connect the error source to the agent.** Add the Sentry MCP server scoped to the project, or paste the trace and logs. If the issue payload lacks package versions or the suspect commit, paste them yourself. Check: The agent can print the stack trace and the latest event for the issue.
3. **Ask for a root cause, read only.** Use plan mode or a read-only sandbox. Ask for the file and line, the cause, the evidence, and a statement of whether this is a code bug at all. Check: The note quotes real code lines and event data, and names what it could not see.
4. **Challenge the diagnosis.** Ask what would prove it wrong. Check one claim yourself in the code or the event. If the error starts in another service, give the agent that repository or the connected trace. Check: You agree with the cause and can explain it to a teammate.
5. **Reproduce with a failing test.** Let the agent write a test that fails for the reason in the note. Run it yourself once. Check: The new test fails on the current code with the same error message as production.
6. **Make the smallest fix and run the suite.** Ask for the minimal change. Reject fixes that swallow the exception or add a broad null check without a reason. Check: The new test passes, the full suite passes, and the diff is small.
7. **Push and deploy through your normal process.** You push the branch, open the pull request, and deploy through CI. After the deploy, watch the Sentry issue for new events on the new release. Check: The issue gets no new events on the fixed release.

## Known failures

- The agent blames the code for an error that comes from infrastructure, such as restarts or timeouts. Fix: Ask it to classify the error before it fixes anything, and give it the deploy and uptime history for the same window. Phase 1 of the prompt makes it stop when the error is not a code bug.

- The cause is in another service, so the agent fixes the wrong place. Fix: Give it the trace across services and access to the other repository. Sentry's own team reports that its agent could not diagnose a front-end 500 error whose cause was in the back end until it got trace data.

- The agent cannot map the error to the right code, especially across many repositories. Fix: Tell it the repository and release. One Sentry MCP user reports that the agent had to search the whole organisation's code to find the source, which was unreliable.

- The fix hides the error instead of fixing it, or a test is changed to match the bug. Fix: Require a failing test that reproduces the production error and review the test diff before the code diff.
- The agent reads the code on main, but production runs an older release. Fix: Give it the release tag or SHA and ask it to read the code at that commit.

## Starting prompt

```text
Investigate this production error. Do not edit any file until I approve your root cause.

Error: [Sentry issue ID, for example PROJ-123, or paste the stack trace]
First seen / release: [release tag or commit SHA]
Frequency and who is affected: [e.g. 400 events in 24h, only on /checkout, only iOS]
Recent changes: [link or list of deploys and merged PRs since the error started]
Logs: [paste the 20-50 log lines around one occurrence, with secrets removed]

Phase 1, read only:
1. Read the stack trace and find the exact file and line in this repo. Check out the code at the release where the error started, not just main.
2. Explain the root cause in three sentences or fewer. Quote the code lines and the event data that prove it.
3. Say whether this is a code bug, bad input, a dependency or config problem, or infrastructure noise (timeouts, deploy restarts, a downstream service). If it is not a code bug, stop and tell me what to check instead.
4. List what you could not see, for example package versions, the suspect commit, or a request body.
Stop here and wait for my reply.

Phase 2, after I approve:
5. Create a branch named [fix/proj-123].
6. Write a test that reproduces the error and fails.
7. Make the smallest fix that makes it pass. Do not catch and ignore the error, and do not change other tests.
8. Run [the test command] and show the output.
9. Commit on the branch. Do not push, open a pull request, deploy, or touch production data. Show me the diff.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"triage-production-error-into-a-fix-pr","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.