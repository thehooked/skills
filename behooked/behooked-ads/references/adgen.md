# adgen — product images to ad

The control path: you provide the product media and pick the creative direction. More templates than
`link-2-ad`, plus optional brand avatar and voice.

## Inputs (`inputs` dict)
Required:
- `product_image_1`, `product_image_2`, `product_image_3` — product photo URLs (stage locals with
  `get_upload_url`).
- `product_description` — what the product is / key selling points.

Optional:
- `logo` — brand logo URL.
- `avatar_image` — a spokesperson/brand avatar to feature.
- `avatar_voice` — the voice for the avatar.
- `brand_colors`, `template`, `aspect_ratio`, `custom_instruction`, `product_name`.

`s3_input_fields` (must be URLs): `product_image_1..3`, `logo`. Upload local files first.

## Parameters (`parameters` dict)
- `template` — creative style. adgen supports a wider set than link-2-ad: unboxing, customer_review,
  simple_ugc, clean_minimal, viral, luxury, product_story, cinematic, founder_story, before_after,
  lifestyle, asmr, greenscreen, hype_launch, appscreen. **Confirm the live list from `describe_app`.**
- `aspect_ratio` — default `9:16` (vertical/social); also `16:9`, `1:1`.
- `quality` — standard / high / premium (higher tiers cost more; get figures from `estimate_app_cost`).
- `brand_colors` — e.g. `"#111111, #F5F5F5"`.
- `custom_instruction` — free-text creative direction.
- `duration` — clip length (default provided by the app).

## Flow
```
get_upload_url (x3+)  -> upload product images (+ logo/avatar)
describe_app("adgen")
estimate_app_cost("adgen", parameters={template, aspect_ratio, quality}, inputs={...})  # say the number
validate_app_inputs("adgen", inputs)
generate_app("adgen", inputs={...}, parameters={...}, idempotency_key)
await_app_result(request_id)   # -> ad video url
```

## Notes
- Bills only on success. Multi-minute render — set expectations from `time_estimate`.
- To generate several styles at once, use `generate_app_batch` with `template_counts` (see
  [batch-variations.md](batch-variations.md)).
