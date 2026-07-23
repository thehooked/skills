# Workflows

## Canonical single generation

```
describe_model(media_type, model)          # learn params + allowed values
-> build params{}
estimate_cost(media_type, model, params)   # then STATE the credit cost to the user
validate_params(media_type, model, params) # fix errors until clean
generate_<media>(model, prompt, params, idempotency_key)
await_result(request_id)                   # -> output_url
```

Rules the server enforces (don't fight them):
- Never call a `generate_*` tool as the first action.
- Never generate before `validate_params` returns no errors **in this turn**.
- Never generate before you've stated the credit cost in your visible reply.

## Polling

- `await_result(request_id, timeout, poll_interval)` blocks until done or timeout (timeout capped at
  3600s). Prefer it for a single job.
- `get_result(request_id)` is a one-shot status read; use it for a quick check or in your own loop.
- `list_jobs` shows recent submissions if you lost a `request_id`.
- Set expectations first via the `time_estimate` from `describe_model`: image ~20s; video / edit /
  lipsync can run minutes. Tell the user they can keep working meanwhile.

## Chaining

- **media → media** the user already asked for as one step (e.g. generate an image, then animate it):
  feed the completed `output_url` straight into the next tool's input. Fine to do without stopping.
- **media → app** (a charged app step): first show the user the intermediate `output_url`(s) and get an
  explicit go-ahead before running the app — they may want to regenerate or pick a specific result.

## Idempotency & retries

- Put an `idempotency_key` on every `generate_*` call. On a transient failure, retry with the **same**
  key — the server replays the original submit and does not double-charge.
- A brand-new key means a brand-new (charged) generation.

## Cost & quality

The user sees **credits only** — never a money figure. When several models/tiers would satisfy the
goal, compare their credit costs and prefer the cheaper one when quality is comparable. Say the number
before charging.

## Failure semantics

If a job comes back `failed` (or a submit errors), tell the user **no credits were charged** — media
charges are refunded on failure. Only say this on an actual failure; never imply a refund on success.
