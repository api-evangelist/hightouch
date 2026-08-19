---
name: hightouch-docs
description: Hightouch documentation — reverse ETL, audience building, identity resolution, and AI-powered marketing. Covers REST API, CLI, Events SDK, 292+ destination connectors, and 42+ source connectors.
---

# Hightouch Documentation

Hightouch is a data activation platform that syncs data from warehouses and databases to 292+ business tools. It covers reverse ETL, audience building (Customer Studio), identity resolution, AI decisioning, and real-time event streaming.

Documentation: https://hightouch.com/docs

## Core concepts

- **Source**: A data warehouse or database (Snowflake, BigQuery, Redshift, Databricks, PostgreSQL, etc.) that Hightouch reads from.
- **Model**: A SQL query, table, dbt model, or visual segment that defines the dataset to sync.
- **Destination**: A business tool (CRM, ad platform, email tool, etc.) that receives synced data.
- **Sync**: A configured pipeline that maps model columns to destination fields and runs on a schedule.
- **Audience**: A segment of users defined with visual or SQL rules in Customer Studio.
- **Schema**: A unified customer data model (user, account, event) in Customer Studio.

## REST API

Base URL: `https://api.hightouch.com/api/v1`

Authentication: Bearer token via `Authorization: Bearer <API_KEY>`. Create API keys in **Settings > API keys**.

Common operations:

| Operation | Method | Endpoint |
|-----------|--------|----------|
| List syncs | GET | `/syncs` |
| Get sync | GET | `/syncs/{id}` |
| Trigger sync | POST | `/syncs/{id}/trigger` |
| List models | GET | `/models` |
| List sources | GET | `/sources` |
| List destinations | GET | `/destinations` |

Full API reference: https://hightouch.com/docs/developer-tools/api-reference

## CLI

Install:

```bash
npm install -g @hightouch/cli
```

Key commands:

```bash
ht login                    # Authenticate
ht syncs list               # List all syncs
ht syncs trigger <sync-id>  # Trigger a sync run
ht models list              # List all models
ht sources list             # List all sources
```

Docs: https://hightouch.com/docs/developer-tools/ht-cli

## Events SDK

Track user events and send them to Hightouch for real-time activation.

Available SDKs: `Android`, `Browser`, `C#`, `Flutter`, `Go`, `HTTP API`, `Java`, `Node.js`, `PHP`, `Python`, `React Native`, `Ruby`, `iOS`

Browser quick start:

```html
<script>
  !function(){var e=window.htevents=window.htevents||[];if(!e.initialize)if(e.invoked)console.error("Hightouch snippet already invoked.");else{e.invoked=!0;e.methods=["trackSubmit","trackClick","trackLink","trackForm","pageview","identify","reset","group","track","ready","alias","debug","page","once","off","on","addSourceMiddleware","addIntegrationMiddleware","setAnonymousId","addDestinationMiddleware"];e.factory=function(t){return function(){var n=Array.prototype.slice.call(arguments);n.unshift(t);e.push(n);return e}};for(var t=0;t<e.methods.length;t++){var n=e.methods[t];e[n]=e.factory(n)}e.load=function(t,n){var o=document.createElement("script");o.type="text/javascript";o.async=!0;o.src="https://cdn.hightouch-events.com/browser/release/v1-latest/events.min.js";var r=document.getElementsByTagName("script")[0];r.parentNode.insertBefore(o,r);e._loadOptions=n;e._writeKey=t};e.SNIPPET_VERSION="0.0.1";
  e.load("YOUR_WRITE_KEY");
  e.page();
  }}();
</script>
```

Key methods:

```javascript
htevents.identify("user-123", { email: "user@example.com", plan: "enterprise" });
htevents.track("Order Completed", { orderId: "abc", total: 99.99 });
htevents.page("Docs", "API Reference");
htevents.group("company-456", { name: "Acme Corp", industry: "SaaS" });
```

Docs: https://hightouch.com/docs/events/overview

## Sync configuration

### Sync modes

- **Upsert**: Insert new records, update existing ones (matched by primary key).
- **Mirror**: Full sync — upsert matching records and remove records no longer in the model.
- **Update**: Only update existing records; never create new ones.
- **Insert**: Only create new records; never update existing ones.

### Schedule types

- **Interval**: Run every N minutes/hours.
- **Cron**: Custom cron expression.
- **dbt Cloud**: Trigger after a dbt Cloud job completes.
- **Airflow / Dagster / Prefect**: Orchestrator-triggered via API.
- **Visual**: Pick specific days and times in the UI.
- **Continuous**: Near-real-time syncing via change data capture (CDC) on supported sources.

Docs: https://hightouch.com/docs/syncs/overview

## Customer Studio

Build audiences and computed traits with a visual UI or SQL, no code required.

- **Audiences**: Define user segments with AND/OR filter groups. Supports nested conditions, event filters, and related entity joins.
- **Computed traits**: Aggregations on user data (count, sum, average, most frequent, first/last, etc.) that become columns on the user model.
- **Splits**: Randomly divide an audience into groups for A/B testing.

Docs: https://hightouch.com/docs/customer-studio/overview

## Extensions and integrations

Hightouch integrates with data pipeline and orchestration tools: `Airflow`, `Connections`, `Dagster`, `Datadog`, `Dbt Cloud`, `Dbt Models`, `Dbt Observability`, `Fivetran`, `Git Sync`, `Looker Models`, `Mage`, `Pagerduty`, `Prefect`, `Sigma`.

- **292+ destinations**: CRMs, ad platforms, email/SMS tools, analytics, data warehouses, and more.
- **42+ sources**: Snowflake, BigQuery, Redshift, Databricks, PostgreSQL, MySQL, S3, GCS, and more.

Browse all integrations: https://hightouch.com/docs/destinations/overview and https://hightouch.com/docs/sources/overview

## Workspace management

- **SSO/SAML**: Configure single sign-on via Okta, Azure AD, Google, or any SAML 2.0 provider.
- **RBAC**: Role-based access with workspace-level and resource-level permissions (Admin, Editor, Viewer, plus custom roles).
- **Approval flows**: Require review before syncs run or config changes apply.
- **Audit logs**: Track who changed what and when.

Docs: https://hightouch.com/docs/workspace-management/overview

## Troubleshooting

- **Sync errors**: Check the sync run log in the Hightouch UI. Each row shows status, error message, and affected records.
- **Live Debugger**: Real-time view of API requests Hightouch sends to a destination — shows payloads, response codes, and errors.
- **Sync alerts**: Configure Slack, email, or PagerDuty alerts for sync failures, row-level errors, or schedule delays.

Docs: https://hightouch.com/docs/syncs/sync-alerts

## Quick reference

| Resource | URL |
|----------|-----|
| Documentation home | https://hightouch.com/docs |
| API reference | https://hightouch.com/docs/developer-tools/api-reference |
| CLI docs | https://hightouch.com/docs/developer-tools/ht-cli |
| Events SDK | https://hightouch.com/docs/events/overview |
| Syncs | https://hightouch.com/docs/syncs/overview |
| Customer Studio | https://hightouch.com/docs/customer-studio/overview |
| Sources | https://hightouch.com/docs/sources/overview |
| Destinations | https://hightouch.com/docs/destinations/overview |
| Status page | https://status.hightouch.com |
| Changelog | https://hightouch.com/changelog |
| MCP server | https://hightouch.com/docs/api/mcp (Streamable HTTP, no auth) |
| llms.txt | https://hightouch.com/docs/llms.txt |
| Full docs (LLM) | https://hightouch.com/docs/llms-full.txt |
