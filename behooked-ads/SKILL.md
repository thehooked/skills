---
version: 0.1.0
name: behooked-ads
description: |
  Create product advertisement videos with BeHooked Studio's live MCP. Turn a product URL or a few
  product photos into a finished ad, or generate a batch of ad variations across creative templates.
  Use when: "make an ad for this product", "turn this Shopify/Amazon link into an ad", "create a UGC
  video ad", "generate 5 ad variations", "make an unboxing / customer-review / luxury ad".
  NOT for: plain media generation (use behooked-generate), product photoshoot stills
  (use behooked-product-photoshoot), house tours (use behooked-house-tour), or billing (web-only).
argument-hint: "[product URL or description] [--template <name>] [--count N] [--aspect 9:16|16:9|1:1]"
allowed-tools: mcp__behooked__*
---

# BeHooked — Ads

Create product ad videos through the **BeHooked Studio MCP** apps surface. Two apps:

- **`link-2-ad`** — the fast path: give a product **URL**, `scrape` pulls the images + copy, and one
  call renders an ad.
- **`adgen`** — the control path: you provide product images + description and pick a creative
  `template` (and optionally a brand avatar/voice).

> Tools are written unprefixed here; your client may show them as
> `mcp__behooked__<tool>`. Use whatever the client exposes. The MCP must be connected
> (see behooked-generate Step 0). `user_id` is never an input.

## Apps take two dicts

`generate_app(app_name, inputs, parameters, ...)`:
- **`inputs`** — media/product fields. Anything in the app's `s3_input_fields` (product images, logo)
  must be a **fetchable URL** — stage local files with `get_upload_url` first.
- **`parameters`** — tuning (`template`, `aspect_ratio`, `quality`, `brand_colors`, `custom_instruction`).

Always call `describe_app(app_name)` first for the live contract (allowed values, required inputs,
quality tiers, template list). See [references/link-2-ad.md](references/link-2-ad.md) and
[references/adgen.md](references/adgen.md).

## Mandatory workflow (server-enforced)

1. **Discover** — `describe_app("link-2-ad")` or `describe_app("adgen")` for inputs, `template`
   options, quality tiers, and the `time_estimate`.
2. **Prepare inputs** — for `link-2-ad`, `scrape(url, app_name="link-2-ad")` → returns a
   `scrape_request_id` (free). For `adgen`, upload product images via `get_upload_url`.
3. **Estimate + say the number** — `estimate_app_cost(app_name, parameters, inputs, template_counts)`
   and state the credit cost in your reply before generating. For a batch, pass `template_counts` so the
   figure covers **all** ads.
4. **Validate** — `validate_app_inputs(app_name, inputs)`; fix errors.
5. **Generate** — `generate_app(...)` (single) or `generate_app_batch(...)` (variations), with an
   `idempotency_key`.
6. **Poll** — `await_app_result(request_id)` / `get_app_batch(batch_id)` for the video `output_url`(s).

## The two flows

### Link → Ad (fastest)
```
scrape("https://store.example/product/123", app_name="link-2-ad")   # -> scrape_request_id
describe_app("link-2-ad")            # confirm templates + quality
estimate_app_cost("link-2-ad", parameters={template, aspect_ratio, quality})
generate_app("link-2-ad", parameters={...}, scrape_request_id="<from scrape>", idempotency_key)
await_app_result(request_id)         # -> ad video url
```
If scrape can't reach the site or misses images, fall back to the manual `adgen` flow with uploaded
images.

### Product images → Ad (adgen, full control)
```
get_upload_url x3   -> upload product_image_1..3   (and logo if any)
describe_app("adgen")
estimate_app_cost("adgen", parameters={template, aspect_ratio, quality}, inputs={...})
validate_app_inputs("adgen", inputs)
generate_app("adgen", inputs={product_image_1, product_image_2, product_image_3, product_description, ...},
             parameters={template, aspect_ratio, quality, brand_colors, custom_instruction}, idempotency_key)
await_app_result(request_id)
```

### Batch variations
Both apps are batch-capable. `generate_app_batch(app_name, template_counts={...}, inputs, parameters)`
renders multiple ads across templates in one submission. See
[references/batch-variations.md](references/batch-variations.md). Estimate with the same
`template_counts` so the stated cost covers every ad.

## Templates & tuning
- `template` picks the creative style. `link-2-ad`: unboxing, customer_review, simple_ugc,
  clean_minimal, viral, luxury, product_story. `adgen` adds more (cinematic, founder_story,
  before_after, lifestyle, asmr, greenscreen, hype_launch, appscreen, …) and supports an
  `avatar_image` + `avatar_voice`. Always confirm the live list from `describe_app`.
- `aspect_ratio` (9:16 vertical is the default and best for social), `quality` tier (standard / high /
  premium — pricier tiers via `describe_app`), `brand_colors`, `custom_instruction`.

## UX rules
- State the credit cost before generating; for batches state the total for all ads.
- Ad jobs are **not** instant — set expectations from `time_estimate` (often several minutes) and tell
  the user they can keep working.
- On failure, apps bill **only on success**, so tell the user nothing was charged.
- New account → `account_required`: send them to behooked.ai to pick a plan, then continue here.
- Show the finished video URL(s); don't dump job ids.

## References
- [references/link-2-ad.md](references/link-2-ad.md) — the scrape→ad flow in detail.
- [references/adgen.md](references/adgen.md) — inputs, templates, avatars, brand controls.
- [references/batch-variations.md](references/batch-variations.md) — `template_counts` batching.
