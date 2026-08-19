---
name: Operate an AI Decisioning flow
description: Inspect, extend and run a Hightouch AI Decisioning flow and its message variants.
api: openapi/_original/hightouch-api-openapi.json
operations:
  - ListFlows
  - GetFlow
  - ListMessages
  - GetMessage
  - CreateMessage
  - UpdateMessage
  - RunFlow
generated: '2026-08-13'
method: generated
---

# Operate an AI Decisioning flow

Inspect, extend and run a Hightouch AI Decisioning flow and its message variants.

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

1. **Find the flow.** `ListFlows`, then `GetFlow` for the one you want. Note `status`, `decisionEngineId` and
   `audienceId` — the audience is a Customer Studio object the REST API does not expose, so treat it as opaque.
2. **Review the message set.** `ListMessages` for the flow, `GetMessage` for detail. Each message carries
   `channelId`, `config`, `variables` and `guardrails`.
3. **Add a variant.** `CreateMessage` with the channel and config. `guardrails` are what stop the engine sending
   something it should not — set them on every new message, not afterwards.
4. **Adjust.** `UpdateMessage` (PATCH) to change copy, variables or guardrails without recreating the variant.
5. **Run.** `RunFlow` executes the flow. Not idempotent — a second call is a second run. `RunFlow` declares a
   429, so honour backoff.
