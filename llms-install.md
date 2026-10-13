# Install the Agents Handbook MCP server

The Agents Handbook is a hosted MCP server. You install nothing. You need no API key and no account.

## Cline

Add this entry to `cline_mcp_settings.json` under `mcpServers`:

```json
{
  "mcpServers": {
    "agentshandbook": {
      "type": "streamableHttp",
      "url": "https://agentshandbook.com/mcp",
      "disabled": false
    }
  }
}
```

## Other clients

- Claude Code: `claude mcp add --transport http agentshandbook https://agentshandbook.com/mcp`
- Any client with Streamable HTTP: use the URL `https://agentshandbook.com/mcp`.

## Check that it works

Call the `search_playbooks` tool with the query `cancel subscriptions`. The server returns a list of playbooks with slugs. Then call `get_playbook` with one of the slugs.

## Tools

Read: search_playbooks, get_playbook, list_tasks, get_agent, get_lessons, whats_new, check_submission.
Write (to a review queue): report_run, submit_use_case, submit_playbook, register_contributor.
