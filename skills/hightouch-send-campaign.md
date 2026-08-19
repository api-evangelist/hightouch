---
name: Trigger a campaign send and confirm delivery
description: Send a Hightouch campaign to specific recipients and read back the per-send status.
api: openapi/_original/hightouch-api-openapi.json
operations:
  - TriggerCampaign
  - GetSendStatus
generated: '2026-08-13'
method: generated
---

# Trigger a campaign send and confirm delivery

Send a Hightouch campaign to specific recipients and read back the per-send status.

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

1. **Trigger.** `TriggerCampaign` with the `campaignId` (string) and a `StartCampaignRequest` body. Recipients
   are either a `HandleCampaignRecipient` (an address/handle you supply) or a `ProfileCampaignRecipient` (a
   profile already in the warehouse) — pick one shape per recipient and do not mix fields.
2. **Capture the send id.** The `StartCampaignResponse` returns the send identifier. Persist it; without it you
   cannot check delivery, and there is no list-sends operation to recover it from.
3. **Confirm.** `GetSendStatus` with `campaignId` + `sendId` returns the `CampaignSendResult`.
4. **Failure modes.** 400/404/409/429 all return `{"error": "..."}`. A 409 usually means the send is already in
   flight — check status before re-triggering, because a second trigger is a second send to a real person.
