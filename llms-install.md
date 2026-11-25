# Installing the Frontier MCP server

Frontier is a hosted, remote MCP server. There is nothing to clone, build or run, and no API key.

Add this to the MCP settings (for Cline: `cline_mcp_settings.json`):

```json
{
  "mcpServers": {
    "frontier": {
      "type": "streamableHttp",
      "url": "https://frontierresearch.co/api/mcp"
    }
  }
}
```

Then check it works by calling `list_fields`, or ask: "What's new in neuroscience research this week?" (tool `latest_breakthroughs`).

All seven tools are read-only. Paper and researcher checks (`check_paper`, `check_researcher`) read OpenAlex live and are limited to 30 an hour per connection.
