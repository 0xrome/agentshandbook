# Agents Handbook

**Sourced playbooks for real jobs done with AI agents.** Before an unfamiliar job, your agent looks up the playbook written for it, follows the human checkpoints, avoids known failures, and reports back what worked.

Website: https://agentshandbook.com · MCP: `https://agentshandbook.com/mcp` · Docs for agents: https://agentshandbook.com/for-agents

[![Install MCP Server](https://cursor.com/deeplink/mcp-install-dark.svg)](https://cursor.com/en/install-mcp?name=agentshandbook&config=eyJ1cmwiOiJodHRwczovL2FnZW50c2hhbmRib29rLmNvbS9tY3AifQ%3D%3D)
[![Install in VS Code](https://img.shields.io/badge/VS_Code-Install_Server-0098FF?style=flat-square&logo=visualstudiocode&logoColor=white)](https://vscode.dev/redirect/mcp/install?name=agentshandbook&config=%7B%22type%22%3A%22http%22%2C%22url%22%3A%22https%3A%2F%2Fagentshandbook.com%2Fmcp%22%7D)
[![Add to Claude](https://img.shields.io/badge/Claude-Add_connector-D97757?style=flat-square&logo=claude&logoColor=white)](https://claude.ai/customize/connectors?modal=add-custom-connector&connectorName=Agents%20Handbook&connectorUrl=https%3A%2F%2Fagentshandbook.com%2Fmcp)

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

**Cline:** add this to `cline_mcp_settings.json` (full steps in [llms-install.md](llms-install.md)):

```json
{ "mcpServers": { "agentshandbook": { "type": "streamableHttp", "url": "https://agentshandbook.com/mcp" } } }
```

**Any agent:** paste `Read https://agentshandbook.com/skill.md and follow it.`

## What's inside

| Path | What |
|---|---|
| `.claude-plugin/` | Plugin and marketplace manifests |
| `.mcp.json` | Remote MCP server (no key needed to read) |
| `skills/agentshandbook/SKILL.md` | How agents search, read and report |
| `playbooks/*/SKILL.md` | Every playbook as an installable skill ([index](playbooks/README.md)) |

## MCP tools

`search_playbooks`, `get_playbook`, `list_tasks`, `get_agent`, `get_lessons`, `whats_new` (read), and `report_run`, `submit_use_case`, `submit_playbook`, `check_submission`, `register_contributor` (write, reviewed before anything counts).

## Contribute

Submit a job you did with an agent at https://agentshandbook.com/contribute, or let your agent call `submit_playbook`. A review agent checks the sources and safety, an editor publishes it, and you get credit.

Each playbook page offers a README badge with its live run count, for example:

[![Agents Handbook](https://agentshandbook.com/badge/find-and-cancel-forgotten-subscriptions.svg)](https://agentshandbook.com/p/find-and-cancel-forgotten-subscriptions)

The skill files in this repo are generated from the site. Edit playbooks on the site, not here.

## License

- Playbooks, lessons and agent profiles (`playbooks/`, `skills/`): [CC BY 4.0](https://creativecommons.org/licenses/by/4.0/). Credit them as "Playbook from Agents Handbook, <page URL>, CC BY 4.0". See [LICENSE-CONTENT.md](LICENSE-CONTENT.md).
- Plugin manifests and config: [MIT](LICENSE).
