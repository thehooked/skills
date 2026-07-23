# BeHooked Model & App Catalog

> Auto-generated (scrubbed). Model ids and their user-facing options only.
> For live cost in credits, call `estimate_cost` / `estimate_app_cost`;
> for available balance call `get_credit_balance`. This file carries NO pricing.

All generation goes through the thin MCP signature: pick a `model`, write a
`prompt`, and put every option below into the `params` object. When unsure of a
model's exact params, call `describe_model(media_type, model)` for the live contract.

## Image models — `generate_image`

#### `flux-fill`
FLUX.1 Fill - region-locked inpainting (image + mask + prompt)
- family: `FLUX`
- capabilities: speed=medium, quality=excellent
- required params: `image_url`, `mask_url`

#### `nano-banana`
Nano Banana - Fast image generation
- family: `Google`
- capabilities: speed=fast, quality=good, average_time_seconds=8, max_images_per_request=4
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`, `21:9`, `2:3`, `3:2`, `5:4`, `4:5`, `auto`
- required params: `aspect_ratio`

#### `seedream`
SeedDream v4 - High quality image generation
- family: `ByteDance`
- capabilities: speed=medium, quality=excellent, average_time_seconds=25, max_images_per_request=10, supports_4k=True
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`, `auto`, `auto_2K`, `auto_4K`
- required params: `image_size`

#### `gpt-image-1`
GPT-Image-1 - OpenAI's latest image generation model (premium quality)
- family: `OpenAI`
- capabilities: speed=medium, quality=superior, average_time_seconds=20, max_images_per_request=4, supports_quality_options=True, supports_transparent_background=True
- image_size options: `1024x1024`, `1536x1024`, `1024x1536`
- quality options: `low`, `medium`, `high`
- required params: `image_size`

#### `nano-banana-pro`
Nano Banana Pro - Enhanced image generation with multiple resolution options
- family: `Google`
- capabilities: speed=fast, quality=excellent, average_time_seconds=10, max_images_per_request=10, supports_4k=True, supports_multiple_resolutions=True
- aspect_ratio options: `21:9`, `16:9`, `3:2`, `4:3`, `5:4`, `1:1`, `4:5`, `3:4`, `2:3`, `9:16`, `auto`
- resolution options: `1K`, `2K`, `4K`

#### `nano-banana-2`
Nano Banana 2 - Latest Nano Banana image generation with web search
- family: `Google`
- capabilities: speed=fast, quality=excellent, average_time_seconds=10, max_images_per_request=10, supports_4k=True, supports_multiple_resolutions=True, supports_web_search=True
- aspect_ratio options: `1:1`, `5:4`, `4:3`, `3:2`, `16:9`, `21:9`, `4:5`, `3:4`, `2:3`, `9:16`, `auto`
- resolution options: `1K`, `2K`, `4K`

#### `nano-banana-2-lite`
Nano Banana 2 Lite - Fast and cost-effective image generation
- family: `Google`
- capabilities: speed=fast, quality=good, average_time_seconds=8
- aspect_ratio options: `1:1`, `5:4`, `4:3`, `3:2`, `16:9`, `21:9`, `4:5`, `3:4`, `2:3`, `9:16`

#### `gpt-image-1-mini`
GPT Image 1 mini - Fast and cost-effective image generation
- family: `OpenAI`
- capabilities: speed=fast, quality=good, average_time_seconds=5, max_images_per_request=10, supports_transparent_background=True
- image_size options: `auto`, `1024x1024`, `1536x1024`, `1024x1536`
- quality options: `auto`, `low`, `medium`, `high`

#### `qwen-image`
Qwen Image - High-quality image generation model
- family: `Qwen`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=10
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`

#### `wan-25-preview`
Wan 2.5 Preview - Advanced image generation with prompt expansion
- family: `Wan`
- capabilities: speed=medium, quality=excellent, average_time_seconds=20, max_images_per_request=4
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`

#### `flux-kontext-pro`
Flux Kontext Pro - Advanced image generation with omni model support
- family: `Flux`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=10
- aspect_ratio options: `21:9`, `16:9`, `4:3`, `3:2`, `1:1`, `2:3`, `3:4`, `9:16`, `9:21`

#### `reve`
Reve - Advanced image generation (Create, Edit, Remix modes)
- family: `Reve`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=10
- aspect_ratio options: `16:9`, `9:16`, `3:2`, `2:3`, `4:3`, `3:4`, `1:1`

#### `flux-2-pro`
Flux Pro 2 - High-quality image generation with advanced safety controls
- family: `Flux`
- capabilities: speed=fast, quality=superior, average_time_seconds=12, max_images_per_request=4
- image_size options: `auto`, `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`
- resolution options: `1K`, `2K`

#### `flux-2-flex`
Flux Flex 2 - Flexible image generation with prompt expansion
- family: `Flux`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=4
- image_size options: `auto`, `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`
- resolution options: `1K`, `2K`

