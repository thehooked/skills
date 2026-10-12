# CLAUDE.md — repo conventions

Guidance for agents/contributors working in this repo. This is a **public** distribution of skills; keep
it clean of anything internal.

## What this repo is

Five agent **skills** for BeHooked, each a `SKILL.md` + a `references/` folder. The skills are prose over
the live BeHooked Studio MCP, which the user connects separately — there is no backend code here. They
install two ways: the open cross-agent installer (`npx skills add thehooked/skills`, the primary path,
which reads the `SKILL.md` dirs straight from the repo) or as a Claude Code marketplace plugin
(`behooked`; no MCP is bundled). Both consume the same skill directories.

```
.claude-plugin/marketplace.json      # marketplace (plugin source: "./")
.claude-plugin/plugin.json           # plugin metadata
behooked-generate/  behooked-ads/  behooked-product-photoshoot/  behooked-house-tour/  behooked-talking-head/
```

**Flat layout + `source: "./"` + skills-only, on purpose.** This mirrors the exact shape that installs
cleanly (higgsfield-ai/skills). Two things that made install FAIL — do not reintroduce either:
1. **A subdirectory plugin `source` (e.g. `"./behooked"`)** — Claude Code rejects it with "This plugin
   uses a source type your Claude Code version does not support" (still failing on 2.1.218). The plugin
   must be the repo root with `source: "./"`.
2. **A bundled remote (`type: http`) MCP** (`.mcp.json` in the plugin) — same rejection. Ship skills
   only; users connect the hosted MCP once with
   `claude mcp add --transport http behooked https://mcp.behooked.ai/mcp/`.

## Hard rules

1. **No pricing, ever.** No credit amounts, no dollar figures. Skills tell the agent to fetch cost live
   via `estimate_cost` / `estimate_app_cost` / `get_credit_balance`. Never bake numbers into docs.
2. **No infrastructure/provider details.** Don't name the routing/hosting vendors or internal endpoints.
   Model *ids* (e.g. `gpt-image-2`) and their user-facing options are fine; the plumbing behind them is
   not.
3. **`user_id` is never a tool input.** The MCP derives identity from the signed-in session. No skill
   should ask for or pass a user id.
4. **`behooked-generate/references/model-catalog.md` is generated, not hand-edited.** It's produced by an
   internal, fail-closed generator that whitelists only public-safe fields. If it's stale, regenerate it
   from the internal tooling — don't edit it by hand (and never paste pricing/provider fields into it).

## Tool naming

Skills refer to MCP tools by base name (`generate_image`, `describe_app`, …). Because users add the MCP
themselves as a server named `behooked`, clients expose the tools as `mcp__behooked__<tool>`; each
`SKILL.md` uses `allowed-tools: mcp__behooked__*`. This assumes the server is named exactly `behooked`
(as INSTALL instructs). If a client namespaces differently, the base names in the prose still tell the
agent what to call.

## Workflow the skills encode (must stay consistent with the server)

discover (`describe_model` / `describe_app`) → estimate + **state the credit cost** → validate →
generate (with an `idempotency_key`) → poll (`await_result` / `await_app_result`). Never generate as a
first action, never before validating, never before stating cost. Apps/media don't charge on failure.

**Talking Head is different** (its own six tools, not `generate_app`): script agreed in chat →
`list_talking_head_avatars` → `estimate_talking_head` (estimate **and** validate; state the cost) →
`start_talking_head` → `check_talking_head` until `awaiting_approval` → show every scene + the exact
approval cost and get a yes → `approve_talking_head(expected_credits)` → `check_talking_head` until
`done`. It charges each step as it starts and refunds a failed step (not the finished ones before it).

## Adding or editing a skill

- Mirror an existing `SKILL.md`: frontmatter (`version`, `name`, `description` with "Use when:" / "NOT
  for:", `argument-hint`, `allowed-tools`) + a body with Step 0 (MCP connected), the workflow, a
  selection tree, UX rules, and reference links.
- `npx skills` auto-discovers any new `SKILL.md` dir, but still register it in
  `.claude-plugin/marketplace.json` under `skills` so the plugin install path picks it up too.
- Re-check the hard rules before committing.
