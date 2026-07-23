# Prompt engineering per media type

General: describe the **subject, then the details** (composition, lighting, mood, style), then
technical constraints. Keep one clear intent per generation. Put format/size/duration in `params`, not
the prompt.

## Image
- Lead with the subject and action, then setting, lighting, lens/composition, and style.
- For legible text in an image, name the exact text in quotes and pick a strong text model
  (`gpt-image-2`). State placement ("centered", "top banner").
- For product/photoreal: specify surface, background, lighting (softbox, natural), and camera angle.
- Negative intent ("no people", "plain background") works better stated positively ("empty studio
  backdrop").
- Set `num_images` to get variations in one call when the model supports it.

## Video
- Describe the shot as a single continuous action; avoid cramming multiple scene changes into one clip.
- Note camera motion ("slow dolly in", "static tripod"), pacing, and subject motion.
- For image-to-video, the prompt describes the **motion** to apply to the provided still.
- If the model supports native audio (`generate_audio` param on video models), describe the desired
  sound/dialogue; otherwise generate audio separately.

## Audio
- **TTS:** put the exact words to speak where the model expects them (usually `params._prompt_text`).
  Keep punctuation natural — it drives pacing. Pick voice/style via model params.
- **Music:** describe genre, mood, instrumentation, tempo, and energy arc. Give a duration in `params`.
- **SFX:** describe the single sound event concisely ("heavy wooden door creaking open, close mic").

## Edit / restyle
- State the target style/look and what to preserve ("keep the subject and motion, restyle to
  watercolor"). Provide the source video URL as the model's input.

## Lipsync
- Provide a clear, front-facing face image/video and a clean voice/audio track. The prompt is usually
  minimal; the inputs carry the work.

When results miss, change one variable at a time (model, then prompt specificity, then params) so you
can tell what moved the needle.