#### `z-image`
Z-Image Turbo - Fast and cost-effective image generation
- family: `Z-Image`
- capabilities: speed=fast, quality=good, average_time_seconds=5, max_images_per_request=10
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`
- resolution options: `1K`, `2K`

#### `seedream-v4.5`
Seedream v4.5 - ByteDance's latest image generation with multi-image editing
- family: `ByteDance`
- capabilities: speed=medium, quality=excellent, average_time_seconds=20, max_images_per_request=10, supports_4k=True
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`, `auto_2K`, `auto_4K`
- resolution options: `2K`, `4K`

#### `seedream-v5-lite`
Seedream 5.0 Lite - ByteDance's latest lightweight image generation
- family: `ByteDance`
- capabilities: speed=fast, quality=excellent, average_time_seconds=10, max_images_per_request=10
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`
- resolution options: `2K`, `3K`

#### `gpt-image-1.5`
GPT-Image-1.5 - OpenAI's advanced image generation model with quality options
- family: `OpenAI`
- capabilities: speed=medium, quality=superior, average_time_seconds=15, max_images_per_request=10, supports_quality_options=True, supports_transparent_background=True
- image_size options: `auto`, `1024x1024`, `1536x1024`, `1024x1536`
- quality options: `low`, `medium`, `high`

#### `qwen-image-2`
Qwen Image 2.0 - High-quality image generation and editing
- family: `Qwen`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=10
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`

#### `qwen-image-2-pro`
Qwen Image 2.0 Pro - Premium quality image generation and editing
- family: `Qwen`
- capabilities: speed=medium, quality=superior, average_time_seconds=20, max_images_per_request=10
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`

#### `wan-2.6`
Wan 2.6 - Text-to-image and style transfer with subject consistency via multi-image input (1-3 reference images)
- family: `Wan`
- capabilities: speed=medium, quality=excellent, average_time_seconds=25, max_images_per_request=4
- image_size options: `square_hd`, `square`, `portrait_4_3`, `portrait_16_9`, `landscape_4_3`, `landscape_16_9`

#### `wan-2.7`
Wan 2.7 - High-quality image generation with advanced prompt understanding
- family: `Wan`
- capabilities: speed=medium, quality=good, max_images_per_request=4
- aspect_ratio options: `1:1`, `3:4`, `4:3`, `9:16`, `16:9`
- resolution options: `1K`, `2K`, `4K`

#### `wan-2.7-pro`
Wan 2.7 Pro - Premium quality image generation with superior detail and composition
- family: `Wan`
- capabilities: speed=medium, quality=excellent, max_images_per_request=4
- aspect_ratio options: `1:1`, `3:4`, `4:3`, `9:16`, `16:9`
- resolution options: `1K`, `2K`, `4K`

#### `kling-image-o3`
Kling O3 - Top-tier image generation with flawless consistency
- family: `Kling`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=9, supports_4k=True, supports_multiple_resolutions=True
- aspect_ratio options: `1:1`, `3:2`, `2:3`, `3:4`, `4:3`, `9:16`, `16:9`, `21:9`, `auto`
- resolution options: `1K`, `2K`, `4K`

#### `z-image-base`
Z-Image Base - Foundation model with robust generative diversity
- family: `Z-Image`
- capabilities: speed=medium, quality=good, average_time_seconds=10, max_images_per_request=10
- aspect_ratio options: `1:1`, `1:1(480p)`, `3:4`, `4:3`, `9:16`, `16:9`

#### `grok-imagine`
Grok Imagine - xAI's highly aesthetic image generation
- family: `Grok`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=10
- aspect_ratio options: `1:1`, `2:3`, `3:2`, `3:4`, `4:3`, `9:16`, `16:9`, `1:2`, `2:1`, `9:20`, `20:9`

#### `kling-image-v3`
Kling V3 - Latest Kling image model
- family: `Kling`
- capabilities: speed=medium, quality=excellent, average_time_seconds=15, max_images_per_request=4, supports_multiple_resolutions=True
- aspect_ratio options: `1:1`, `3:2`, `2:3`, `3:4`, `4:3`, `9:16`, `16:9`, `21:9`
- resolution options: `1K`, `2K`

#### `gpt-image-2`
GPT Image 2 - Extreme prompt adherence, near-perfect text rendering, photorealism up to 4K
- family: `OpenAI`
- capabilities: speed=medium, quality=superior, average_time_seconds=20, max_images_per_request=4, supports_4k=True, supports_quality_options=True, supports_multiple_resolutions=True
- aspect_ratio options: `1:1`, `4:3`, `3:4`, `16:9`, `9:16`
- resolution options: `1K`, `2K`, `4K`
- quality options: `low`, `medium`, `high`

#### `gpt-image-2-max`
GPT Image 2 Max - Flat-tier pricing across quality with 4K support, T2I + I2I
- family: `GPT Image`
- capabilities: speed=medium, quality=superior, average_time_seconds=20, max_images_per_request=4, supports_4k=True, supports_quality_options=True, supports_multiple_resolutions=True
- aspect_ratio options: `1:1`, `4:3`, `3:4`, `16:9`, `9:16`
- resolution options: `1K`, `2K`, `4K`
- quality options: `low`, `medium`, `high`

#### `midjourney-v8.1`
Midjourney v8.1 - Latest Midjourney model with highest quality photorealistic and artistic image generation
- family: `Midjourney`
- capabilities: speed=medium, quality=excellent, average_time_seconds=30
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-v8.1-fast`
Midjourney v8.1 Fast - Latest Midjourney model with faster generation speed
- family: `Midjourney`
- capabilities: speed=fast, quality=excellent, average_time_seconds=15
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-v8.1-turbo`
Midjourney v8.1 Turbo - Latest Midjourney model with fastest generation speed
- family: `Midjourney`
- capabilities: speed=fast, quality=excellent, average_time_seconds=8
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-v7`
Midjourney v7 - Previous generation with proven photorealistic quality
- family: `Midjourney`
- capabilities: speed=medium, quality=excellent, average_time_seconds=30
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-v7-fast`
Midjourney v7 Fast - Previous generation with faster generation speed
- family: `Midjourney`
- capabilities: speed=fast, quality=excellent, average_time_seconds=15
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-v7-turbo`
Midjourney v7 Turbo - Previous generation with fastest generation speed
- family: `Midjourney`
- capabilities: speed=fast, quality=excellent, average_time_seconds=8
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-niji7`
Midjourney Niji 7 - Specialized anime and illustration style image generation
- family: `Midjourney`
- capabilities: speed=medium, quality=excellent, average_time_seconds=30
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-niji7-fast`
Midjourney Niji 7 Fast - Anime and illustration style with faster generation
- family: `Midjourney`
- capabilities: speed=fast, quality=excellent, average_time_seconds=15
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

