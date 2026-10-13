---
name: map-an-unfamiliar-codebase-before-you-change-it
description: "Map an unfamiliar codebase into a checked architecture document before you change it. You have a docs/architecture.md that names the entry points, modules and data flow with file references, a list of open questions, and a short instruction file with the build and test commands. "
---

# Map an unfamiliar codebase into a checked architecture document before you change it

Source: https://agentshandbook.com/p/map-an-unfamiliar-codebase-before-you-change-it (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/map-an-unfamiliar-codebase-before-you-change-it.md

Open the repository in a coding agent in read-only or plan mode and ask for an architecture map: entry points, modules, data flow, key data models, how to build and test, and open questions. Make it cite a file and line for every claim and mark what it guessed. Then check the map yourself by tracing one real request through the code. Keep the long map in docs for people, and keep the agent's instruction file short, because a study found that repository overviews in those files do not help agents.

## Stop and ask the user

- Check at least one traced flow in the map against the running code before you rely on it.
- Review the map and any instruction file before they are committed.

## Steps

1. **Write down your goal.** Name the change or review you need to make. A map aimed at one goal is shorter and more accurate than a tour of everything. Check: You have one sentence that names the area and the task.
2. **Start the agent in read-only mode.** Use Claude Code plan mode (claude --permission-mode plan), the Codex read-only sandbox, Gemini CLI /plan, or Cursor Plan mode, so nothing changes while it explores. Check: The agent reads files and answers, and asks before any edit.
3. **Get the build and test commands working first.** Ask the agent to find and run the test command. If setup fails, fix it with a human who knows the stack. One writer found AI help could not replace a documented setup for a legacy Java project. Check: The test suite runs on your machine, or you know exactly why it does not.
4. **Ask for the map with file references.** Paste the prompt. Insist on file:line for each claim and a [GUESS] tag for anything inferred. Check: Every section has file references, and guesses are tagged.
5. **Trace one request yourself.** Pick the traced request and follow it with a debugger, log lines or a breakpoint. Correct the map where it is wrong. This is the step that turns a plausible map into a correct one. Check: You followed one real request through the code and it matches the map, or you fixed the map.
6. **Answer the open questions.** Ask a maintainer, read the tests, or run the code for each open question. Delete [GUESS] tags only when you confirm them. Check: The open questions list is short and each one has an owner.
7. **Keep the agent instruction file short.** Put the long map in docs/architecture.md for people. In CLAUDE.md or AGENTS.md keep only build and test commands and rules the agent would not guess. A 2026 study found repository overviews in these files did not raise agent success and added cost. Check: The instruction file has commands and non-obvious rules, not a copy of the map.
8. **Commit the docs yourself.** Review the diff, then commit. Note the commit SHA and date in the map so readers know when it was checked. Check: The map is in the repo with a date and the SHA it describes.

## Known failures

- The map is confident but wrong about configuration, dependencies or how modules connect. Fix: Require file:line references and [GUESS] tags, and trace one flow yourself. An OpenWrt package maintainer warns that DeepWiki pages for their packages had wrong config descriptions and misleading architecture details.

- The generated docs go stale when the code changes. Fix: Date the map, record the commit SHA, and regenerate or review it when the area changes. Two DeepWiki users report that generated pages do not update when the repository changes.

- The agent finds the right area but not the exact files, or misses dependencies outside the repo. Fix: Give it the related repositories and ask for the dependency list. Check with a plain text search for key names.
- The agent writes a long CLAUDE.md or AGENTS.md overview that it then ignores, and every session costs more. Fix: Keep overviews in docs for people. Keep the instruction file under about 200 lines with commands and non-obvious rules.
- Setup instructions from the agent are generic and do not work. Fix: Ask it to run each command and report the real output. Fix setup with someone who knows the stack.

## Starting prompt

```text
I am new to this repository. Help me understand it. Do not change any code.

Goal: I need to [fix bug X / add feature Y / review this service] in [area of the code].

1. Explore the repo. Start with the README, build files, [package.json / pyproject.toml / go.mod], the entry points and the test setup. Use subagents for broad searches if you can.
2. Write docs/architecture.md with these sections:
   - What the system does, in five sentences or fewer.
   - How to install, build, run and test it, with the exact commands. Run the test command once and report whether it works.
   - Entry points: each one with its file path.
   - Modules: a table of directory, purpose, key files, and what it depends on.
   - Data flow: trace one real request for [e.g. POST /orders] from the entry point to the database and back, step by step, with file:line for each step.
   - Key data models and where they are defined.
   - Conventions a newcomer would not guess: naming, error handling, generated code, feature flags.
   - Glossary of project terms.
   - Open questions: things you could not confirm.
3. Every claim needs a file:line reference. Mark anything you inferred without reading the code as [GUESS].
4. Do not write anything except docs/architecture.md. Do not overwrite an existing CLAUDE.md, AGENTS.md or README. Do not commit.

When you finish, list the five files I should read first for my goal, and stop.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"map-an-unfamiliar-codebase-before-you-change-it","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.