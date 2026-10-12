---
version: 0.1.0
name: behooked-talking-head
description: |
  Make a talking-head video (a presenter speaking your script, with b-roll scenes and captions) with
  BeHooked Studio's live MCP. You write the script with the user, they pick a presenter, they approve
  the scene layout and its exact cost, and the finished video comes back.
  Use when: "make a talking-head video", "have an avatar say this script", "presenter video about X",
  "UGC-style video with a speaker and b-roll", "spokesperson video for my product".
  NOT for: plain lipsync on your own clip (use behooked-generate), product ads from a link
  (use behooked-ads), house tours (use behooked-house-tour), or billing (web-only).
argument-hint: "[topic or script] [--quality base|good|great] [--captions <style>]"
allowed-tools: mcp__behooked__*
---

# BeHooked — Talking Head

A presenter (an "avatar") speaks a script you write together with the user. BeHooked adds the voice,
b-roll images and videos, captions and background music, and renders a vertical video.

> Tools written unprefixed; your client may show `mcp__behooked__<tool>`. The MCP must
> be connected (see behooked-generate Step 0). `user_id` is never an input.

## The tools
| Tool | Charges? | What it does |
|---|---|---|
| `list_talking_head_avatars` | no | The presenters this account can use (library + their own), with `preview_url` and `usable` |
| `estimate_talking_head` | no | Validates the request **and** estimates its cost (this is the estimate *and* validate step) |
| `start_talking_head` | yes | Creates the project from your script and starts the voice |
| `check_talking_head` | yes (only steps already stated) | Moves the project forward; stops for approval; returns the final video |
| `approve_talking_head` | yes | Approves the layout the user was shown, at the exact cost they saw |
| `list_talking_head_jobs` | no | Finds earlier projects so you can continue one |

## Mandatory workflow
1. **Write the script with the user** in the chat, and get their OK. About **3.2 spoken words per
   second**; the speech must be **5–180 seconds**. Write it to be spoken: short sentences, a hook first,
   a clear call to action at the end.
2. **Pick a presenter** — `list_talking_head_avatars`; show the previews (`preview_url`) and let the user
   choose. Only `usable: true` avatars can be started.
3. **Estimate + validate + say the number** — `estimate_talking_head(avatar_id, script, …)`. Fix every
   entry in `errors`. Then **state `before_approval_credits`** in your reply, and say that the b-roll and
   the avatar video are priced exactly when the layout is ready, and need their approval then.
4. **Start** — `start_talking_head(…same inputs…, idempotency_key)`. Reuse the key on a retry.
5. **Check until approval** — call `check_talking_head(job_id, wait_s=…)` until `status` is
   `awaiting_approval`.
6. **Show the layout and ask** — list every scene in `layout_review.scenes` (time, image or video,
   the phrase it covers) and `layout_review.approve_credits`. Ask the user to approve.
7. **Approve** — only after a yes: `approve_talking_head(job_id, expected_credits=<approve_credits>)`.
   If the cost changed, it is refused — show the new figure and ask again.
8. **Check until done** — `check_talking_head` until `status` is `done`; give the user `final_video_url`.

```
(script agreed in chat)
list_talking_head_avatars                       # user picks from previews
estimate_talking_head(avatar_id, script)        # fix errors; SAY before_approval_credits
start_talking_head(avatar_id, script, idempotency_key)
check_talking_head(job_id, wait_s=600)          # repeat until awaiting_approval
# show scenes + approve_credits, get a yes
approve_talking_head(job_id, expected_credits)
check_talking_head(job_id, wait_s=600)          # repeat until done -> final_video_url
```

## Options (defaults in brackets)
- `avatar_quality` — `low` (Base), `medium` (Good) **[default]**, `high` (Great). Higher looks better
  and costs more per second of speech.
- `voice_speed` — 0.6–1.5 **[1.2]**.
- `caption_type` — **[`advanced-tiktok`]**; other classic styles, `none`, or `dc:<style>`. An invalid id
  returns the full list in `errors`.
- `style` — `full` **[default]** (b-roll full screen) or `splits` (adds split-screen scenes).
- `music` — on **[default]** or off.

## UX rules
- **Never call `start_talking_head` or `approve_talking_head` as the first action.** Script, presenter,
  estimate, stated cost — then start. Layout shown, user said yes — then approve.
- **The approval is the big charge** (all b-roll + the avatar video). Always show every scene and the
  exact `approve_credits` first. If the user says no, stop — nothing more is charged.
- A whole video usually takes several minutes and can take longer. Tell the user they can keep working;
  call `check_talking_head` with `wait_s` up to 600.
- **Failures:** Talking Head charges each step as it starts. If a step fails, **that step is refunded**
  (earlier finished steps are not). `check_talking_head` returns `error.phase` and `error.retry_cost` —
  tell the user, and retry with `check_talking_head(job_id, retry=true)` only if they agree.
- `concurrency_limit` → too many generations running for their plan; wait for one to finish, retry.
  `insufficient_credits` at start → the project is kept as a draft; they top up at behooked.ai, then
  `check_talking_head` continues it.
- To change scenes, upload their own b-roll, or pick music, the user opens `website_url` — the same
  project is on the website.
- Return the finished video URL; don't dump job ids or raw status objects.

## References
- [references/talking-head.md](references/talking-head.md) — statuses, the layout review, retries,
  resuming a project, and script-writing tips.