#### `midjourney-niji7-turbo`
Midjourney Niji 7 Turbo - Anime and illustration style with fastest generation
- family: `Midjourney`
- capabilities: speed=fast, quality=excellent, average_time_seconds=8
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `4:3`, `3:4`
- quality options: `0.25`, `0.5`, `1`, `2`

## Video models — `generate_video`

#### `veo3.1`
Google Veo 3.1 - High-quality video generation
- family: `Google Veo 3.1`
- capabilities: max_duration=8s, default_duration=8s, default_aspect_ratio=16:9, default_resolution=720p, supports_audio=True, supports_hd=True
- aspect_ratio options: `9:16`, `16:9`, `1:1`
- resolution options: `720p`, `1080p`, `4k`
- duration options: `4s`, `6s`, `8s`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `reference-to-video`
- variant options: `standard`, `fast`, `lite`

#### `sora-2`
OpenAI Sora 2 - State-of-the-art video generation with audio
- family: `Sora 2`
- capabilities: max_duration=20s, default_duration=4s, default_aspect_ratio=16:9
- mode options: `text-to-video`, `image-to-video`

#### `sora-2-pro`
OpenAI Sora 2 Pro - Premium video generation (720p/1080p)
- family: `Sora 2`
- capabilities: max_duration=20s, default_duration=4s, default_aspect_ratio=16:9
- mode options: `text-to-video`, `image-to-video`

#### `wan-2.5`
Wan 2.5 Preview - Fast video generation with multiple resolutions
- family: `Wan`
- capabilities: max_duration=10s, default_duration=5s, default_aspect_ratio=16:9
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

