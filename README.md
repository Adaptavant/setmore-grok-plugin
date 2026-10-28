# Setmore Grok Plugin

Connects [Grok Build](https://x.ai/) to your [Setmore](https://www.setmore.com) account via the hosted Setmore MCP server, so you can manage scheduling directly from Grok.

## What it does

- Book, reschedule, and cancel appointments
- Check staff availability and working hours
- Look up and manage customers
- Manage services and settings (account owners and admins only)
- Send and read Setmore Connect messages

## How it works

This plugin points Grok at Setmore's hosted MCP server (`https://mcp.setmore.com/mcp`) over HTTP. No local server or install is required — see [`.mcp.json`](./.mcp.json). Export `SETMORE_OAUTH_CLIENT_SECRET` (the Fullauth client secret) before starting Grok. You'll be prompted to sign in to your Setmore account the first time a tool is used.

## Marketplace listing metadata

For the `xai-org/plugin-marketplace` catalog entry (`.grok-plugin/marketplace.json`, added separately in that repo):

- **keywords**: `setmore`, `setmore scheduling`, `setmore appointments`, `setmore booking`, `setmore calendar`, `setmore connect`
- **domains**: `setmore.com`, `mcp.setmore.com`, `auth.setmore.com`
- **category**: `productivity`

## Files

| File | Purpose |
|---|---|
| `.mcp.json` | Points Grok at the hosted Setmore MCP server |
| `.grok-plugin/plugin.json` | Plugin manifest (name, description, keywords) |
| `skills/setmore/SKILL.md` | Usage guidance for the assistant |

## License

[MIT](./LICENSE)
