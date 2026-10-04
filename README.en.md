# Ficiel MCP: connect Claude to your Instagram, WhatsApp and LinkedIn DMs

[Version française](README.md)

Ficiel is an AI inbox that rereads your Instagram, WhatsApp and LinkedIn conversation history to find and follow up with prospects who never got a reply.

This repository documents Ficiel's MCP (Model Context Protocol) server: the endpoint that lets Claude, Cursor or any MCP client read your conversations, find a contact, spot dormant leads and draft a follow-up, with your permission. It contains documentation only. The server is a service hosted by Ficiel and its code is not published here.

- Server URL: `https://bridge.ficiel.io/mcp` (Streamable HTTP)
- Tools: 65 as of October 4, 2026 (32 read, 33 write), full list in [TOOLS.md](TOOLS.md) (titles and descriptions in French, as sent by the server)
- Text is never cut: messages, voice notes, notes and agent instructions come back in full; long answers are paginated (`next_cursor`)
- Media are readable: an image carries its description and visible text, a document its text, a video its duration and spoken words; `ficiel_get_media` returns the image or document itself
- Channels: Instagram, WhatsApp, LinkedIn
- Official page: https://ficiel.io/mcp/
- Official MCP registry: `io.ficiel/ficiel`

## Claude app (claude.ai, desktop, mobile)

1. Connect your channels to Ficiel (https://app.ficiel.io).
2. In Claude, open Settings, then Connectors, and add a custom connector with the URL `https://bridge.ficiel.io/mcp`.
3. Claude sends you to Ficiel: sign in and choose what the assistant may do (read only, or read and send).

No key to copy: the connection uses OAuth and shows up in your Ficiel settings, where you can revoke it at any time.

## Claude Code

Create a key in your Ficiel settings, then:

```bash
claude mcp add --transport http ficiel https://bridge.ficiel.io/mcp --header "Authorization: Bearer YOUR_KEY"
```

## Cursor and other MCP clients

```json
{
  "mcpServers": {
    "ficiel": {
      "url": "https://bridge.ficiel.io/mcp",
      "headers": { "Authorization": "Bearer YOUR_KEY" }
    }
  }
}
```

Keys start with `fk_live_`. A key belongs to a single organization and never sees anything else.

## ChatGPT

ChatGPT accepts remote MCP servers in developer mode, on the web, for Plus, Pro, Business, Enterprise and Education plans ([OpenAI documentation](https://developers.openai.com/api/docs/guides/developer-mode)):

1. In ChatGPT, Settings, Security and login: turn on developer mode.
2. Create a developer-mode app with the URL `https://bridge.ficiel.io/mcp`, OAuth authentication.
3. ChatGPT sends you to Ficiel: sign in and choose read only, or read and send.

This follows OpenAI's documentation but has not been tested end to end by Ficiel yet: verified clients are Claude (app and Claude Code) and Cursor.

## Example requests

- "List the conversations where my last message was seen and got no reply for more than three days."
- "Read my whole thread with @name and tell me what made them hesitate."
- "Draft a follow-up for the five prospects who asked my price in September, I will approve them in Ficiel."

## Nothing is sent without a human

An assistant can read almost everything and do almost nothing on its own. See [HUMAIN.md](HUMAIN.md) (in French): read-only keys by default, a named recipient required on every send and checked against the real contact, no messages to strangers, the same safeguards as the app.

## Access

The server is open to organizations subscribed to Ficiel. During the free audit, or if a subscription is unpaid, tools return an explicit refusal. Trial: https://ficiel.io (10 days free).

## Contact

Abraham Rajoelina, founder of Ficiel: abraham@ficiel.io

Documentation licensed under CC BY 4.0 (see [LICENSE](LICENSE)).