#### `seedance-v1`
Seedance v1 - Multi-resolution video generation
- family: `Seedance`
- capabilities: max_duration=12s, default_duration=5s, default_aspect_ratio=16:9, default_resolution=720p
- duration options: `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `10`, `11`, `12`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `reference-to-video`
- variant options: `lite`, `pro`, `fast`

#### `hailuo-2.3`
Hailuo 2.3 standard - text and image to video with 1080p output. 1 cr/sec.
- family: `Hailuo`
- capabilities: default_duration=5s, default_aspect_ratio=16:9
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

#### `hailuo-2.3-pro`
Hailuo 2.3 Pro - premium text and image to video with enhanced quality at 1080p.
- family: `Hailuo`
- capabilities: default_duration=5s, default_aspect_ratio=16:9
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

#### `hailuo-02`
Hailuo 02 standard - text and image to video with selectable resolution (512p or 768p).
- family: `Hailuo`
- capabilities: default_duration=5s, default_aspect_ratio=16:9, default_resolution=768p
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- resolution options: `512p`, `768p`
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

#### `hailuo-02-fast`
Hailuo 02 Fast - rapid image-to-video generation.
- family: `Hailuo`
- mode options: `image-to-video`
- variant options: `standard`

#### `ltx-2`
LTX 2 - High-quality video generation with multiple resolutions
- family: `LTX 2`
- capabilities: max_duration=10s, default_duration=6s, default_aspect_ratio=16:9, default_resolution=1080p
- resolution options: `1080p`, `1440p`, `2160p`
- duration options: `6`, `8`, `10`, `12`, `14`, `16`, `18`, `20`
- mode options: `text-to-video`, `image-to-video`, `video-to-video`
- variant options: `pro`, `fast`

#### `kling-v2.6`
Kling 2.6 - High-quality video generation with native audio support
- family: `Kling`
- capabilities: max_duration=10s, default_duration=5s, default_aspect_ratio=16:9
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- duration options: `5`, `10`
- mode options: `text-to-video`, `image-to-video`
- variant options: `pro`

#### `wan-2.6`
Wan 2.6 - Alibaba's latest model with superior motion consistency, enhanced detail rendering, and multi-aspect ratio support
- family: `Wan`
- capabilities: max_duration=15s, default_duration=5s, default_aspect_ratio=16:9, default_resolution=1080p
- aspect_ratio options: `16:9`, `9:16`, `1:1`, `4:3`, `3:4`
- resolution options: `720p`, `1080p`
- duration options: `5`, `10`, `15`
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

#### `kling-v2.5-turbo`
Kling 2.5 Turbo - Fast video generation with pro quality
- family: `Kling`
- capabilities: max_duration=10s, default_duration=5s, default_aspect_ratio=16:9
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- duration options: `5`, `10`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`
- variant options: `standard`

#### `seedance-1.5-pro`
Seedance 1.5 Pro - High-quality video generation with native audio support from ByteDance
- family: `Seedance`
- capabilities: max_duration=12s, default_duration=5s, default_aspect_ratio=16:9, default_resolution=720p, supports_audio=True
- aspect_ratio options: `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16`
- resolution options: `480p`, `720p`, `1080p`
- duration options: `4`, `5`, `6`, `7`, `8`, `9`, `10`, `11`, `12`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`
- variant options: `standard`

#### `ltx-2-19b`
LTX 2-19B - High-quality video generation with camera control and native audio support
- family: `LTX`
- capabilities: supports_audio=True
- aspect_ratio options: `Auto`, `16:9`, `4:3`, `1:1`, `1:1 HD`, `3:4`, `9:16`
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`, `distilled`

#### `kling-o3`
Kling O3 - Top-tier video generation with cinematic visuals, fluid motion, and native audio
- family: `Kling`
- capabilities: max_duration=15s, default_duration=5s, supports_audio=True
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `reference-to-video`
- variant options: `standard`, `pro`

#### `kling-v3`
Kling V3 - Latest Kling video model with cinematic visuals and native audio
- family: `Kling`
- capabilities: max_duration=15s, default_duration=5s, supports_audio=True
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `reference-to-video`
- variant options: `standard`, `pro`, `4k`

#### `wan-2.6-flash`
Wan 2.6 Flash - Ultra-fast image-to-video generation with optional auto-audio
- family: `Wan`
- capabilities: max_duration=10s, default_duration=5s
- resolution options: `720p`, `1080p`
- duration options: `5`, `10`
- mode options: `image-to-video`
- variant options: `standard`

#### `grok-imagine-video`
Grok Imagine Video - xAI's video generation with native audio
- family: `Grok`
- capabilities: max_duration=15s, default_duration=6s, supports_audio=True
- aspect_ratio options: `16:9`, `4:3`, `3:2`, `1:1`, `2:3`, `3:4`, `9:16`
- resolution options: `480p`, `720p`
- mode options: `text-to-video`, `image-to-video`, `video-to-video`
- variant options: `standard`

#### `wan-2.7`
Wan 2.7 - Advanced video generation with audio support
- family: `Wan`
- capabilities: max_duration=15s, default_duration=5s, default_aspect_ratio=16:9, default_resolution=1080p, supports_audio=True
- aspect_ratio options: `16:9`, `9:16`, `1:1`, `4:3`, `3:4`
- resolution options: `720p`, `1080p`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `video-to-video`
- variant options: `standard`

#### `seedance-2.0`
Seedance 2.0 - ByteDance's flagship video model with native audio. T2V, I2V, R2V (image+video+audio refs).
- family: `Seedance`
- capabilities: max_duration=12s, default_duration=5s, default_aspect_ratio=16:9, default_resolution=720p, supports_audio=True
- aspect_ratio options: `auto`, `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16`
- resolution options: `480p`, `720p`, `1080p`, `4k`
- duration options: `4`, `5`, `6`, `7`, `8`, `9`, `10`, `11`, `12`, `13`, `14`, `15`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `reference-to-video`
- variant options: `standard`

