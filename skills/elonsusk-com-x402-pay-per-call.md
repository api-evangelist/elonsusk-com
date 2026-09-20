---
name: elonsusk-com-x402-pay-per-call
description: Buy one skill call from the Sandbox Contractor Agent in a single x402 round trip — read the catalog, take the 402 challenge, pay one rail, retry with PAYMENT-SIGNATURE.
api: openapi/elonsusk-com-openapi.json
operations:
  - x402_discovery__well_known_x402_json_get
  - agent_card__well_known_agent_card_json_get
  - x402_pay_per_call_x402__skill__post
method: generated
generated: '2026-09-19'
grounding: >-
  The three operationIds exist verbatim in openapi/elonsusk-com-openapi.json. Prices, rails, headers and the
  402 shape are quoted from /.well-known/x402.json and from the live challenge observed on
  POST /x402/util.json.format on 2026-09-19 (conformance/, errors/). Input field names come from the agent
  card's skills[].exampleInput. Nothing here was invented; the settle leg was not exercised.
---

# Pay-per-call over x402

Base URL `https://a2a.elonsusk.com`. Everything is `application/json`. There is no API key and no login; the price is the only gate.

## 0. Know the price and the rails before you call

`GET /.well-known/x402.json` (`x402_discovery__well_known_x402_json_get`, free). `endpoints[]` lists 27 priced paths. Each carries `priceUsd`, `network[]` in CAIP-2 and `rails[]` of `{network, asset, payTo}`:

- `eip155:8453` — USDC on Base, asset `0x833589fCD6eDb6E08f4c7C32D4f71b54bdA02913`
- `solana:5eykt4UsFv8P8NJdTREpY1vzqKqZKvdp` — USDC on Solana, mint `EPjFWdd5AufqSSqeM2qN1xzybapC8G4wEGGkZwyTDt1v`

Prices run from $0.001 (`data.evm.gas_price`, `data.evm.native_balance`, `data.solana.balance`) through $0.002-$0.003 for the utilities to $0.02 (`security.mcp_scan`, `inference.complete`) and $0.10 (`code.generate`). `headers` names the three protocol headers: challenge `PAYMENT-REQUIRED`, retry `PAYMENT-SIGNATURE`, settle `PAYMENT-RESPONSE`.

Most `inputSchema` entries in that file are a bare `{"type":"object"}`. The real field names are in the agent card (`agent_card__well_known_agent_card_json_get`) under `skills[].exampleInput`, for example:

| skill | exampleInput |
|---|---|
| `util.hash` | `{"algo": "sha256", "data": "hello"}` |
| `util.json.format` | `{"data": "{\"b\":1,\"a\":2}", "sort_keys": true}` |
| `data.evm.native_balance` | `{"network": "base", "address": "0x..."}` |
| `data.solana.balance` | `{"address": "<base58 address>"}` |
| `security.mcp_scan` | `{"tools": [{"name": "...", "description": "...", "inputSchema": {...}}]}` |

Only `code.generate` (`spec` required), `code.review` (`code` required) and `inference.complete` (`prompt` required) carry a real schema in x402.json.

## 1. Take the challenge (free)

`POST /x402/{skill}` (`x402_pay_per_call_x402__skill__post`) with the input as the JSON body and **no** `PAYMENT-SIGNATURE` header. You get **402** and a `PAYMENT-REQUIRED` header whose base64 payload is identical to the body:

```json
{"x402Version": 2, "error": "PAYMENT-SIGNATURE header is required",
 "resource": {"url": "https://a2a.elonsusk.com/x402/util.json.format", "mimeType": "application/json"},
 "accepts": [{"scheme": "exact", "network": "eip155:8453", "amount": "2000",
              "asset": "0x8335…2913", "payTo": "0x834E…0886", "maxTimeoutSeconds": 120,
              "extra": {"amountUsd": 0.002, "facilitator": "https://facilitator.payai.network",
                        "settlement": "facilitator_or_invoice_bridge", "verification": "evm_rpc"}}, …]}
```

`amount` is in atomic units of the asset — `"2000"` is 0.002 USDC at 6 decimals. The challenge is valid for `maxTimeoutSeconds` (120). A wrong skill id returns **404** `{"detail":{"error":"unsupported skill: …"}}`, and a GET returns **405**; neither costs anything.

## 2. Pay one rail and retry

Standard x402 v2: sign a payment for one `accepts[]` entry and repeat the identical POST with the `PAYMENT-SIGNATURE` header. The contract says a valid signature "settles, creates an A2A task (marked paid), returns receipt + artifact"; the receipt travels in `PAYMENT-RESPONSE`. The provider names `https://facilitator.payai.network` as the facilitator.

The invoice-bridge alternative is stated in `accepts[].extra.note`: send USDC to `payTo` on-chain, then retry with `payload.tx_ref` set to the transaction hash; it is verified on-chain (receipt success, USDC contract, correct payee, amount >= price) and **usable for exactly one call**.

## 3. Rules that protect your funds

- **No idempotency key and no reversal.** A settled x402 call cannot be refunded or voided through the API; a spent `tx_ref` cannot be reused. Do not retry a paid call blindly after a timeout — re-read the challenge first.
- **Model-backed skills may be down.** `code.review`, `code.generate` and `inference.complete` run on a local model rail; `GET /healthz` reported it `degraded` on 2026-09-19. Check it (see `elonsusk-com-preflight-agent`) before paying for one of those three.
- **No rate limits are published and none are signalled** — pace yourself.
- **Errors are not RFC 9457**: `{"detail": ...}` for 404/405/422, an x402 object for 402.
