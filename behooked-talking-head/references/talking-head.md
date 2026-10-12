# Talking Head — reference

## How a project moves
`start_talking_head` creates the project and starts the voice. After that, every
`check_talking_head` call reads the project and presses the next step as soon as it is ready:

| `status` | `step` | Meaning | What you do |
|---|---|---|---|
| `draft` | `voice` | The voice has not started (e.g. the account was short of credits) | After a top-up, call `check_talking_head` |
| `running` | `voice` / `layout` / `assets` / `compose` | Work is in progress | Call `check_talking_head` again (`poll_after_s` is a hint) |
| `awaiting_approval` | `approval` | The layout is ready | Show `layout_review`, ask, then `approve_talking_head` |
| `done` | `done` | Finished | Give the user `final_video_url` |
| `failed` | the failed step | A step failed and was refunded | Tell the user `error.message` + `error.retry_cost`; retry only on a yes |

`check_talking_head` never approves and never retries on its own. If the agent stops calling it,
nothing more is charged — the project waits, and any later `check_talking_head` (or the website)
picks it up again.

## The layout review
At `awaiting_approval`, `layout_review` holds:
- `scenes` — one per b-roll scene: `time` (e.g. `0:03.2-0:06.7`), `kind` (`image` or `video`),
  `phrase` (the words it covers), `description` (what it will show), `cost`.
- `approve_credits` — the exact total charged on approval (all scenes + the avatar video).
- `breakdown` — image count/credits, video count/credits, avatar credits.
- `voice_seconds`, `presenter_only_seconds` — speech length and the time with no b-roll.

Show it as a short table plus the total. Pass `approve_credits` unchanged as `expected_credits`.

## Retries
`error.phase` tells you what failed: `audio` (voice), `transcript`, `layout`, `avatar`, `assets`
(one or more scenes), or `compose` (captions/render). `check_talking_head(job_id, retry=true)` presses
the matching retry once — for `assets`, every failed scene — and then keeps the project moving.

## Resuming
`list_talking_head_jobs` lists the user's projects (newest first) with `status` and `website_url`.
Continue any of them with `check_talking_head(job_id)`.

## Writing the script
- Aim for **3.2 words per second**: ~30 s ≈ 95 words, ~60 s ≈ 190 words. Keep it between 5 and 180
  seconds of speech.
- Open with a hook in the first sentence; one idea per sentence; end with a call to action.
- Write numbers and abbreviations the way they should be spoken; avoid long lists and parentheses.
- Show the user the full script and get their OK before starting — the voice is charged at start.

## XML export (Premiere / DaVinci)
Only when the user asks, and only for a `done` project: `export_talking_head_xml(job_id, wait_s)`.
- `status: ready` gives `xml_zip_url`, a permanent link to a large zip (timeline `.xml`, presenter, voice,
  b-roll, `captions.srt`, `captions.mov`, `HOW_TO_IMPORT.txt`). **Hand over the link only.**
- `status: running` means it's still building (usually a few minutes); call again. It never starts a second export.
- `status: failed` means calling it again retries. If the video changed after rendering, finish it with
  `check_talking_head` first.
- Importing: Premiere Pro **File > Import**; DaVinci Resolve **File > Import > Timeline** with
  **Use sizing information** ticked.