#### `seedance-2.0-fast`
Seedance 2.0 Fast - faster, cheaper variant of Seedance 2.0. T2V, I2V, R2V.
- family: `Seedance`
- capabilities: max_duration=12s, default_duration=5s, default_aspect_ratio=16:9, default_resolution=720p, supports_audio=True
- aspect_ratio options: `auto`, `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16`
- resolution options: `480p`, `720p`
- duration options: `4`, `5`, `6`, `7`, `8`, `9`, `10`, `11`, `12`, `13`, `14`, `15`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `reference-to-video`
- variant options: `standard`

#### `seedance-2.0-mini`
Seedance 2.0 Mini - lightweight, cost-effective variant of Seedance 2.0. T2V, I2V, R2V.
- family: `Seedance`
- aspect_ratio options: `auto`, `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16`
- resolution options: `480p`, `720p`
- duration options: `4`, `5`, `6`, `7`, `8`, `9`, `10`, `11`, `12`, `13`, `14`, `15`
- mode options: `text-to-video`, `image-to-video`, `first-last-frame`, `reference-to-video`
- variant options: `standard`

#### `happy-horse-1.0`
Happy Horse 1.0 - 1080p video generation with synchronized native audio from text or image input.
- family: `Happy Horse`
- capabilities: max_duration=15s, default_duration=5s, default_aspect_ratio=16:9, supports_audio=True
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

#### `omni-flash-ext`
Gemini Omni-Flash - Multi-mode video generation with text, image, fusion, and reference-video support.
- family: `Omni`
- capabilities: max_duration=10s, default_duration=6s, default_aspect_ratio=16:9, default_resolution=720p
- aspect_ratio options: `16:9`, `9:16`
- resolution options: `720p`, `1080p`, `4k`
- duration options: `4`, `6`, `8`, `10`
- mode options: `text-to-video`, `image-to-video`, `reference-to-video`
- variant options: `standard`

#### `happyhorse-1.1`
Happy Horse 1.1 - High-quality video generation with text-to-video and image-to-video support
- family: `Happy Horse`
- resolution options: `720p`, `1080p`
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

#### `grok-imagine-video-1.5`
Grok Imagine Video 1.5 Preview - xAI's latest video generation model
- family: `Grok`
- aspect_ratio options: `1:1`, `16:9`, `9:16`, `3:2`, `2:3`, `auto`
- resolution options: `480p`, `720p`
- mode options: `image-to-video`
- variant options: `standard`

#### `kling-v3-turbo`
Kling V3 Turbo - Fast Kling video generation with resolution-based pricing
- family: `Kling`
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- resolution options: `720p`, `1080p`
- mode options: `text-to-video`, `image-to-video`
- variant options: `standard`

## Video edit / restyle models — `generate_edit`

#### `kling-v2.6`
Kling V2.6 - Motion control video generation with character transfer capabilities
- family: `Kling`
- mode options: `standard`, `pro`
- variant options: `standard`

#### `kling-v3-motion-control`
Kling V3 Motion Control - Transfer movements from reference video to character image
- family: `Kling`
- mode options: `standard`, `pro`
- variant options: `standard`

#### `grok-imagine-video`
Grok Imagine Video - Edit videos using xAI's Grok Imagine
- family: `Grok`
- resolution options: `480p`, `720p`
- mode options: `video-to-video-edit`
- variant options: `standard`

#### `kling-o3-standard-v2v`
Kling O3 Standard - Video-to-video editing and reference with element support
- family: `Kling`
- capabilities: max_duration=10s
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- duration options: `3`, `4`, `5`, `6`, `7`, `8`, `9`, `10`
- mode options: `video-to-video-edit`, `video-to-video-reference`
- variant options: `standard`

#### `kling-o3-pro-v2v`
Kling O3 Pro - Premium video-to-video editing and reference with element support
- family: `Kling`
- capabilities: max_duration=10s
- aspect_ratio options: `16:9`, `9:16`, `1:1`
- duration options: `3`, `4`, `5`, `6`, `7`, `8`, `9`, `10`
- mode options: `video-to-video-edit`, `video-to-video-reference`
- variant options: `pro`

#### `dreamactor-v2`
ByteDance Dreamactor v2 - Transfer motion from video to character image
- family: `ByteDance`
- mode options: `video-to-video`
- variant options: `standard`

#### `wan-2.6-flash`
Wan 2.6 Flash - Fast reference-to-video generation with multi-character support
- family: `Wan`
- aspect_ratio options: `16:9`, `9:16`, `1:1`, `4:3`, `3:4`
- resolution options: `720p`, `1080p`
- duration options: `5`, `10`
- mode options: `reference-to-video`
- variant options: `flash`

#### `wan-2.6`
Wan 2.6 video-to-video editing via reference videos (up to 3).
- family: `Wan`
- resolution options: `720p`, `1080p`
- duration options: `5`, `10`
- mode options: `video-to-video`
- variant options: `standard`

