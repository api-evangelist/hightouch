---
name: Build a warehouse-to-destination sync
description: Stand up the full Hightouch chain — source, model, destination, sync — and run it once.
api: openapi/_original/hightouch-api-openapi.json
operations:
  - ListSource
  - CreateSource
  - ListModel
  - CreateModel
  - ListDestination
  - CreateDestination
  - CreateSync
  - TriggerRun
  - ListSyncRuns
generated: '2026-08-13'
method: generated
---

# Build a warehouse-to-destination sync

Stand up the full Hightouch chain — source, model, destination, sync — and run it once.

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

1. **Find or create the source.** `ListSource` (filter with `slug` or `name`) to see whether the warehouse is
   already connected. Only call `CreateSource` if it is not — a duplicate source means duplicate warehouse
   compute. `Source.id` is a number.
2. **Define the dataset.** `ListModel` filtered by `sourceId`, then `CreateModel` if needed. A model needs a
   `sourceId`, a `primaryKey`, and exactly one query body: `raw`, `table`, `dbt`, `dbt_cloud`, `visual` or
   `custom` — `queryType` says which one you used. The primary key must be unique or the first run fails with
   `NON_UNIQUE_PRIMARY_KEY`.
3. **Find or create the destination.** `ListDestination`, then `CreateDestination` with the connector `type` and
   its `configuration`.
4. **Create the sync.** `CreateSync` with `modelId`, `destinationId`, the field `configuration`, and a
   `schedule` (interval, cron, visual cron, or dbt). Leave `schedule` off for a trigger-only sync.
5. **Run it.** `TriggerRun` with the sync id. This is not idempotent.
6. **Confirm.** `ListSyncRuns` for the sync and read `status`, `successfulRows`, `failedRows` and `error`.
   On failure, resolve the platform error code before re-triggering.
