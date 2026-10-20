# Ficiel MCP: connect Claude to your Instagram, WhatsApp and LinkedIn DMs

[Version française](README.md)

Ficiel is an AI inbox for coaches and setters: it surfaces old Instagram, WhatsApp and LinkedIn conversations worth following up, drafts the message, and nothing is sent without human approval.

This repository documents Ficiel's MCP (Model Context Protocol) server: the endpoint that lets Claude, Cursor or any MCP client read your conversations, find a contact, spot dormant leads and draft a follow-up, with your permission. It contains documentation only. The server is a service hosted by Ficiel and its code is not published here.

- Server URL: `https://bridge.ficiel.io/mcp` (Streamable HTTP)
- Tools: 74 as of October 20, 2026, 17 of which display an interactive screen, plus 12 ready-made requests (prompts) in your assistant's menu; no voice message is ever generated, a voice message sent is always one you recorded (stats, funnel, cash, leads to follow up, drafted follow-up, prospect card, analysis…), full list in [TOOLS.md](TOOLS.md) (titles and descriptions in French, as sent by the server)
- Interactive screens (MCP Apps, since October 8, 2026): "who left me on read?" shows the leads to follow up with a Follow up button; the drafted follow-up opens in the same screen and is sent on a click on Send. Also a prospect card and a monthly summary
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
- "Read my whole thread with `@name` and tell me what made them hesitate."
- "Draft a follow-up for the five prospects who asked my price in September, I will approve them in Ficiel."

## Nothing is sent without a human

Ficiel is AI setting with human approval: Kord does a setter's work, and you approve every send. An assistant can read almost everything and do almost nothing on its own. See [HUMAIN.md](HUMAIN.md) (in French): read-only keys by default, a named recipient required on every send and checked against the real contact, no messages to strangers, the same safeguards as the app.

## Access

The server is open to organizations on a trial (10 days free: https://ficiel.io) or subscribed. Without a started trial, while paused, or if a subscription is unpaid or expired, every tool returns a refusal with the link to reactivate access.

What the assistant can do depends on the plan. **Essentiel**: all the day-to-day work, meaning reading, searching, preparing, sending and scheduling follow-ups, organizing contacts (tags, stages, notes, one at a time or in bulk) and adjusting Kord. **Intégral**: on top of that, creating and configuring automations, per-channel AI and the offer amount. Reading those settings, pausing a channel or turning an automation off stay open to everyone. A reserved tool returns a refusal that says what the current plan already allows and links to change plans.

## Contact

Abraham Rajoelina, founder of Ficiel: abraham@ficiel.io

Documentation licensed under CC BY 4.0 (see [LICENSE](LICENSE)).

## Where to find Ficiel MCP

- Official MCP Registry: `io.ficiel/ficiel`
- [Glama](https://glama.ai/mcp/connectors/io.ficiel/ficiel)
- [LobeHub](https://lobehub.com/mcp/ficiel)
- [Cursor Directory](https://cursor.directory/plugins/ficiel-mcp)
- [mcpservers.org](https://mcpservers.org/servers/ficiel-io-mcp)
- Official page: https://ficiel.io/mcp/

## License

The documentation in this repository is licensed under Creative Commons Attribution 4.0 International (CC BY 4.0, full text in [LICENSE](LICENSE)), © 2026 Ficiel.io, Abraham Rajoelina. It covers only the files in this repository: the Ficiel service, its MCP server and their code are not covered and remain the property of Ficiel.io.