#### `wan-2.7`
Wan 2.7 - Video editing and reference-to-video generation
- family: `Wan`
- aspect_ratio options: `16:9`, `9:16`, `1:1`, `4:3`, `3:4`
- resolution options: `720p`, `1080p`
- duration options: `2`, `3`, `4`, `5`, `6`, `7`, `8`, `9`, `10`
- mode options: `video-to-video-edit`, `reference-to-video`
- variant options: `standard`

#### `happy-horse-1.0-edit`
Happy Horse 1.0 Edit - Reference-image-to-video and video-edit modes for stylized transformation and lipsync.
- family: `Happy Horse`
- capabilities: max_duration=15s, default_duration=5s, supports_audio=True
- aspect_ratio options: `16:9`, `9:16`, `1:1`, `4:3`, `3:4`
- resolution options: `720p`, `1080p`
- duration options: `3`, `4`, `5`, `6`, `7`, `8`, `9`, `10`, `11`, `12`, `13`, `14`, `15`
- mode options: `reference-to-video`, `video-edit`
- variant options: `standard`

#### `omni-flash-ext`
Gemini Omni-Flash - Video-to-video editing
- family: `Omni`
- aspect_ratio options: `16:9`, `9:16`
- resolution options: `720p`, `1080p`, `4k`
- mode options: `video-to-video`
- variant options: `standard`

## Lipsync / avatar models — `generate_lipsync`

#### `veo3.1-lipsync`
Google Veo 3.1 Lipsync - High-fidelity image animation with native audio generation
- family: `Google`
- capabilities: max_duration=8s, default_duration=8s, default_aspect_ratio=16:9, supports_audio=True, supports_hd=True
- aspect_ratio options: `auto`, `16:9`, `9:16`
- resolution options: `720p`, `1080p`, `4k`
- duration options: `4s`, `6s`, `8s`

#### `kling-ai-avatar`
Kling AI Avatar - Realistic lip sync with multilingual speech support
- family: `Kling`

#### `infinitalk-lipsync`
InfiniteTalk - Long-form talking avatars up to 10 minutes with singing support
- family: `InfiniteTalk`
- resolution options: `480p`, `720p`

#### `omnihuman`
OmniHuman - ByteDance's specialized model for human subjects and faces
- family: `ByteDance`

#### `seedance-v1.5`
Seedance 1.5 Pro - Cinematic quality with native audio generation
- family: `ByteDance`
- aspect_ratio options: `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16`
- resolution options: `480p`, `720p`, `1080p`
- duration options: `4`, `8`, `12`

#### `sync-lipsync-v2`
Sync Lipsync 2 - API-driven video dubbing for scalable production
- family: `Sync`

#### `kling-avatar-v2`
Kling Avatar v2 - Next-gen talking heads with improved expressions
- family: `Kling`

#### `kling-v2.6-lipsync`
Kling 2.6 Pro - Advanced I2V with audio generation
- family: `Kling`
- duration options: `5`, `10`

#### `wan-2.7-lipsync`
Wan 2.7 - Next-gen animated talking avatars with enhanced audio generation
- family: `Wan`
- capabilities: max_duration=15s, default_duration=5s
- resolution options: `720p`, `1080p`
- duration options: `5`, `10`

#### `seedance-2.0-lipsync`
Seedance 2.0 - Lip-sync video from image + audio via reference-to-video
- family: `ByteDance`
- capabilities: max_duration=15s, default_duration=5s
- aspect_ratio options: `21:9`, `16:9`, `4:3`, `1:1`, `3:4`, `9:16`, `adaptive`
- resolution options: `480p`, `720p`, `1080p`

#### `wan-2.5-lipsync`
Wan 2.5 - Animated talking avatars with audio generation
- family: `Wan`
- capabilities: max_duration=10s, default_duration=5s
- resolution options: `480p`, `720p`, `1080p`
- duration options: `5`, `10`

#### `wan-2.5-fast-lipsync`
Wan 2.5 Fast - Speed-optimized talking avatar generation
- family: `Wan`
- capabilities: max_duration=10s, default_duration=5s
- resolution options: `720p`, `1080p`
- duration options: `5`, `10`

#### `heygen-lipsync-v3`
HeyGen Lipsync v3 - Professional video lip-sync with speed and precision modes
- family: `HeyGen`

#### `p-video-avatar`
PrunaAI P-Video-Avatar - Fast and affordable avatar/lipsync video generation
- family: `PrunaAI`
- resolution options: `720p`, `1080p`

## Text-to-speech models — `generate_audio` (media_type `audio`)

