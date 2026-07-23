---
version: 0.1.0
name: behooked-product-photoshoot
description: |
  Turn a single product (or subject) photo into a set of cinematic studio shots with BeHooked Studio's
  live MCP, using the `shots` app — 9 storyboard-style images from one photo.
  Use when: "make a product photoshoot", "generate studio shots of this", "give me 9 angles/shots of
  this product", "cinematic product photography from this photo".
  NOT for: ad videos (use behooked-ads), arbitrary single-image generation (use behooked-generate),
  house tours (use behooked-house-tour), or billing (web-only).
argument-hint: "[product photo path or URL] [--aspect 1:1|4:3|16:9]"
allowed-tools: mcp__plugin_behooked_behooked__list_apps, mcp__plugin_behooked_behooked__describe_app, mcp__plugin_behooked_behooked__validate_app_inputs, mcp__plugin_behooked_behooked__generate_app, mcp__plugin_behooked_behooked__await_app_result, mcp__plugin_behooked_behooked__get_app_result, mcp__plugin_behooked_behooked__list_app_jobs, mcp__plugin_behooked_behooked__get_upload_url, mcp__plugin_behooked_behooked__get_credit_balance
---

# BeHooked — Product Photoshoot

Generate a cinematic product photoshoot from one photo, via the **BeHooked Studio MCP** `shots` app. It
produces 9 storyboard-style shots from a single input image.

> Tools written unprefixed; your client may show `mcp__plugin_behooked_behooked__<tool>`. The MCP must
> be connected (see behooked-generate Step 0). `user_id` is never an input.

## What `shots` is
- A **pipeline** app (multi-stage) that is nonetheless directly runnable via `generate_app`.
- Input: one image. Output: 9 images (`output_type: image`).

## Inputs & parameters
- `inputs.image_url` — the product/subject photo. **Required.** It's an `s3_input_field`, so it must be
  a fetchable URL — stage a local file with `get_upload_url` first.
- `parameters.aspect_ratio` — default `1:1`; confirm allowed values from `describe_app`.

## Mandatory workflow (server-enforced)
1. **Stage the image** — `get_upload_url` → upload the local photo → use the returned URL. (Skip if you
   already have a public URL.)
2. **Discover** — `describe_app("shots")` for the contract, allowed `aspect_ratio` values, and the
   `time_estimate`. Note: for pipeline apps, `estimate_app_cost` **raises** — state the completion
   charge from `describe_app`'s pricing block (in credits) instead.
3. **Validate** — `validate_app_inputs("shots", {"image_url": "<url>"})`; fix errors.
4. **Generate** — `generate_app("shots", inputs={"image_url": "<url>"}, parameters={"aspect_ratio": "1:1"},
   idempotency_key)`.
5. **Poll** — `await_app_result(request_id)` → the 9 shot image URLs.

```
get_upload_url  ->  upload photo  ->  image_url
describe_app("shots")                     # state the credit cost from its pricing block
validate_app_inputs("shots", {image_url})
generate_app("shots", inputs={image_url}, parameters={aspect_ratio}, idempotency_key)
await_app_result(request_id)              # -> 9 images
```

## UX rules
- State the credit cost (from `describe_app`, since estimate raises for pipelines) before generating.
- It's a multi-stage pipeline — set time expectations from `time_estimate`; it takes longer than a
  single image. Tell the user they can keep working.
- Bills only on success. On failure, tell the user nothing was charged.
- New account → `account_required`: send to behooked.ai to pick a plan, then continue here.
- A clean, well-lit input photo with the product clearly visible gives the best shots.
- Return the set of image URLs; don't dump job ids.

## References
- [references/shots-pipeline.md](references/shots-pipeline.md) — how the pipeline app runs and polls.
- [references/product-inputs.md](references/product-inputs.md) — uploading and the inputs/parameters split.
