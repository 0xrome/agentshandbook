---
name: turn-issues-into-pull-requests-with-cloud-agents
description: "Turn small tracker issues into reviewed pull requests with cloud coding agents. Each chosen issue gets a pull request with a passing test run that you review, ask to change, merge or close. You stay in control of every merge. "
---

# Turn small tracker issues into reviewed pull requests with cloud coding agents

Source: https://agentshandbook.com/p/turn-issues-into-pull-requests-with-cloud-agents (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/turn-issues-into-pull-requests-with-cloud-agents.md

Pick small, well-described issues, write them like a spec with a repro and a test command, and assign them to a cloud agent such as GitHub Copilot's cloud agent, Claude Code in GitHub Actions, Codex cloud, Jules, Cursor or Devin. The agent works on a branch and opens a pull request. You review it like a junior colleague's work and merge it yourself. Teams that report good results put build and test instructions in an AGENTS.md or CLAUDE.md file first and kept tasks small.

## Stop and ask the user

- Choose which issues go to the agent and rewrite them with a repro, expected behaviour and a test command.
- Read any change to CI or workflow files before you approve the workflow run.
- Review and merge every pull request yourself. Close the ones that are not worth finishing.

## Steps

1. **Make the repo buildable by an agent.** Write an AGENTS.md or CLAUDE.md with the exact install, build, test and lint commands and the rules the agent must follow. Make sure the agent's cloud environment can download packages. The .NET team reports that early failures came from an agent that could not reach packages or build the repo. Check: A fresh agent session can install dependencies and run the test suite without your help.
2. **Pick small, well-scoped issues.** Start with bug fixes that have a repro, test additions, cleanup and small refactors. Avoid performance work, design decisions and platform code the agent cannot build in its Linux runner. Check: You have three to five issues that each name the files involved and a test command.
3. **Rewrite each issue as a spec.** Use the template in the prompt. Put new information in the issue before you assign it, because some agents do not see later issue comments. Check: Each issue has a repro, expected behaviour, scope limits and a definition of done.
4. **Assign the issue to the agent.** Assign it in the tracker (Copilot takes issues from GitHub and Linear, and Cursor takes them from Linear), mention @claude, or paste it into Codex cloud or Jules. Start with one or two issues, not ten. Check: The agent acknowledges the task and starts a session or a branch.
5. **Check the pull request before CI runs.** Open the diff. If it touches workflow files, lockfiles or anything outside the scope, stop here. Then approve the workflow run if your agent needs that. Check: The diff stays inside the files you named, and CI runs on the branch.
6. **Review it like a new teammate's work.** Check that the new test fails without the change, that no test was deleted or loosened, and that the agent reused existing helpers instead of writing a copy. Ask for changes in a pull request comment. Check: You can explain why the change is correct, and the test output in the description matches CI.
7. **Merge, fix by hand, or close.** Merge good pull requests yourself. If a pull request is close, push the last fix yourself. The .NET team reports a much higher merge rate when humans pushed commits to agent pull requests. Close the rest with a note on what the agent missed. Check: Every agent pull request is merged or closed within a few days, and none sit open.
8. **Feed lessons back into the instructions file.** Add each repeated mistake as a rule in AGENTS.md or CLAUDE.md, such as "reuse toReadableText for labels" or "never edit generated files". Check: The next pull requests stop repeating the same mistake.

## Known failures

- The agent cannot build or test the repo in its cloud environment, so it guesses. Fix: Write the setup commands into AGENTS.md or CLAUDE.md and allow the package registries it needs. Do not review a pull request whose description has no test output.

- Pull requests arrive faster than anyone can review them. Fix: Limit how many issues are assigned at once and set a rule to close stale agent pull requests.
- The agent writes a new helper that duplicates an existing one. Fix: Tell it to search for similar functions first and name the module to reuse. In Birgitta Boeckeler's test, four of six agent runs duplicated logic that already existed.

- The agent changes or weakens tests so that they pass. Fix: Require a new failing test and forbid edits to existing assertions without a reason in the PR description. Check the test diff first.
- The agent keeps working on a task that cannot be done instead of saying it is blocked. Fix: Give it a time or turn limit and ask it to report blockers. Close the task and rewrite it smaller.
- The agent does not see review comments or issue updates you add later. Fix: Put new information in a pull request comment that mentions the agent, or paste it into the agent's chat.

## Starting prompt

```text
Paste this into the issue body, or into the optional prompt field when you assign the agent.

## Task
[One sentence: what should change and why.]

## Repro
[Steps, input, or a failing test name. Example: run `npm test -- src/date.test.ts`, the test "formats ISO dates" fails.]

## Expected behaviour
[What correct looks like. Include an example input and output.]

## Scope
- Files that are likely involved: [src/date.ts, src/date.test.ts].
- Do not change: [public API signatures, database migrations, .github/workflows/, lockfiles unless the task needs it].
- Keep the change under about [50] lines if you can. If it needs more, stop and explain why in the PR description.

## Definition of done
- Add or update a test that fails before your change and passes after it. Do not delete, skip or weaken existing tests.
- Run [npm test && npm run lint && npm run typecheck] and paste the result in the PR description.
- In the PR description, list what you changed, what you did not do, and anything you are unsure about.
- Open the pull request for review. Do not merge it. Do not push to [main].
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"turn-issues-into-pull-requests-with-cloud-agents","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.