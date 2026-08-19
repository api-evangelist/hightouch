---
name: Govern first-party event schemas
description: Create and maintain Hightouch Events contracts and domains so undeclared events are handled deliberately.
api: openapi/_original/hightouch-api-openapi.json
operations:
  - ListContracts
  - GetContract
  - CreateContract
  - UpdateContract
  - ListDomains
  - GetDomain
  - CreateDomain
  - UpdateDomain
generated: '2026-08-13'
method: generated
---

# Govern first-party event schemas

Create and maintain Hightouch Events contracts and domains so undeclared events are handled deliberately.

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

1. **Inventory.** `ListDomains` then `ListContracts` to see the event governance already in place. Both use
   string ids.
2. **Create the domain.** `CreateDomain` groups related contracts; its `components` array holds the contract
   references and `eventSources` binds it to the sources that emit.
3. **Declare the contract.** `CreateContract` with the `events` schema declaration and, critically,
   `onUndeclaredSchema` — this decides what happens to an event the contract does not describe. Set it
   deliberately; the default is a governance decision, not a detail.
4. **Evolve, do not replace.** `UpdateContract` / `UpdateDomain` (PATCH) when the schema changes, so existing
   `eventSources` bindings survive.
5. **Verify.** `GetContract` / `GetDomain` and diff the returned `events` against what you intended before
   pointing production traffic at it.
