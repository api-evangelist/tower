# Tower

Tower ([tower.dev](https://tower.dev)) is a Python-native data flow orchestrator and fully-managed data backend for pipelines, agents, and data applications. It pairs serverless (or self-hosted) Python compute with an open Apache Iceberg-based lakehouse compatible with Snowflake, Spark, and DuckDB. Teams deploy versioned apps with a Towerfile, run dbt Core and dlt ingestion pipelines, schedule and observe runs, and power data agents grounded in fresh company data. Founded by engineers from Snowflake, Databricks, Google Cloud Dataflow, and Puppet. Backed by Speedinvest.

## API surface

- **Tower API** — REST API at `https://api.tower.dev/v1` ([reference](https://docs.tower.dev/docs/reference/api/tower-api)); OpenAPI 3.1 published live at [/v1/openapi.json](https://api.tower.dev/v1/openapi.json) and harvested in [`openapi/`](openapi/). 112 operations across accounts, apps, versions, deploys, runs, environments, schedules, secrets, Iceberg catalogs, teams, service accounts, API keys, webhooks, and alerts.
- **Authentication** — `X-API-Key` header (keys prefixed `sk-`, scope-reducible) or session bearer tokens; documented permission scopes captured in [`scopes/`](scopes/).
- **Errors** — RFC 9457 `application/problem+json` ([`errors/`](errors/)).
- **Webhooks** — HMAC-SHA512-signed deliveries (`X-Tower-Signature`) plus SSE streams ([`asyncapi/`](asyncapi/)).
- **MCP server** — official, ships inside the CLI (`tower mcp-server`, stdio/http/sse) with a Claude Code plugin ([`mcp/`](mcp/)).
- **Agent Skills** — provider-published skills from [tower/agent-skills](https://github.com/tower/agent-skills) and the CLI plugin, saved verbatim in [`skills/`](skills/).
- **CLI + SDK** — one `tower` package on PyPI (CLI + MCP server + Python SDK); Homebrew tap and prebuilt binaries per release ([`packages/`](packages/), [`cli/`](cli/)).

This repository is part of the [API Evangelist](https://apievangelist.com) network and is indexed by [APIs.io](https://apis.io) via [`apis.yml`](apis.yml).
