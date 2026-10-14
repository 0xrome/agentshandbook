---
name: upgrade-a-framework-across-a-repo-with-tests-as-the-gate
description: "Upgrade a framework across a repo with a coding agent and the test suite as the gate. The repo runs on the new version on a branch of small commits, the full test suite passes with no tests removed, and you have a list of behaviour changes to check in staging. "
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/upgrade-a-framework-across-a-repo-with-tests-as-the-gate
  version: "2026-10-13"
---

# Upgrade a framework across a repo with a coding agent and the test suite as the gate

Source: https://agentshandbook.com/p/upgrade-a-framework-across-a-repo-with-tests-as-the-gate (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/upgrade-a-framework-across-a-repo-with-tests-as-the-gate.md

Run the official codemod first, then let a coding agent work through the failing tests one at a time with small commits. Turn deprecation warnings into errors so the agent gets a concrete list. Go one major version at a time. Forbid it to change settings defaults, migrations or tests without asking, because the reported failures come from quiet config changes, outdated API knowledge and broken behaviour that tests do not cover. You push and deploy, not the agent.

## Stop and ask the user

- Approve the upgrade plan and the order of version steps before any code changes.
- Approve every change to settings defaults, database migrations, dependency versions or existing tests.
- Review the branch and deploy it to staging yourself before production.

## Steps

1. **Get the current version green.** Fix or quarantine flaky tests before you start. Record the test count and runtime. Check: The suite passes twice in a row on the current version, and you know the test count.
2. **Plan from the official docs.** Ask the agent to read the upgrade guides and list breaking changes with file references and packages to bump. Spot-check the package list against each package's changelog. Check: You have a step plan, one major version at a time, and you checked a sample of the package claims.
3. **Run the codemod and commit it alone.** Run the framework's codemod, for example `npx @next/codemod upgrade [version]` for Next.js or django-upgrade for Django. Use a dry run first where it exists (`--dry` for Next.js codemods). Check: One commit holds only codemod output, and the build still starts.
4. **Make deprecations fail loudly.** Run the tests with deprecation warnings as errors so the agent works from a list instead of guesses. Check: You see a concrete list of failing tests.
5. **Fix one failing test per commit.** Let the agent take the first failing test, make the smallest fix and commit. Small commits make review and rollback easy. Watch for edits to test files. Check: Each commit is small, names the test it fixes, and touches no test assertions.
6. **Stop at every settings, migration or dependency decision.** When the new version changes a default, keep the old value explicitly unless you decide otherwise. Check settings that come from environment variables, not just the base file. Check: Every changed default is a decision you made and wrote down.
7. **Compare the test count and run the full suite.** Confirm the number of tests is the same or higher than at the start, and that nothing is newly skipped. Check: Same or more tests, all passing, no new skips.
8. **Deploy to staging and check behaviour.** You push the branch and deploy it to staging. Click through login, forms and pages that tests do not cover. Fix what breaks with the same one-fix-per-commit loop. Check: Staging works on the flows in your behaviour checklist.

## Known failures

- The agent changes a settings default to match the new version, which silently changes behaviour. Fix: Forbid default changes without approval. In one Django upgrade, the agent proposed turning on time zone support, which the author says would have reinterpreted stored times, so he pinned the old value.

- Tests pass but staging breaks, because the fix only covered the base config. Fix: Ask the agent to search every settings file and environment variable for the changed setting. Add a boot-time check. The same Django author hit this with a login setting.

- The agent writes code for the old API or invents a migration path. Fix: Give it the upgrade guide and changelog, or a docs MCP server, and run the type checker after each change.
- The agent skips a required upgrade command, such as a framework's config update step. Fix: Put each command as an explicit step in the prompt or skill. One user of a Rails upgrade skill reports the agent skipped bin/rails app:update several times because it was only mentioned in report text.

- The agent deletes or loosens tests to get to green. Fix: Compare the test count before and after, review every test file diff, and forbid test edits without approval.
- Each change is fine on its own, but the code becomes a mess across many sessions. Fix: Set the target structure up front and write the decisions into CLAUDE.md or AGENTS.md. One team reports a template that grew past 1,100 lines during a migration before they reset the design.

- Package compatibility claims are wrong. Fix: Check each package's own changelog. The Django author found two errors in a third of the agent's package table that he checked, caused by stale metadata.

## Starting prompt

```text
We are upgrading [framework] from [current version] to [target version] in this repo. You are the hands; I make the risky decisions.

Before you edit anything:
1. Read the official upgrade guide and changelog for each version between [current] and [target]: [link to upgrade guide]. Do not rely on memory for APIs that changed after your training data. If you cannot open the docs, tell me.
2. List the breaking changes that affect this repo, with file references, and the third-party packages that need a new version. Mark any package compatibility you could not confirm from its own changelog.
3. Propose the order of steps. Go one major version at a time. Wait for my approval.

Then, for each step:
4. Create a branch [upgrade/framework-N]. Run the official codemod: [command, for example `npx @next/codemod upgrade 16` or `git ls-files -z -- "*.py" | xargs -0 django-upgrade --target-version 5.2`]. Commit its output alone.
5. Run [test command] with deprecation warnings as errors: [for example `python -W error::DeprecationWarning -m pytest`].
6. Loop: take the first failing test, make the smallest fix, run that test and the related tests, commit with a message that names the test. Then the next one.

Rules:
- Never delete, skip or loosen a test or an assertion to make it pass. If a test looks wrong, stop and ask.
- Ask before you change a settings default, a database migration, a lockfile entry outside this upgrade, or CI config.
- Do not refactor or modernise code that is not broken. Note it in a follow-up list instead.
- Do not push, merge or deploy.

At the end, give me: the commits, the full test result, the list of behaviour changes I must check in staging, and the follow-up list.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"upgrade-a-framework-across-a-repo-with-tests-as-the-gate","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
