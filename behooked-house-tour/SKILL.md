---
version: 0.1.0
name: behooked-house-tour
description: |
  Generate a cinematic real-estate walkthrough video from house photos with BeHooked Studio's live MCP,
  using the `house-tour` app — up to 7 room images become a tour, optionally narrated by a guide avatar.
  Use when: "make a house tour video", "turn these listing photos into a walkthrough", "real-estate
  tour video from these room images", "property walkthrough with a presenter".
  NOT for: product ads (use behooked-ads), product photoshoots (use behooked-product-photoshoot),
  general video generation (use behooked-generate), or billing (web-only).
argument-hint: "[house photo paths or URLs] [--aspect 16:9|9:16] [--avatar <url>]"
allowed-tools: mcp__behooked__*
---

# BeHooked — House Tour

Generate a cinematic property walkthrough from listing photos, via the **BeHooked Studio MCP**
`house-tour` app.

> Tools written unprefixed; your client may show `mcp__behooked__<tool>`. The MCP must
> be connected (see behooked-generate Step 0). `user_id` is never an input.

## Inputs & parameters
- `inputs.image_urls` — **required, a list** (this is an `array_input`) of up to 7 room/house photo
  URLs. Each must be a fetchable URL — stage local files with `get_upload_url`.
- Optional inputs: `avatar_url` (a tour-guide presenter), `avatar_preview_url`, `avatar_scrambled`.
- `parameters` (confirm via `describe_app`): `aspect_ratio` (default `16:9`), `quality` tier
  (standard / pro), `duration`, `resolution`, `generate_audio`, `template`
  (default `cinematic`).

## Mandatory workflow (server-enforced)
1. **Stage images** — `get_upload_url` per photo → upload → collect the URLs into a list.
2. **Discover** — `describe_app("house-tour")` for the contract, allowed values, quality tiers, and
   `time_estimate`.
3. **Estimate + say the number** — `estimate_app_cost("house-tour", parameters={...}, inputs={...})`;
   state the credit cost before generating.
4. **Validate** — `validate_app_inputs("house-tour", inputs)`; make sure `image_urls` is a **list** and
   fix any errors.
5. **Generate** — `generate_app("house-tour", inputs={"image_urls": [...]}, parameters={...},
   idempotency_key)`.
6. **Poll** — `await_app_result(request_id)` → the walkthrough video `output_url`.

```
get_upload_url (per photo) -> upload -> image_urls = [url1, url2, ...]   # up to 7
describe_app("house-tour")
estimate_app_cost("house-tour", parameters={aspect_ratio, quality, template}, inputs={image_urls})  # say it
validate_app_inputs("house-tour", {image_urls, ...})
generate_app("house-tour", inputs={image_urls, avatar_url?}, parameters={...}, idempotency_key)
await_app_result(request_id)   # -> tour video url
```

## UX rules
- **`image_urls` must be a list**, even for a single image — it's an `array_input`. A bare string will
  fail validation.
- State the credit cost before generating. It's a multi-minute render — set expectations from
  `time_estimate` and tell the user they can keep working.
- Bills only on success. On failure, tell the user nothing was charged.
- New account → `account_required`: send to behooked.ai to pick a plan, then continue here.
- Return the finished video URL; don't dump job ids.

## Known limitations (tell the user upfront if relevant)
- **Content moderation:** the underlying video model can reject certain inputs (e.g. images it flags),
  which surfaces as a failed job. This short-circuits provider fallback, so re-submitting the same photo
  will fail again — swap the offending image or adjust inputs. Nothing is charged on a moderation
  failure. This app is the most likely of the BeHooked skills to hit such a block, so set expectations.
- Keep to clear, well-lit interior/exterior room photos for the best (and most reliably accepted) tours.

## References
- [references/house-tour.md](references/house-tour.md) — inputs, the array requirement, avatars, and
  failure handling in detail.
