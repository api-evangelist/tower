# Tower

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
> **On a security or compliance team?** Email
> [info@apievangelist.com](mailto:info@apievangelist.com) with *security* in the subject line and
> you will get a person, not a form. We will tell you exactly which public URLs this profile was
> built from so your team can see the same surface we did, and we will take the listing down on
> request while you work through it.
>
> Full detail: **[Where this data comes from](https://apievangelist.com/about/where-our-data-comes-from)**
<!-- API-EVANGELIST-PROVENANCE:END -->

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