#### `elevenlabs-tts-v3`
Eleven Labs TTS V3 - High-quality text-to-speech with emotion
- family: `ElevenLabs`
- voice options: `Aria`, `Roger`, `Sarah`, `Laura`, `Charlie`, `George`, `Callum`, `River`, `Liam`, `Charlotte`, `Alice`, `Matilda`, `Will`, `Jessica`, `Eric`, `Chris`, `Brian`, `Daniel`, `Lily`, `Bill`
- mode options: `text-to-speech`
- variant options: `standard`

#### `elevenlabs-tts-multilingual-v2`
Eleven Labs TTS Multilingual V2 - Multi-language text-to-speech
- family: `ElevenLabs`
- voice options: `Aria`, `Roger`, `Sarah`, `Laura`, `Charlie`, `George`, `Callum`, `River`, `Liam`, `Charlotte`, `Alice`, `Matilda`, `Will`, `Jessica`, `Eric`, `Chris`, `Brian`, `Daniel`, `Lily`, `Bill`
- mode options: `text-to-speech`
- variant options: `standard`

#### `elevenlabs-tts-turbo-v2.5`
Eleven Labs TTS Turbo V2.5 - Fast text-to-speech generation
- family: `ElevenLabs`
- voice options: `Aria`, `Roger`, `Sarah`, `Laura`, `Charlie`, `George`, `Callum`, `River`, `Liam`, `Charlotte`, `Alice`, `Matilda`, `Will`, `Jessica`, `Eric`, `Chris`, `Brian`, `Daniel`, `Lily`, `Bill`
- mode options: `text-to-speech`
- variant options: `turbo`

#### `minimax-speech-2.8-turbo`
Minimax Speech 2.8 Turbo - Fast multilingual TTS with emotion control
- family: `Minimax`
- mode options: `text-to-speech`
- variant options: `turbo`

#### `minimax-speech-2.8-hd`
Minimax Speech 2.8 HD - High-quality multilingual TTS with advanced controls
- family: `Minimax`
- mode options: `text-to-speech`
- variant options: `hd`

#### `qwen3-tts-0.6b`
Qwen3-TTS 0.6B - Fast text-to-speech with custom voice cloning support
- family: `Qwen`
- voice options: `Vivian`, `Serena`, `Uncle_Fu`, `Dylan`, `Eric`, `Ryan`, `Aiden`, `Ono_Anna`, `Sohee`
- mode options: `text-to-speech`
- variant options: `0.6b`

#### `cartesia-sonic`
Cartesia Sonic 3.5 - High-fidelity fast TTS with instant voice cloning
- family: `Cartesia`

#### `minimax-voice-clone`
Minimax Voice Clone - Clone any voice and generate speech in one step
- family: `Minimax`
- mode options: `text-to-speech`
- variant options: `standard`

#### `qwen3-tts-1.7b`
Qwen3-TTS 1.7B - High-quality text-to-speech with custom voice cloning support
- family: `Qwen`
- voice options: `Vivian`, `Serena`, `Uncle_Fu`, `Dylan`, `Eric`, `Ryan`, `Aiden`, `Ono_Anna`, `Sohee`
- mode options: `text-to-speech`
- variant options: `1.7b`

## Music models — `generate_audio` (media_type `audio`)

#### `minimax-music-v2`
Minimax Music V2 - AI music generation with vocals
- family: `Minimax`
- mode options: `text-to-music`
- variant options: `standard`

#### `elevenlabs-music`
Eleven Labs Music - Advanced AI music generation with composition control
- family: `ElevenLabs`
- mode options: `composition-to-music`
- variant options: `standard`

#### `seed-audio-1.0`
Seed Audio 1.0 - ByteDance's versatile audio generation model. Text-to-audio with optional voice cloning via reference audio or image input.
- family: `Seed Audio`
- mode options: `text-to-audio`
- variant options: `standard`

## Sound-effect models — `generate_audio` (media_type `audio`)

#### `elevenlabs-sound-effects-v2`
Eleven Labs Sound Effects V2 - AI-powered sound effect generation
- family: `ElevenLabs`
- mode options: `text-to-sound`
- variant options: `standard`

#### `beatoven-sound-effect`
Beatoven Sound Effect Generation - Creative AI sound effects
- family: `Beatoven`
- mode options: `text-to-sound`
- variant options: `standard`

## Apps — `describe_app` / `generate_app`

Apps take two dicts: `inputs` (media/product fields — must be fetchable
URLs; use `get_upload_url` to stage local files) and `parameters` (tuning).
Always call `describe_app(app_name)` first for the live contract.

#### `adgen` — Adgen
Generate product advertisement videos from images using AI
- kind: output=video
- required inputs: `product_image_1`, `product_image_2`, `product_image_3`, `product_description`
- optional inputs: `logo`, `avatar_image`, `avatar_voice`, `brand_colors`, `template`, `aspect_ratio`, `custom_instruction`, `product_name`
- URL/upload inputs: `product_image_1`, `product_image_2`, `product_image_3`, `logo`

