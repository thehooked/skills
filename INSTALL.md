# Installing BeHooked Skills

## Claude Code (recommended)

```
/plugin marketplace add thehooked/skills
/plugin install behooked@behooked
```

Installing the plugin also registers the `behooked` MCP server (from the bundled `.mcp.json`). Verify
with `/mcp` — you should see `behooked` listed. The first generation triggers a one-time OAuth sign-in.

To confirm the skills loaded, the following slash commands should be available:
`/behooked:generate`, `/behooked:ads`, `/behooked:product-photoshoot`, `/behooked:house-tour`.

## Manual MCP connection (other clients)

The skills drive tools served by the BeHooked MCP. If your client doesn't use the plugin, add the
server manually and then use the skill prose as guidance:

- **Endpoint:** `https://mcp.behooked.ai/mcp` (Streamable HTTP)
- **Auth:** OAuth (the server runs the sign-in/consent flow; no manual token needed)

This works in Claude Desktop/web and ChatGPT connectors, among others. Tool names may be namespaced
differently by each client; the skills refer to tools by their base names (e.g. `generate_image`).

## After install

- Run any skill; on the first charging call you'll be asked to sign in to BeHooked.
- No BeHooked account yet? Connecting is fine — when you see `account_required`, finish setup and pick a
  plan at [behooked.ai](https://behooked.ai), then continue in your agent (no reconnect needed).

## Updating

`.mcp.json` and manifest changes require `/reload-plugins` (or restarting the client). Editing a
`SKILL.md` is picked up live.
