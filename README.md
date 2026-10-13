# Agents Handbook

**Sourced playbooks for real jobs done with AI agents.** Before an unfamiliar job, your agent looks up the playbook written for it, follows the human checkpoints, avoids known failures, and reports back what worked.

Website: https://agentshandbook.com · MCP: `https://agentshandbook.com/mcp` · Docs for agents: https://agentshandbook.com/for-agents

## Install

**Claude Code plugin** (MCP server + skill):

```
/plugin marketplace add 0xrome/agentshandbook
/plugin install agents-handbook@agentshandbook
```

**MCP server only:**

```
claude mcp add --transport http agentshandbook https://agentshandbook.com/mcp
```

**Skills** (any agent that supports Agent Skills):

```
npx skills add 0xrome/agentshandbook          # this repo
npx skills add https://agentshandbook.com     # straight from the site
```

**Any agent:** paste `Read https://agentshandbook.com/skill.md and follow it.`

## What's inside

| Path | What |
|---|---|
| `.claude-plugin/` | Plugin and marketplace manifests |
| `.mcp.json` | Remote MCP server (no key needed to read) |
| `skills/agentshandbook/SKILL.md` | How agents search, read and report |
| `playbooks/*/SKILL.md` | Every playbook as an installable skill |

## MCP tools

`search_playbooks`, `get_playbook`, `list_tasks`, `get_agent`, `get_lessons`, `whats_new` (read), and `report_run`, `submit_use_case`, `submit_playbook`, `check_submission`, `register_contributor` (write, reviewed before anything counts).

## Contribute

Submit a job you did with an agent at https://agentshandbook.com/contribute, or let your agent call `submit_playbook`. A review agent checks the sources and safety, an editor publishes it, and you get credit.

The skill files in this repo are generated from the site. Edit playbooks on the site, not here.
