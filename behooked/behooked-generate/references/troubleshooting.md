# Troubleshooting

## Tools aren't available / not connected
The BeHooked MCP isn't connected — it's a separate one-time setup from the skill. Add it once:
```
claude mcp add --transport http behooked https://mcp.behooked.ai/mcp
```
Then complete the OAuth sign-in on the first generation call.

## `account_required`
The connected login has no BeHooked plan yet. Someone can OAuth-connect before ever setting up BeHooked.
Tell the user to sign in and pick a plan at **behooked.ai**, then continue right here — **no reconnect
needed**. Nothing was charged. Don't retry generations until the balance resolves. Call
`get_credit_balance` early in a session to catch this before spending a turn on setup.

## `concurrency_limit`
Too many generations are running at once for the user's plan. Wait for a running job to finish, then
retry. Nothing was charged.

## Job comes back `failed` / a submit errors
No credits were charged (media charges refund on failure). Report the failure plainly. Common causes:
- **Moderation / NSFW / safety block** — the provider rejected the prompt or input. Rephrase or change
  the image; this short-circuits provider fallback, so a retry with the same content will fail again.
- **Bad params** — you skipped `validate_params`. Re-run it, fix the errors, regenerate.
- **Transient provider error** — retry with the **same** `idempotency_key`.

## Validation errors
`validate_params` lists exactly what's wrong (unknown key, value not in `allowed_values`, missing
required param). Fix each and re-validate before generating. Don't force a generate around a validation
error — it will be rejected or waste a charge.

## Wrong aspect ratio / size
Different models name sizes differently (canonical `16:9` vs preset `landscape_16_9` vs pixels
`1536x1024`). Use the value from that model's `parameter_validation` / the catalog, not a value from a
different model.

## Long waits
Video, edit, and lipsync jobs can take several minutes (sometimes 20+). Set expectations from the
`time_estimate` before polling, and tell the user they can keep working; the job keeps running.

## Billing / plans / buying credits
There are no tools for payments, upgrades, or top-ups — these are **web-only**. `get_credit_balance`
can report the balance, but changing it happens at behooked.ai. Route the user there.

## A feature exists on the web but not here
Some capabilities (e.g. certain pipeline apps marked `runnable:false` by `list_apps`) aren't exposed
over MCP yet. Say it's available on behooked.ai and MCP support is planned — don't imply it failed.