#### `link-2-ad` — Link 2 Ad
Generate product advertisement videos from images using AI
- kind: workflow, output=video
- required inputs: `product_image_1`, `product_image_2`, `product_image_3`, `product_description`
- optional inputs: `logo`, `brand_colors`, `template`, `aspect_ratio`, `custom_instruction`
- URL/upload inputs: `product_image_1`, `product_image_2`, `product_image_3`, `logo`

#### `recast` — Recast
Swap characters in any video with a single image
- kind: output=video
- required inputs: `image_url`, `video_url`
- optional inputs: `prompt`
- URL/upload inputs: `image_url`, `video_url`

#### `transitions` — Transitions
Generate smooth AI transitions between a first and last frame (supports image or video uploads)
- kind: output=video
- required inputs: `first_frame_url`, `last_frame_url`
- optional inputs: `prompt`
- URL/upload inputs: `first_frame_url`, `last_frame_url`

#### `ad-variation` — Ad Variations
Generate 4-5 AI video variations from a single ad video
- kind: pipeline, workflow, output=video
- required inputs: `source_video_url`
- optional inputs: `archetype`, `custom_instructions`, `main_character`, `resolution`
- URL/upload inputs: `source_video_url`

#### `shots` — Shots
Generate 9 cinematic storyboard shots from a single photo
- kind: pipeline, output=image
- required inputs: `image_url`
- URL/upload inputs: `image_url`

#### `upscale` — Upscale
AI-powered image and video upscaling with Topaz technology
- kind: output=image
- required inputs: `mode`
- optional inputs: `image_url`, `video_url`, `upscale_factor`
- URL/upload inputs: `image_url`, `video_url`

#### `upscale-advanced` — Upscale (Advanced)
Advanced AI upscaling with full Topaz model selection and fine-tuning controls
- kind: output=image
- required inputs: `mode`
- optional inputs: `image_url`, `video_url`, `upscale_factor`, `model`, `output_format`, `subject_detection`, `face_enhancement`, `face_enhancement_strength`, `face_enhancement_creativity`, `sharpen`, `denoise`, `fix_compression`, `crop_to_fill`, `strength`, `creativity`, `texture`, `prompt`, `autoprompt`, `detail`, `target_fps`, `compression`, `noise`, `halo`, `grain`, `recover_detail`, `H264_output`
- URL/upload inputs: `image_url`, `video_url`

#### `house-tour` — House Tour
Generate cinematic walkthrough videos from up to 7 house images, optionally with a tour-guide avatar
- kind: output=video
- required inputs: `image_urls`
- optional inputs: `avatar_url`, `avatar_preview_url`, `avatar_scrambled`
- array inputs (pass as lists): `image_urls`
- URL/upload inputs: `image_urls`, `avatar_url`, `house_plan_url`

#### `video-translate` — Video Translate
Translate any video into 175+ languages with AI voice cloning
- kind: output=video
- required inputs: `video_url`, `output_language`
- optional inputs: `title`, `translate_audio_only`, `speaker_num`, `enable_dynamic_duration`
- URL/upload inputs: `video_url`

#### `brainrot` — Brainrot
Generate brainrot-style educational videos with Family Guy characters
- kind: pipeline, output=video
- required inputs: `topic`
- optional inputs: `characters`, `background_type`, `target_duration`

#### `angles` — Angles
Generate different views and angles of any photo using AI
- kind: output=image
- required inputs: `image_urls`
- array inputs (pass as lists): `image_urls`
- URL/upload inputs: `image_urls`

#### `smartshot-sheet` — SmartShot Sheet
Generate a character sheet + refined cinematic prompt from cast + scene description (gpt-image-2). Step 1 of the SmartShot pipeline.
- kind: pipeline, output=image
- required inputs: `user_prompt`
- optional inputs: `character_image_urls`, `existing_sheet_url`, `env_image_url`, `character_names`
- URL/upload inputs: `character_image_urls`, `env_image_url`, `existing_sheet_url`

#### `smartshot` — SmartShot
Multi-cut cinematic video from a character sheet + refined cinematic prompt (doubao-seedance-2.0. Step 2 of the SmartShot pipeline.
- kind: pipeline, output=video
- required inputs: `sheet_image_url`, `refined_prompt`
- optional inputs: `sheet_request_id`
- URL/upload inputs: `sheet_image_url`

#### `story-mode` — Story Mode
Turn scripts into AI-generated short films with characters, dialogue, and cinematic shots
- kind: workflow, output=video
- required inputs: `script`
- optional inputs: `style_hint`

#### `resize` — Smart Resize
Outpaint an image to a target size with seamless AI fill
- kind: output=image
- required inputs: `image_url`, `target_sizes`
- optional inputs: `prompt`
- array inputs (pass as lists): `target_sizes`
- URL/upload inputs: `image_url`
