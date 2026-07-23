# Batch ad variations

`link-2-ad` and `adgen` are batch-capable: render several ads across creative templates in one
submission with `generate_app_batch`.

## How it works
- `template_counts` is a map of `template -> how many` to render, e.g.
  `{"unboxing": 2, "viral": 1, "luxury": 1}` → 4 ads total.
- The same `inputs` (product images/description) and base `parameters` apply to every ad; the template
  varies per the counts.

## Flow
```
# prepare inputs once (scrape for link-2-ad, or upload for adgen)
describe_app(app_name)
estimate_app_cost(app_name, parameters={...}, inputs={...}, template_counts={...})  # covers ALL ads
generate_app_batch(app_name, template_counts={...}, inputs={...}, parameters={...}, idempotency_key)
get_app_batch(batch_id)   # poll the batch -> per-ad output_urls
```

## Cost
Pass `template_counts` to `estimate_app_cost` so the figure is the **total** (per-ad cost × counts).
State that total in your reply before generating — the user is approving the whole batch.

## Notes
- Poll the batch with `get_app_batch(batch_id)`; it reports each ad's status/URL as they complete.
- Bills only on success (per ad). Set time expectations — a batch takes longer than a single ad.
- Confirm the batch-capable app list and per-app template options from `list_apps` / `describe_app`.
