# Installing BeHooked Skills

Installation is two one-time steps: install the skills, then connect the BeHooked MCP.

## 1. Install the skills

```
npx skills add thehooked/skills
```

`npx skills` is the open, cross-agent installer ([vercel-labs/skills](https://github.com/vercel-labs/skills)).
It reads the skills straight from this GitHub repo and writes them into the right place for your agent —
Claude Code, Cursor, Codex, and more. No npm package, no API keys.

In **Claude Code**, run `/reload-skills` afterward to load them in the current session. Confirm the skills
are available from your prompts — e.g. `/behooked:generate`, `/behooked:ads`,
`/behooked:product-photoshoot`, `/behooked:house-tour`.

## 2. Connect the BeHooked MCP

```
claude mcp add --transport http behooked https://mcp.behooked.ai/mcp/
```

The skills drive tools served by the hosted BeHooked MCP, so connect it once. Two details matter:

- **Name the server exactly `behooked`** — the skills reference tools as `mcp__behooked__*`.
- **Keep the trailing slash** on the URL — the MCP advertises its OAuth resource with the slash and the
  Claude Code CLI client requires an exact match.

Verify with `/mcp` — you should see `behooked` listed. The first generation triggers a one-time OAuth
sign-in.

## Alternative: Claude Code marketplace plugin

Instead of `npx skills`, you can install the skills as a Claude Code plugin:

```
/plugin marketplace add thehooked/skills
/plugin install behooked@behooked
```

Then connect the MCP as in step 2 above. (The plugin ships **skills only** — Claude Code doesn't yet
reliably bundle a *remote* MCP server inside a plugin, so the MCP is always a separate one-line add.)

## Other clients (Claude Desktop/web, ChatGPT connectors)

The skills drive tools served by the BeHooked MCP. Add the server in your client's connector settings:

- **Endpoint:** `https://mcp.behooked.ai/mcp/` (Streamable HTTP)
- **Auth:** OAuth (the server runs the sign-in/consent flow; no manual token needed)

Tool names may be namespaced differently by each client; the skills refer to tools by their base names
(e.g. `generate_image`), so they still work.

## After install

- Run any skill; on the first charging call you'll be asked to sign in to BeHooked.
- No BeHooked account yet? Connecting is fine — when you see `account_required`, finish setup and pick a
  plan at [behooked.ai](https://behooked.ai), then continue in your agent (no reconnect needed).

## Updating

- **Skills:** `npx skills update` (or re-run `npx skills add thehooked/skills`). Editing a local
  `SKILL.md` is picked up live; in Claude Code, `/reload-skills` reloads them. If you installed via the
  plugin route, use `/reload-plugins` (or restart the client) instead.
- **MCP connection:** `claude mcp remove behooked`, then re-add with the command in step 2.
