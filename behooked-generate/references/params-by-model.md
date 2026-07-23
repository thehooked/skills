# Building the `params` object

The generate tools take only `model`, `prompt`, and `params`. Everything else lives in `params`. The
correct keys are per-model — **read them, don't guess.**

## The reliable pattern

1. `describe_model(media_type, model)` returns:
   - `required_params` / `optional_params` — the keys you may set.
   - `parameter_validation` — the allowed values / ranges per key (e.g. `aspect_ratio.allowed_values`).
   - `default_parameters` — what you get if you omit a key.
   - `modes` / `variants` — for models that support text-to-X vs image-to-X, etc.
2. Build `params` using only those keys, with values drawn from `parameter_validation`.
3. `validate_params(media_type, model, params)` → fix any error → generate.

If you already know the model, the catalog reference lists the same option sets:
[model-catalog.md](model-catalog.md).

## Per-media patterns

### Image (`media_type: "image"`)
- Common `params`: `aspect_ratio` **or** `image_size` (model-specific — some use canonical ratios like
  `16:9`, others named presets like `landscape_16_9`, others pixel sizes like `1536x1024`), `resolution`
  (`1K`/`2K`/`4K` on models that support it), `quality` (`low`/`medium`/`high`), `num_images`.
- Inpainting models (e.g. `flux-fill`) require `image_url` + `mask_url` in `params`.
- Editing an existing image: pass the source as the model's image input key (often `image_url`);
  `describe_model` shows the exact key and whether the model `supports_editing`.

### Video (`media_type: "video"`)
- Common `params`: `aspect_ratio`, `duration` (e.g. `4s`/`6s`/`8s` — values are model-specific),
  `resolution` (`720p`/`1080p`/`4k`), and `generate_audio` on models that support native audio.
- Animate a still (image-to-video): the model exposes a `mode` and an input key like `image_url` /
  `first_frame_url` / `last_frame_url`. Set `mode` to the image-to-video value and pass the URL(s).

### Audio (`media_type: "audio"` — TTS, music, SFX)
- One tool, `generate_audio`; the `model` decides speech vs music vs SFX.
- **TTS:** the spoken text usually goes in `params._prompt_text` (not `prompt`) — confirm with
  `describe_model`. Voice/style keys (e.g. `voice`) are model-specific.
- **Music / SFX:** describe the desired audio in `prompt`; duration/format keys live in `params`.

### Edit (`media_type: "edit"`) and Lipsync (`media_type: "lipsync"`)
- These output video but have their own catalogs — use `media_type` `edit` / `lipsync` for
  describe/estimate/validate.
- Edit/restyle: pass the source video URL as the model's input key (via `describe_model`).
- Lipsync: pass a face image/video **and** a voice/audio input; keys are model-specific.

## Staging local files

Any input URL must be publicly fetchable. For a local file: `get_upload_url` → upload the bytes to the
returned URL → use that URL as the `params` input. Never pass a local path.

## Idempotency

Pass an `idempotency_key` on `generate_*` and reuse the exact same value if you retry a submit — the
server replays the prior submission instead of charging again.
