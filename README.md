# Hightouch

<!-- API-EVANGELIST-PROVENANCE:BEGIN -->
> ### About this repository
>
> **This is not our API.** This repository is an independent, third-party profile of a company's
> **publicly available** API surface, maintained by [API Evangelist](https://apievangelist.com).
> API Evangelist does not operate, host, resell, or support this company's APIs, and is not
> affiliated with or endorsed by the company unless stated on the profile.
>
> **Where the information came from.** Everything here is assembled from material a member of the
> public can reach with a browser and no credentials — the company's own website, developer portal
> and documentation, the specifications it publishes for public use (OpenAPI, AsyncAPI, JSON Schema,
> `apis.json`, `llms.txt` and similar), its public repositories, and its public status, pricing and
> changelog pages. **Nothing here is obtained by breaching a system, defeating an access control, or
> using credentials of any kind.**
>
> **The rating is an independent assessment.** The Kin Score and Agent Readiness rating are
> independently calculated scores of a company's *public* API artifacts, produced by API Evangelist
> against a published rubric. They are not certifications, endorsements, security assessments, or
> audits, and they score published artifacts — not the quality, safety, or security of the software.
>
> **Corrections, re-scores, and removal are free.** No partnership, contract, or purchase is
> required, and you do not need to justify the request.
>
> - **Something wrong?** Open an issue on this repository, or email
>   [info@apievangelist.com](mailto:info@apievangelist.com).
> - **Published something new?** Ask for a re-score and we will re-run the rating.
> - **Want the listing taken down?** Say so and we will honor it. The profile is reduced to your
>   company name, a factual description, and a link to your own site, and the company is recorded as
>   **unrated** — never scored zero for having asked.
>
> **Response times.** Acknowledgement within **one business day**; removal or restriction within
> **two business days**; corrections and re-scores within **five business days**.
>
> **Not from the company, and here with a question?** You are welcome here — we would rather be the
> front line and point you the right way than have a good report go nowhere. What this repository
> can answer is narrow, though, so it is worth knowing who you are actually looking for:
>
> - **A question about how the API works, an account, billing, or a bug in the service** — that is
>   the company's own support, not us. We profile this API; we do not operate it and cannot see
>   your account.
> - **A bug in an open-source project we only catalog** — file it on that project's own repository.
>   This has happened with a real and correct bug report that reached us instead of the people who
>   could fix it, which helped nobody.
> - **Anything about this listing itself** — the description, the tags, the rating, a missing or
>   wrong artifact — is ours. Open an issue here.
> - **Not sure, or something general about API Evangelist or APIs.io** — open an issue on the
>   [APIs.io Inbox](https://github.com/api-search/inbox) and we will route it.
>
> **This repository contains no software, and we will never ask you to download anything.** There is
> no build, release, installer, or binary here — only text and machine-readable API descriptions, so
> there is nothing here that can be "corrupt" or need "repairing". Any issue, comment, or email
> claiming otherwise and offering a download link is not from us and is hostile. Do not follow the
> link; it is a lure. Report it to GitHub and, if you like, tell us at
> [info@apievangelist.com](mailto:info@apievangelist.com) so we can take it down.
>
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

Hightouch is a composable Customer Data Platform (CDP) and agentic marketing platform that activates data directly from cloud warehouses and lakehouses such as Snowflake, BigQuery, Databricks and Redshift to more than 290 SaaS destinations, without copying or storing customer data. The platform covers Reverse ETL, Customer Studio audience building and journey orchestration, identity resolution, first-party event collection with SDKs for web and mobile, real-time personalization, AI Decisioning, Match Booster and an Ad Studio for advertising creative. Developers get a bearer-authenticated REST API at https://api.hightouch.com/api/v1 covering sources, models, destinations, syncs and runs, campaigns, decision-engine flows, event contracts and identity graphs, plus an `ht` CLI, Git Sync for version-controlled resource YAML, workspace environments with approval flows, a public documentation MCP server, and an A2A agent card for the Hightouch Marketing Agent.

**Areas:** CDP · Data Activation · Reverse ETL · Audience Management · Identity Resolution · Event Collection · Marketing · Advertising · AI Agents · Data Warehouse · A2A · Customer Data Platform

## Hightouch on APIs.io

Everything profiled for Hightouch is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/hightouch/](https://apis.io/providers/hightouch/)** — or go straight to one of the APIs or properties below.

### APIs (10)

- [Hightouch Sources API](https://apis.io/apis/hightouch/hightouch-sources-api/) — Warehouse and database sources Hightouch reads from.
- [Hightouch Models API](https://apis.io/apis/hightouch/hightouch-models-api/) — Model definitions (SQL, table, dbt, visual) over a source.
- [Hightouch Destinations API](https://apis.io/apis/hightouch/hightouch-destinations-api/) — Destination connectors receiving synced data.
- [Hightouch Syncs API](https://apis.io/apis/hightouch/hightouch-syncs-api/) — Syncs, sync runs, sync sequences and their triggers.
- [Hightouch Campaigns API](https://apis.io/apis/hightouch/hightouch-campaigns-api/) — Trigger a campaign send to handle- or profile-based recipients and read back per-send status.
- [Hightouch Events API](https://apis.io/apis/hightouch/hightouch-events-api/) — First-party event governance — event contracts and event domains.
- [Hightouch Decision Engine API](https://apis.io/apis/hightouch/hightouch-decision-engine-api/) — The Decision Engine API from Hightouch — 5 operation(s) for decision engine.
- [Hightouch Id Graphs API](https://apis.io/apis/hightouch/hightouch-id-graphs-api/) — The Id Graphs API from Hightouch — 1 operation(s) for id graphs.
- [Hightouch Idr API](https://apis.io/apis/hightouch/hightouch-idr-api/) — The Idr API from Hightouch — 4 operation(s) for idr.
- [Hightouch Sync Sequences API](https://apis.io/apis/hightouch/hightouch-sync-sequences-api/) — The Sync Sequences API from Hightouch — 2 operation(s) for sync sequences.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### AsyncAPI (1)

Event-driven and webhook contracts.

- [Hightouch Webhooks](https://apis.io/asyncapis/hightouch/hightouch-webhooks/)

#### GraphQL (1)

GraphQL schemas.

- [Moved to /providers/hightouch/](https://apis.io/graphqls/hightouch/hightouch-graphql/)

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [hightouch-docs](https://apis.io/servers/hightouch/hightouch-docs/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Hightouch Agentic Access](https://apis.io/agentic-access/hightouch/hightouch-agentic-access/)

#### Collections (5)

Postman and Open Collection request collections.

- [Hightouch Management API](https://apis.io/collections/hightouch/open-hightouch/)
- [Hightouch Management Destinations API](https://apis.io/collections/hightouch/open-hightouch-destinations-api/)
- [Hightouch Management Destinations Models API](https://apis.io/collections/hightouch/open-hightouch-models-api/)
- [Hightouch Management Destinations Sources API](https://apis.io/collections/hightouch/open-hightouch-sources-api/)
- [Hightouch Management Destinations Syncs API](https://apis.io/collections/hightouch/open-hightouch-syncs-api/)

#### Overlays (11)

OpenAPI overlays, including conversational phrasing for each operation.

- [Hightouch Api Overlay](https://apis.io/overlays/hightouch/hightouch-api-overlay/)
- [Hightouch Campaigns Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-campaigns-api-phrasing-overlay/)
- [Hightouch Decision Engine Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-decision-engine-api-phrasing-overlay/)
- [Hightouch Destinations Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-destinations-api-phrasing-overlay/)
- [Hightouch Events Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-events-api-phrasing-overlay/)
- [Hightouch Id Graphs Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-id-graphs-api-phrasing-overlay/)
- [Hightouch Idr Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-idr-api-phrasing-overlay/)
- [Hightouch Models Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-models-api-phrasing-overlay/)
- [Hightouch Sources Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-sources-api-phrasing-overlay/)
- [Hightouch Sync Sequences Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-sync-sequences-api-phrasing-overlay/)
- [Hightouch Syncs Api Phrasing Overlay](https://apis.io/overlays/hightouch/hightouch-syncs-api-phrasing-overlay/)

#### Security (3)

Authentication, trust centre, and vulnerability disclosure.

- [Hightouch Authentication](https://apis.io/security/hightouch/hightouch-authentication/)
- [Hightouch Domain Security](https://apis.io/security/hightouch/hightouch-domain-security/)
- [Hightouch Trust Center](https://apis.io/security/hightouch/hightouch-trust-center/)

#### OAuth scopes (1)

The permissions the API asks for.

- [Hightouch Scopes](https://apis.io/scopes/hightouch/hightouch-scopes/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Hightouch Plans Pricing](https://apis.io/plans/hightouch/hightouch-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Hightouch Rate Limits](https://apis.io/rate-limits/hightouch/hightouch-rate-limits/)

#### FinOps (1)

What the API costs to run, by operation.

- [Hightouch Finops](https://apis.io/finops/hightouch/hightouch-finops/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://hightouch.com/)
- [Documentation](https://hightouch.com/docs)
- [Getting started](https://hightouch.com/docs/getting-started/welcome)
- [API reference](https://hightouch.com/docs/api-reference)
- [Pricing](https://hightouch.com/pricing)
- [Sign up](https://app.hightouch.com/signup)
- [Blog](https://hightouch.com/blog)
- [Compliance](https://hightouch.com/platform/security)
- [Terms of service](https://hightouch.com/terms-of-service)
- [Privacy policy](https://hightouch.com/privacy-policy)
- [GitHub](https://github.com/hightouchio)
- [Status](https://status.hightouch.io)

## API Evangelist rating

**Kin Score 66.4** — strong · rubric 0.25.0 · scored 2026-10-23

| Facet | Score |
|---|---|
| Discoverability | 75.0 |
| Contract quality | 61.8 |
| Contract governance | 18.2 |
| Operational transparency | 47.4 |
| Developer ergonomics | 75.6 |
| Access clarity | 85.5 |

**Agent readiness 63.3** — agent-ready (gated down from agent-native)

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | documented (partial credit) |
| Auth Clarity | served (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | verified |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | yes |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | served (partial credit) |
| Protected Resource Metadata | verified |
| Dynamic Client Registration | yes |
| Agentic Commerce | — |
| Pagination Ratio | paginated |
| Operation Distinctiveness | distinct |

**Regulatory alignment 39.2** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/hightouch/](https://apis.io/providers/hightouch/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Hightouch: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/hightouch/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
