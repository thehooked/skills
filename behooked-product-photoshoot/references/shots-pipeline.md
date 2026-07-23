# shots — the pipeline app

`shots` is a pipeline app: it orchestrates multiple internal stages to turn one photo into 9 cinematic
shots. You don't manage the stages — you submit once and poll.

## Running it
```
describe_app("shots")     # contract + pricing block (credits) + time_estimate
validate_app_inputs("shots", {"image_url": "<url>"})
generate_app("shots", inputs={"image_url": "<url>"}, parameters={"aspect_ratio": "1:1"}, idempotency_key)
await_app_result(request_id)   # blocks until the pipeline finishes -> 9 image urls
```

## Pricing quirk for pipeline apps
`estimate_app_cost` **raises** for pipeline apps like `shots` — there's no per-second/per-item figure to
sum. Instead, read the completion charge (in credits) from `describe_app("shots")`'s pricing block and
state that to the user before generating.

## Polling
- `await_app_result(request_id)` waits for the whole pipeline; it can take a while (set expectations
  from `time_estimate`).
- `get_app_result(request_id)` is a one-shot status check if you'd rather poll yourself.
- `list_app_jobs(app_name="shots")` finds recent runs if you lost the `request_id`.

## Notes
- Bills only on success — no charge if the pipeline fails.
- Reuse the same `idempotency_key` on a retry so a resend doesn't double-charge.
