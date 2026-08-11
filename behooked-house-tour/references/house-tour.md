# house-tour — details

Turn up to 15 house/room photos into a cinematic walkthrough video, optionally narrated by a guide
avatar.

## Inputs (`inputs` dict)
- `image_urls` — **required, a list** of up to 15 photo URLs (this is an `array_input`; a bare string
  fails validation). Fields under `s3_input_fields` must be fetchable URLs — upload locals first.
  15 is the web app's cap; the server only enforces the model's own 30-reference ceiling across
  rooms + avatar + floor plan combined.
- `avatar_url` (optional) — a tour-guide presenter to narrate/appear.
- `avatar_preview_url`, `avatar_scrambled` (optional) — avatar support fields.

## Parameters (`parameters` dict) — confirm via `describe_app`
- `aspect_ratio` — default `16:9` (also `9:16` for vertical/social).
- `resolution` — `480p` (default) or `720p`. This is the price axis: cost scales with
  resolution AND duration, so pass both to `estimate_app_cost` for a real figure. There are
  no quality tiers — a `quality` value is ignored.
- `duration` — `8` / `12` / `15` / `30` seconds. Every length renders in a single pass.
- `template` — default `cinematic`.
- `generate_audio` — default provided by the app.

## Flow
```
get_upload_url (per photo) -> upload -> image_urls = [url1, ..., url15]
describe_app("house-tour")
estimate_app_cost("house-tour", parameters={...}, inputs={"image_urls": [...]})   # state the number
validate_app_inputs("house-tour", {"image_urls": [...], ...})
generate_app("house-tour", inputs={"image_urls": [...], "avatar_url": "..."}, parameters={...}, idempotency_key)
await_app_result(request_id)   # -> walkthrough video url
```

## Failure handling
- **Moderation blocks:** the underlying video model may reject an image, surfacing as a failed job.
  Provider fallback is short-circuited for moderation, so resubmitting the same photo fails again —
  replace the flagged image. Nothing is charged on failure.
- **Validation:** the most common mistake is passing `image_urls` as a string instead of a list. Keep it
  a list even for one image.
- Bills only on success; reuse the same `idempotency_key` on a retry.

## Tips
- Order the photos in the sequence you want the tour to flow (entrance → living areas → bedrooms → …).
- Clear, well-lit, straight-on room photos produce the best and most reliably accepted tours.
- Set time expectations from `time_estimate` — this is a multi-minute render.
