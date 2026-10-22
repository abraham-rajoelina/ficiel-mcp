# Installing the Ficiel MCP server (for AI agents)

Ficiel is a hosted remote MCP server. There is nothing to clone, build or run locally.

- Endpoint: `https://bridge.ficiel.io/mcp`
- Transport: Streamable HTTP
- Authentication: OAuth (dynamic client registration) or a personal API key

## Requirements

The user needs a Ficiel account (https://app.ficiel.io) with at least one Instagram, WhatsApp or LinkedIn channel connected.

## Option 1: OAuth (preferred when the client supports it)

Add a remote server with the URL `https://bridge.ficiel.io/mcp`. On first use the client opens Ficiel in the browser; the user signs in and chooses read only, or read and send.

## Option 2: API key

Ask the user to create a key in Ficiel (Settings, MCP). Keys start with `fk_live_`. Then add:

```json
{
  "mcpServers": {
    "ficiel": {
      "type": "streamableHttp",
      "url": "https://bridge.ficiel.io/mcp",
      "headers": { "Authorization": "Bearer fk_live_..." }
    }
  }
}
```

Never write the key into a file that is committed to a repository.

## Check

List the tools: names start with `ficiel_` (83 tools, full list in TOOLS.md). Nothing is sent to a contact without the user's approval; every send must name its recipient.
