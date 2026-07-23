# Installing BeHooked Skills

Installation is two one-time steps: install the skills plugin, then connect the BeHooked MCP.

## Claude Code (recommended)

```
# 1. install the skills
/plugin marketplace add thehooked/skills
/plugin install behooked@behooked

# 2. connect the BeHooked MCP (run in your terminal, not inside Claude Code)
claude mcp add --transport http behooked https://mcp.behooked.ai/mcp
```

Verify with `/mcp` — you should see `behooked` listed. Confirm the skills loaded — these slash commands
should be available: `/behooked:generate`, `/behooked:ads`, `/behooked:product-photoshoot`,
`/behooked:house-tour`. The first generation triggers a one-time OAuth sign-in.

> **Why two steps?** Claude Code doesn't yet reliably support bundling a *remote* MCP server inside a
> plugin (installing such a plugin fails with a "source type not supported" error on current versions).
> So the skills ship on their own and you connect the hosted MCP with the one-line `claude mcp add`.
> Name the server exactly `behooked` so the skills' tool references resolve.

## Other clients (Claude Desktop/web, ChatGPT connectors)

The skills drive tools served by the BeHooked MCP. Add the server in your client's connector settings:

- **Endpoint:** `https://mcp.behooked.ai/mcp` (Streamable HTTP)
- **Auth:** OAuth (the server runs the sign-in/consent flow; no manual token needed)

Tool names may be namespaced differently by each client; the skills refer to tools by their base names
(e.g. `generate_image`), so they still work.

## After install

- Run any skill; on the first charging call you'll be asked to sign in to BeHooked.
- No BeHooked account yet? Connecting is fine — when you see `account_required`, finish setup and pick a
  plan at [behooked.ai](https://behooked.ai), then continue in your agent (no reconnect needed).

## Updating

Skill/plugin manifest changes: `/reload-plugins` (or restart the client). Editing a `SKILL.md` is picked
up live. To update the MCP connection: `claude mcp remove behooked` then re-add.
