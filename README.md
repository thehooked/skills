# BeHooked Skills

AI media-generation skills for coding agents, powered by the live **[BeHooked Studio](https://behooked.ai)** MCP.

Generate images, video, and audio, and run marketing apps (product ads, product photoshoots, real-estate
house tours) directly from your agent — no CLI, no API keys to manage. Installing the plugin registers
the BeHooked MCP for you; you sign in once via OAuth on the first generation.

## Skills

| Skill | What it does |
|-------|--------------|
| `/behooked:generate` | Images, video, audio (speech/music/SFX), video edits, and lipsync — picks the right model, prices it in credits, returns a hosted media URL. |
| `/behooked:ads` | Product ad videos from a URL (auto-scraped) or your product photos; single ads or batches of variations across creative templates. |
| `/behooked:product-photoshoot` | 9 cinematic studio shots from a single product photo. |
| `/behooked:house-tour` | Cinematic real-estate walkthrough video from listing photos, optionally with a guide avatar. |

## Install (Claude Code)

```
/plugin marketplace add thehooked/skills
/plugin install behooked@behooked
```

That's it. The `behooked` MCP server is registered automatically. The **first** time a skill runs a
generation, your browser opens a one-time BeHooked sign-in (OAuth); after that it just works.

> New to BeHooked? You can connect before you have an account. When a skill reports `account_required`,
> finish signing up and pick a plan at **[behooked.ai](https://behooked.ai)** — then continue right in
> your agent, no reconnect needed.

## How it works

Each skill is a prompt/orchestration layer over the BeHooked Studio MCP (`https://mcp.behooked.ai/mcp`).
The skills encode model selection, parameter building, and the priced-then-generate workflow; the MCP
does the generation and returns a hosted URL. Generation spends **credits** (your BeHooked plan); a
skill always tells you the credit cost before it charges, and failed jobs aren't charged.

## Requirements

- An MCP-capable agent (Claude Code today; the MCP also works in Claude Desktop/web and ChatGPT
  connectors if you add `https://mcp.behooked.ai/mcp` manually).
- A BeHooked account with credits (set up at [behooked.ai](https://behooked.ai)).

## License

MIT — see [LICENSE](LICENSE).
