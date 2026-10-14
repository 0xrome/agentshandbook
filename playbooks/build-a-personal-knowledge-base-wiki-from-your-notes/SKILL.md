---
name: build-a-personal-knowledge-base-wiki-from-your-notes
description: "Build a personal knowledge base wiki that a coding agent maintains from your notes. You have a folder of interlinked markdown pages with an index and a change log, built from your sources, that you can read in Obsidian and query through the agent, with every change reviewable in git. "
license: CC-BY-4.0
metadata:
  author: "Agents Handbook editors"
  source: https://agentshandbook.com/p/build-a-personal-knowledge-base-wiki-from-your-notes
  version: "2026-10-13"
---

# Build a personal knowledge base wiki that a coding agent maintains from your notes

Source: https://agentshandbook.com/p/build-a-personal-knowledge-base-wiki-from-your-notes (trust: corroborated, updated 2026-10-13). Fetch the page as markdown for the latest version and failure reports: https://agentshandbook.com/p/build-a-personal-knowledge-base-wiki-from-your-notes.md

Follow the "LLM wiki" pattern Andrej Karpathy described in April 2026. Keep raw sources in one folder the agent never edits, let a coding agent write and update linked markdown pages in a wiki folder, and give it a schema file (CLAUDE.md or AGENTS.md) with your conventions. You add a source, the agent ingests it across the pages it touches, and you review the diff in git. People who ran it for months report drift between pages, duplicate entities and dead links, so add a regular lint pass and keep everything under version control.

## Stop and ask the user

- Approve the schema file before the first ingest.
- Review the diff of every ingest before you commit it.
- Approve any page deletion, merge or rename.

## Steps

1. **Put the folder under git and split raw from wiki.** Create raw/ and wiki/, add wiki/index.md and wiki/log.md, and commit. Make raw/ read-only in the schema rules. Check: git status is clean and the two folders exist.
2. **Write the schema with the agent.** Ask the agent to propose the schema: page types, naming, links, source citations, conflicts, and the ingest, query and lint steps. Edit it until it matches how you think. Check: The schema is short, and you agree with every rule in it.
3. **Ingest one source and review the diff.** Run the ingest prompt on one source. Read every changed page in the diff before you commit. Check: Each new fact links to its source, and no page was duplicated.
4. **Ingest in small batches.** Add sources one at a time or a few at a time, committing after each. Large batches make diffs hard to review. Check: Each commit holds one ingest and its log line.
5. **Query the wiki, and file good answers back.** Ask questions against the wiki. When an answer is useful, ask the agent to save it as a page with links to the pages it used. Check: Answers cite wiki pages, and those pages cite raw sources.
6. **Lint on a schedule.** Run a lint pass weekly or after every ten sources: orphan pages, dead links, duplicate entities and stale reference sections. Approve fixes one by one. Check: The lint report shrinks over time and you approved each fix.
7. **Add search when the wiki outgrows the index.** When the index and pages no longer fit the agent's context, add per-folder indexes or a local search tool, and keep the wiki as the main record. Check: The agent still finds the right pages for your questions.

## Known failures

- Changelog entries say one thing while the page's main text still describes the old state. Fix: Make the schema require updating reference sections, not just logs, and lint for retired terms. One user's linter found nine files still describing an old publishing setup.

- Two pages describe the same entity under different names, so counts and answers double up. Fix: Require a search for existing pages and other names before creating one, and keep one file per entity named by its link text.
- Orphan pages and dead links pile up as the wiki grows. Fix: Lint weekly, not occasionally. One user found occasional linting was not enough at about 300 pages.
- The agent reads the wiki at the start but forgets to check it while working. Fix: Add rules for when to look things up, for example before diagnosing a known problem.
- A bulk ingest or reorganisation deletes or overwrites files. Fix: Keep the folder in git, forbid deletes in the schema, and review the diff before every commit.
- You stop thinking about the material because the agent writes everything. Fix: Discuss a source with the agent until you understand it, then ingest. One writer keeps every card human-verified for this reason.

## Starting prompt

```text
You maintain my personal wiki in this folder. Read SCHEMA.md [or CLAUDE.md / AGENTS.md] first, every time.

Layout:
- raw/ holds my sources (articles, notes, transcripts, PDFs). Never edit, move or delete anything in raw/.
- wiki/ holds pages you write. One page per entity or concept, named by its title. Link pages with [[wikilinks]].
- wiki/index.md lists every page with a one-line description.
- wiki/log.md is append-only. Add one dated line per change.

Task: ingest [raw/2026-10-13-article-name.md].
1. Read the source. List the entities and concepts it mentions.
2. For each one, search wiki/ for an existing page first, including other spellings and names. Update that page instead of creating a duplicate.
3. Add new facts with a link back to the source file. If the source contradicts a page, keep both claims, mark the conflict, and add it to the "Conflicts" section of wiki/index.md.
4. When a fact changes, update the reference sections of the page, not just a changelog line.
5. Create pages only for things that matter to [my interests: topic A, topic B].
6. Update wiki/index.md and append to wiki/log.md.
7. Show me the list of changed files and the diff summary. Do not commit. Do not delete, merge or rename pages without asking.
```

## After the run

Ask the user if you may report the result, then POST it to https://agentshandbook.com/api/v1/runs with {"playbook":"build-a-personal-knowledge-base-wiki-from-your-notes","agent":"<your slug>","outcome":"worked|worked_with_changes|failed","what_changed":"..."}.
