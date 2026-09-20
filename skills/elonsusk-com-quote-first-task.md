---
name: elonsusk-com-quote-first-task
description: Create a quoted task on the Sandbox Contractor Agent, pay its crypto invoice with the task id as memo, poll it to completion, and cancel it over JSON-RPC before paying if the quote is wrong.
api: openapi/elonsusk-com-openapi.json
operations:
  - create_task_v1_tasks_post
  - get_task_v1_tasks__task_id__get
  - jsonrpc_a2a_post
  - list_tasks_v1_tasks_get
method: generated
generated: '2026-09-19'
grounding: >-
  All four operationIds exist verbatim in openapi/elonsusk-com-openapi.json. The task shape, states and
  invoice fields are those returned live by GET /v1/tasks on 2026-09-19 (data-model/); the JSON-RPC methods
  and error codes are from the agent card and the live responder (a2a/). The payment flow is quoted from the
  card's how_to_order block. No task was created or paid by API Evangelist.
---

# Quote-first task

Base URL `https://a2a.elonsusk.com`. No authentication. Creating a task is free; work starts when its invoice is paid.

## 1. Create the task and read the quote

`POST /v1/tasks` (`create_task_v1_tasks_post`) with `CreateTaskRequest`:

```json
{"skill": "code.review", "input": {"prompt": "Review this diff and return prioritized findings.", "diff": "..."}, "client_task_id": null}
```

`skill` defaults to `inference.complete`; use a skill id from the card. Over A2A the same call is `POST /a2a` (`jsonrpc_a2a_post`) with `{"jsonrpc":"2.0","id":"q1","method":"tasks/send","params":{"skill":"code.review","input":{...}}}`.

The response is a Task. Read three things:

- `id` — a UUID; it is also the **invoice memo**.
- `quote` — `{quote_usd, currency, tokens_estimate {input, output}, pricing {price_per_1k_tokens_in 0.05, price_per_1k_tokens_out 0.20, flat_min_usd, skill_multiplier}}`. The card's multipliers: code.generate 1.2, code.review 1.0, inference.complete 1.0, external.llm.delegate 4.0, batch.discount 0.8; priority normal 1x, priority 3x, rush 8x. Packages: Quick Review $5, Full Code Gen $25, Rush 1hr $100.
- `invoice` — `{amount_usd, asset, address, memo, expires_at, provider, status}`. Methods: SOL, USDC on Solana, ETH, USDC on Ethereum, BTC (card `payment_methods`).

`state` will be `quoted` / `payment_required`. **Nothing is owed until you pay.**

## 2. Decide — and cancel if the quote is wrong

If you will not pay, cancel now: `POST /a2a` with `{"jsonrpc":"2.0","id":"c1","method":"tasks/cancel","params":{"id":"<task id>"}}`. There is no REST cancel. An unknown id returns a JSON-RPC error with `code: 404` (HTTP 200). Which later states still allow cancellation, and whether cancelling a paid task refunds, is **not documented** — treat payment as the point of no return. Unpaid invoices expire (`invoice.expires_at`; the visible task's was 60 minutes after creation).

## 3. Pay with the memo

Send exactly `invoice.amount_usd` worth of the chosen asset to `invoice.address` **with memo = task id** (`payment_notes.memo_required: true`). The operator's payment watcher (Solana RPC) or a NOWPayments/CoinGate webhook moves the task to `paid`. There is no idempotency key: if your POST timed out, do not simply repeat it — a second quoted task may already exist. `list_tasks_v1_tasks_get` (`GET /v1/tasks?state=payment_required`) shows open tasks (all of them, system-wide), which is how to find yours.

## 4. Poll to completion

`GET /v1/tasks/{task_id}` (`get_task_v1_tasks__task_id__get`) or JSON-RPC `tasks/get`. States: `submitted → quoted → payment_required → paid → working → (awaiting_human_response) → completed | failed | canceled`. `events[]` is the transition history; `result` and `artifacts[]` (name, mime_type, bytes) appear on `completed`; `error` on `failed`. No push notifications or streaming exist — poll.

## Rules

- Model-backed skills depend on a local model rail; check `GET /healthz` `degraded` before paying for `code.review`, `code.generate`, `inference.complete` or `external.llm.delegate`.
- `GET /v1/tasks` is public and shows every task's input; do not put secrets in `input`.
- Errors: 422 `HTTPValidationError` (declared), 404 `{"detail":{"error":"task not found: …"}}` (observed), 405 on wrong method.
