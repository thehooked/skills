# Inputs & uploading

## The inputs / parameters split
`generate_app(app_name, inputs, parameters)`:
- **`inputs`** — the media. For `shots`, just `image_url`. Fields listed in the app's `s3_input_fields`
  must be **fetchable URLs**.
- **`parameters`** — tuning. For `shots`, `aspect_ratio` (default `1:1`; confirm via `describe_app`).

## Staging a local photo
An input URL must be publicly reachable — a local path won't work. To use a local file:
1. `get_upload_url` → returns a URL to upload to (and the public URL to reference).
2. Upload the file bytes to that URL.
3. Pass the returned public URL as `inputs.image_url`.

If the user already has a hosted image URL, use it directly.

## Getting good results
- Use a clear, well-lit photo with the product/subject unobstructed and centered.
- Higher-resolution inputs generally yield better shots.
- Match `aspect_ratio` to where the shots will be used (square for catalog grids, 16:9 for banners) —
  check the allowed values in `describe_app` first.

## Array inputs (other apps)
Some apps require certain inputs as **lists** (their `array_inputs`), and some list items must follow a
shape (e.g. sizes as `"WIDTHxHEIGHT"` strings) — `describe_app` reports `array_inputs` and
`array_item_shapes`. `shots` takes a single `image_url`, so this doesn't apply here, but keep it in mind
when using other apps.
