---
name: Trigger a sync run and monitor it to completion
description: Kick off a Hightouch sync from an orchestrator by id or slug and poll it safely to a terminal state.
api: openapi/_original/hightouch-api-openapi.json
operations:
  - TriggerRun
  - TriggerRunCustom
  - ListSyncRuns
  - GetSync
  - TriggerSequenceRun
  - GetSyncSequenceRun
generated: '2026-08-13'
method: generated
---

# Trigger a sync run and monitor it to completion

Kick off a Hightouch sync from an orchestrator by id or slug and poll it safely to a terminal state.

## Ground rules for every Hightouch API call

- Base URL is `https://api.hightouch.com/api/v1`. TLS 1.2 or later is required.
- Authenticate with `Authorization: Bearer <HIGHTOUCH_APIKEY>`. The key is a workspace API key created by an
  Admin user under Settings > API keys, and it authenticates AS that user — if the creator is deactivated or
  removed during an SSO migration the key returns `401 {"message":"Authentication error"}`.
- There is **no idempotency key**. Re-issuing a trigger can start a second run. Before retrying a trigger,
  read the run list and confirm whether the first attempt landed.
- Rate limit is 200 requests per 10 seconds per workspace, and the API returns **no** rate-limit headers.
  Back off on `429` (body `{"error": "..."}`); you cannot read remaining quota.
- List operations page with `offset` and `limit` (default 20; 100 on run lists) and sort with `orderBy` —
  the allowed `orderBy` values differ per operation, so read the spec for the one you are calling.
- Watch identifier types: `sourceId`, `modelId`, `destinationId` and `/syncs/{syncId}` are **numbers**, while
  `/syncs/{syncId}/runs`, the trigger routes, and every campaign / flow / contract / domain / graph id are
  **strings**.
- Errors are not RFC 9457. Expect `{"message": "...", "details": {...}}` on 409/422 and `{"error": "..."}` on
  400/404/409/429. Sync-level failures carry a platform error code — look it up in
  `errors/hightouch-error-codes.yml`.

## Steps

1. **Check the sync is runnable.** `GetSync` and confirm `disabled` is false. Note `lastRunAt`.
2. **Trigger.** Use `TriggerRunCustom` when your orchestrator keys on a stable `slug` instead of a numeric id;
   use `TriggerRun` when you already hold the sync id. Pass `fullResync` only when you intend to replay the
   whole model — it re-sends every row.
3. **Do not blind-retry.** There is no idempotency key. If the trigger call times out, call `ListSyncRuns` with
   a tight `within` or `after` window and see whether a run already started before triggering again.
4. **Poll.** `ListSyncRuns` with `limit: 1` and `orderBy: created_at`. Poll no faster than the 200-requests /
   10-seconds workspace budget allows, and remember that budget is shared with everything else using the key.
5. **Read the outcome.** `status`, `completionRatio`, `plannedRows`, `successfulRows`, `failedRows`, `error`.
   A run can succeed with rejected rows — check `failedRows`, not just `status`.
6. **Sequences.** For an ordered set of syncs use `TriggerSequenceRun`, then poll `GetSyncSequenceRun` with the
   returned sequence-run id (a string).
