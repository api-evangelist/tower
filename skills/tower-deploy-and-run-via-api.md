---
name: Deploy and run a Tower app via the REST API
description: >-
  Create an app, deploy a version, run it, and follow the run to completion
  using the Tower REST API (api.tower.dev/v1) with an sk- API key.
api: openapi/tower-openapi-original.json
operations: [create-app, deploy-app, run-app, describe-run, describe-run-logs, stream-run-logs]
generated: '2026-07-21'
method: generated
---

# Deploy and run a Tower app via the REST API

Ground rules (from `conventions/tower-conventions.yml` and `errors/tower-problem-types.yml`):

- Authenticate every request with the `X-API-Key` header (keys are prefixed `sk-`). A key missing the operation's required scope gets `403`; this flow needs `apps:create`, `apps:deploy`, `apps:run`, `runs:read`, and `runs:logs`.
- Errors are RFC 9457 `application/problem+json` (`ErrorModel`: `title`, `status`, `detail`, `errors[]`). `422` means validation failure — inspect `errors[]` for the offending field.
- There is no idempotency-key contract: do not blindly retry `POST`s that may have succeeded; check state first with the corresponding `describe-*`/`list-*` operation.

## Steps

1. **Create the app** — `create-app` (`POST /apps`) with a JSON body containing the app `name` (and optional `description`). A `409` means the name already exists; confirm with `describe-app` (`GET /apps/{name}`) and continue.
2. **Deploy a version** — `deploy-app` (`POST /apps/{name}/deploy`). Accepts either a TAR upload (`application/tar`) of the packaged app or a JSON body with `source_uri`. A successful deploy creates an immutable version (v1, v2, ...) pinned to an environment.
3. **Run it** — `run-app` (`POST /apps/{name}/runs`) with the run parameters; pass the target environment where relevant. The response identifies the run's sequence number `seq`.
4. **Follow the run** — poll `describe-run` (`GET /apps/{name}/runs/{seq}`) for status, or attach to `stream-run-logs` (`GET /apps/{name}/runs/{seq}/logs/stream`, Server-Sent Events) for real-time logs. After completion, `describe-run-logs` returns the full log.
5. **Recurring runs** — hand off to `create-schedule` (`POST /schedules`) with a cron expression (scope `schedules:create`); manage in bulk with `activate-schedules` / `deactivate-schedules`.

## Notes for agents

- Prefer the official Tower MCP server (`mcp/tower-mcp.yml`) when operating interactively — `tower_deploy`, `tower_run_remote`, and `tower_apps_logs` wrap this exact flow with local packaging handled for you. Use the raw API for CI or server-side automation with a scoped service-account key (`create-service-account-api-key`).
- Webhooks (`create-webhook`) can push run events to your endpoint instead of polling; verify the `X-Tower-Signature` HMAC (see `asyncapi/tower-webhooks.yml`).
