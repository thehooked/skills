---
version: 0.1.0
name: behooked-generate
description: |
  Generate images, video, audio (speech/music/SFX), video edits/restyles, and lipsync via
  BeHooked Studio's live MCP. Picks the right model for the goal, prices it in credits, and
  returns a hosted media URL.
  Use when: "generate an image", "make a product photo", "create a video", "animate this image",
  "text to speech / voiceover", "make background music", "add a sound effect", "restyle this video",
  "lip-sync this face to audio", "upscale"/edit an existing generation.
  NOT for: full ad creation from a product/URL (use behooked-ads), studio product photoshoots
  (use behooked-product-photoshoot), real-estate house tours (use behooked-house-tour), or anything
  about billing/plans/buying credits (that is web-only at behooked.ai).
argument-hint: "[what to generate] [--image|--video|--audio] [--model <id>]"
allowed-tools: mcp__plugin_behooked_behooked__find_model, mcp__plugin_behooked_behooked__list_models, mcp__plugin_behooked_behooked__describe_model, mcp__plugin_behooked_behooked__estimate_cost, mcp__plugin_behooked_behooked__validate_params, mcp__plugin_behooked_behooked__generate_image, mcp__plugin_behooked_behooked__generate_video, mcp__plugin_behooked_behooked__generate_audio, mcp__plugin_behooked_behooked__generate_edit, mcp__plugin_behooked_behooked__generate_lipsync, mcp__plugin_behooked_behooked__await_result, mcp__plugin_behooked_behooked__get_result, mcp__plugin_behooked_behooked__list_jobs, mcp__plugin_behooked_behooked__get_credit_balance, mcp__plugin_behooked_behooked__get_upload_url, mcp__plugin_behooked_behooked__list_assets
---

# BeHooked — Generate

Generate media through the **BeHooked Studio MCP**. This skill is the "taste layer": which model to
pick, how to build its parameters, and how to run the priced-then-generate workflow the server expects.

> Tool names below are written unprefixed (`generate_image`, `describe_model`, …). They are served by
> the `behooked` MCP; your client shows them prefixed (e.g. `mcp__plugin_behooked_behooked__generate_image`).
> Use whichever the client exposes.

## Step 0 — the MCP must be connected

This skill drives the BeHooked MCP. If installed as the `behooked` plugin, the server is registered
automatically and the **first** charging call triggers a one-time OAuth consent in the browser. If the
tools aren't available, tell the user to add the connector (`/plugin install behooked@behooked`, or add
`https://mcp.behooked.ai/mcp` as an HTTP MCP server) and sign in when prompted. Do not fabricate output.

## The one thing to understand: the thin signature

All five generate tools take the **same shape** — `model`, `prompt`, and a free-form `params` object:

```
generate_image(model, prompt, params={...})
generate_video(model, prompt, params={...})
generate_audio(model, prompt, params={...})   # TTS, music, and SFX all live here
generate_edit(model, prompt, params={...})     # video-to-video / restyle
generate_lipsync(model, prompt, params={...})  # face + audio -> talking video
```

**Every model-specific knob goes inside `params`** — aspect_ratio, resolution, duration, quality,
num_images, voice, reference/input URLs, TTS text, etc. The allowed keys and values are per-model. Never
guess them: read them from `describe_model(media_type, model)` (or the catalog reference). See
[references/params-by-model.md](references/params-by-model.md).

`user_id` is **never** a parameter — the server derives who you are from the login. Don't ask for one.

## Mandatory workflow (the server enforces this order)

1. **Discover** — `find_model` / `list_models` / `describe_model` to lock the exact model id, its
   `params` schema, and allowed values.
2. **Estimate + say the number** — `estimate_cost(media_type, model, params)`. **State the credit cost
   in your reply before generating.** The approval dialog never shows cost; if you don't say it, the
   user approves blind. Compare candidates by credits and, when quality is comparable, prefer cheaper.
3. **Validate** — `validate_params(media_type, model, params)` and fix every error. Do not call a
   generate tool until validation returns no errors.
4. **Generate** — `generate_*`. On any retry, reuse the same `idempotency_key` so a resend never
   double-charges.
5. **Poll** — `await_result(request_id)` (or `get_result`) for the `output_url`. Set time expectations
   first: image ~20s; video / edit / lipsync can take minutes. Tell the user they can keep working.

`media_type` for the estimate/validate/describe tools is one of: `image`, `video`, `audio`, `edit`,
`lipsync`. (TTS, music, and SFX are all `audio`.)

## Model selection (quick tree)

Pick by the user's goal; confirm the exact id and options against
[references/model-catalog.md](references/model-catalog.md) or `describe_model`.

- **Image, photoreal / needs legible text** → `gpt-image-2` (superior, 4K, strong text) or a
  Midjourney v8.1 variant for a stylized/photographic look.
- **Image, fast & cheap iterations** → a Nano Banana variant (fast, many aspect ratios).
- **Image, illustration / anime** → a Midjourney Niji variant.
- **Image, inpainting (mask a region)** → `flux-fill` (needs `image_url` + `mask_url`).
- **Video, wants native audio / dialogue** → a Sora, Kling, or Seedance model that lists
  `supports_audio`; check the catalog for which.
- **Video, animate a still** → any model with an image-to-video mode; pass the still as the input URL.
- **Speech / voiceover (TTS)** → an ElevenLabs or MiniMax speech model; put the spoken text where the
  model expects it (often `_prompt_text` in `params` — confirm via `describe_model`).
- **Music** → `minimax-music-v2` or `elevenlabs-music`. **Sound effect** → `elevenlabs-sound-effects-v2`.
- **Lipsync / talking avatar** → `omnihuman`, a Kling avatar model, or another lipsync id (needs a face
  image/video + a voice/audio input).
- **Restyle / edit an existing video** → `generate_edit` with a video-edit model.

When the user hasn't named a model, pick a sensible default from the tree, say which you chose and why,
and mention it's adjustable.

## UX rules

- Be concise. Never dump raw JSON, request ids, or tool plumbing at the user. Show the result (a link
  or the media) and the credit cost.
- Always poll to completion and return the `output_url`; don't leave a job hanging.
- Local files must be staged first: `get_upload_url` → upload → use the returned URL as the input.
- On a **failed** job, tell the user nothing was charged (media charges refund on failure). Say this
  only on failure.
- **New account:** call `get_credit_balance` early. If it returns `account_required=true`, stop and
  tell the user to finish signup + pick a plan at behooked.ai — they can continue here after, no
  reconnect. Same for an `account_required` / `concurrency_limit` result from a generate call.
- **Out of scope** (billing, upgrading, buying credits, web-only features): route to behooked.ai; there
  are no tools for these.

## References

- [references/model-catalog.md](references/model-catalog.md) — every enabled model id, its options, and
  capabilities (generated; no pricing — get that live from `estimate_cost`).
- [references/params-by-model.md](references/params-by-model.md) — how to turn `describe_model` output
  into a correct `params` object, with per-media patterns.
- [references/prompt-engineering.md](references/prompt-engineering.md) — prompt patterns per media type.
- [references/workflows.md](references/workflows.md) — the full discover→poll flow, chaining, idempotency.
- [references/troubleshooting.md](references/troubleshooting.md) — errors, moderation, timeouts, onboarding.
