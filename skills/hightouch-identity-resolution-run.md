---
name: Run and reprocess an identity graph
description: Trigger a Hightouch identity-resolution run, watch it, and queue records for reprocessing.
api: openapi/_original/hightouch-api-openapi.json
operations:
  - TriggerIdrRun
  - ListIdrRuns
  - TriggerRunIdGraph
  - QueueForReprocessing
  - ReprocessStatus
generated: '2026-08-13'
method: generated
---

# Run and reprocess an identity graph

Trigger a Hightouch identity-resolution run, watch it, and queue records for reprocessing.

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

1. **Trigger.** `TriggerIdrRun` with the `graphId` (string). Pass `fullRerun` only when you mean to rebuild the
   whole graph — an incremental run is the normal path and far cheaper.
2. **Watch.** `ListIdrRuns` for the graph; each run carries `status`, `stats`, `startedAt`, `finishedAt` and
   `error`. `IdrRunStatsByThreshold` in the stats tells you how the match thresholds behaved — read it before
   trusting a new graph configuration.
3. **Reprocess a subset.** `QueueForReprocessing` returns a `requestId`; poll `ReprocessStatus` with that id
   rather than re-queuing.
4. **Legacy route.** `TriggerRunIdGraph` (`/id_graphs/{graphId}/trigger`) is the older trigger path and still
   present in the spec; prefer `TriggerIdrRun` for new automation.
