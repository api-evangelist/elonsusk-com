---
name: elonsusk-com-preflight-agent
description: Before spending on the Sandbox Contractor Agent, read its card, health and metrics to learn which skills exist, which rails are degraded and what the queue looks like.
api: openapi/elonsusk-com-openapi.json
operations:
  - agent_card__well_known_agent_card_json_get
  - health_health_get
  - healthz_healthz_get
  - metrics_v1_metrics_get
method: generated
generated: '2026-09-19'
grounding: >-
  All four operationIds exist verbatim in openapi/elonsusk-com-openapi.json. Field names are those returned
  live on 2026-09-19 (a2a/, lifecycle/, rate-limits/). Nothing here was invented.
---

# Pre-flight: is this agent worth paying right now?

All four reads are free and anonymous. Base URL `https://a2a.elonsusk.com`.

## 1. The card — what is for sale

`GET /.well-known/agent-card.json` (`agent_card__well_known_agent_card_json_get`). Use `supportedInterfaces[0].url` (`https://a2a.elonsusk.com/a2a`) as the JSON-RPC endpoint — the canonical card's top-level `url` is the bare origin and answers **405** to JSON-RPC. `skills[]` has 28 entries; the 24 keyless ones carry `priceUsd` and `exampleInput`. `pricing` gives the metering inputs, `payment_methods` the invoice rails, `task_state_machine` the nine states, `endpoints` a map of every route.

## 2. The live skill list — what actually exists

`GET /health` (`health_health_get`) returns `{"ok": true, "model": "...", "skills": [...]}`. On 2026-09-19 it listed **30** ids — two (`shell.run`, `file.deliver`) that the card does not declare. If a skill you need is in `/health` but not in the card, it is still callable by id on `/v1/tasks`.

## 3. Health — which rails are down

`GET /healthz` (`healthz_healthz_get`):

- `degraded[]` — on 2026-09-19 it read `["ollama"]`, with `ollama.ok false`. That rail backs `code.review`, `code.generate`, `inference.complete` and `external.llm.delegate`, whose card descriptions say "delivered when a rail is up". **Do not pay for those four while the rail is degraded** unless you can wait.
- `queue.by_state` — `payment_required` is unpaid tasks (44 at probe time), `working` and `paid_waiting` are the live backlog.
- `worker.max_concurrent_jobs` (3) and `worker.running` — your position once paid.
- `payment_watcher.enabled` / `provider` — whether invoice payments are being detected automatically (`solana_rpc`).

## 4. Metrics — is anyone getting served

`GET /v1/metrics` (`metrics_v1_metrics_get`): `jobs_total`, `jobs_completed`, `jobs_failed`, `avg_latency_seconds`, revenue counters. On 2026-09-19: 61 jobs, 11 completed, 4 failed, average latency 14.85 s. A high `jobs_failed` relative to `jobs_completed` is a reason to prefer the cheap keyless skills.

## Decide

- Keyless utilities, on-chain reads and security scans (`util.*`, `data.*`, `security.*`) have no model dependency: safe to buy over x402 at $0.001-$0.02 (see `elonsusk-com-x402-pay-per-call`).
- Model-backed work: use the quote-first flow so you see the price before paying (see `elonsusk-com-quote-first-task`), and only after `/healthz` shows the rail up.
- There are no rate limits, no SLA, no status page and no refund policy published; these four reads are the only runtime signal you get.
