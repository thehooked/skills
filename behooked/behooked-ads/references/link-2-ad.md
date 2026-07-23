# link-2-ad — URL to ad

The fast path: a product URL becomes a finished ad video. `scrape` extracts the product images and copy
so you don't have to upload anything.

## Flow
1. `scrape(url, app_name="link-2-ad")` — free. Returns a `scrape_request_id` referencing the pulled
   product data (images + description). If the site blocks scraping or returns no usable images, switch
   to `adgen` with manually uploaded images.
2. `describe_app("link-2-ad")` — confirm `template` options, quality tiers, and `time_estimate`.
3. `estimate_app_cost("link-2-ad", parameters={...})` — **state the credit cost** before generating.
4. `generate_app("link-2-ad", parameters={...}, scrape_request_id="<from step 1>", idempotency_key)`.
5. `await_app_result(request_id)` → the ad video `output_url`.

## Inputs & parameters
- With a `scrape_request_id`, the product images/description come from the scrape — you usually only set
  `parameters`.
- To override or supply your own media instead of scraping, pass `inputs` directly:
  `product_image_1`, `product_image_2`, `product_image_3` (URLs — stage locals via `get_upload_url`),
  `product_description`, optional `logo`.
- `parameters`: `template` (unboxing, customer_review, simple_ugc, clean_minimal, viral, luxury,
  product_story), `aspect_ratio` (default `9:16`), `quality` (standard / high / premium),
  `brand_colors`, `custom_instruction`.

## Notes
- `link-2-ad` is a workflow app; expect a multi-minute render. Set expectations from `time_estimate`.
- Bills only on success. On failure, tell the user nothing was charged.
- Always confirm the current template list and allowed values from `describe_app` — this doc is a guide,
  the tool is the source of truth.
