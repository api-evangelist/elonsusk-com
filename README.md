# Artem / A2A Sandbox

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

Artem / A2A Sandbox is a one-operator agent-commerce sandbox that runs a paid "Sandbox Contractor Agent" at a2a.elonsusk.com: an Agent2Agent (A2A) JSON-RPC agent selling 28 skills — keyless developer utilities (JSON/YAML/CSV conversion, hashing incl. keccak256, base64/hex/base58, JWT decode, UUID, semver, epoch), on-chain data reads (EVM and Solana balances, ERC-20 metadata, gas price, transaction status, SPL supply) and security scans (MCP tool-manifest risk, EVM contract bytecode signals) — plus model-backed code review, code generation and inference sold quote-first. Every skill is payable per call over the x402 v2 HTTP payment protocol (HTTP 402 + PAYMENT-REQUIRED challenge, USDC on Base or Solana, from $0.001) at POST /x402/{skill}, or through a classic multi-chain crypto invoice (SOL, USDC, ETH, BTC) on the REST task API. The same FastAPI origin publishes an OpenAPI 3.1.0 contract at /openapi.json with Swagger UI at /docs, an A2A agent card at /.well-known/agent-card.json, an x402 discovery document at /.well-known/x402.json, and live health and revenue-metrics endpoints. The registrable domain elonsusk.com itself serves no website (TLS refused, HTTP 401); the a2a subdomain is the whole public surface.

**Areas:** Agents · Agentic Commerce · A2A · x402 · Developer Tools · Blockchain · Solana · Ethereum · Security · Code Review · Code Generation · Agent-Native

## Artem / A2A Sandbox on APIs.io

Everything profiled for Artem / A2A Sandbox is published on APIs.io rather than in this repository. Start at the provider page — **[apis.io/providers/elonsusk-com/](https://apis.io/providers/elonsusk-com/)** — or go straight to one of the APIs or properties below.

### APIs (13)

- [Sandbox Contractor Agent (A2A)](https://apis.io/apis/elonsusk-com/sandbox-contractor-agent-a2a/) — Agent2Agent protocol surface: an agent card served from https://a2a.elonsusk.com/.well-known/agent-card.json (and the legacy /.well-known/agent.json)…
- [Artem / A2A Sandbox A2a API](https://apis.io/apis/elonsusk-com/elonsusk-com-a2a-api/) — The A2a API from Artem / A2A Sandbox — 1 operation(s) for a2a.
- [Artem / A2A Sandbox A2A Autonomous Trader Agent API](https://apis.io/apis/elonsusk-com/elonsusk-com-a2a-autonomous-trader-agent-api/) — The A2A Autonomous Trader Agent API from Artem / A2A Sandbox — 1 operation(s) for a2a autonomous trader agent.
- [Artem / A2A Sandbox Health API](https://apis.io/apis/elonsusk-com/elonsusk-com-health-api/) — The Health API from Artem / A2A Sandbox — 1 operation(s) for health.
- [Artem / A2A Sandbox Healthz API](https://apis.io/apis/elonsusk-com/elonsusk-com-healthz-api/) — The Healthz API from Artem / A2A Sandbox — 1 operation(s) for healthz.
- [Artem / A2A Sandbox Healthz.earn.superteam API](https://apis.io/apis/elonsusk-com/elonsusk-com-healthz-earn-superteam-api/) — The Healthz.earn.superteam API from Artem / A2A Sandbox — 1 operation(s) for healthz.earn.superteam.
- [Artem / A2A Sandbox Leads API](https://apis.io/apis/elonsusk-com/elonsusk-com-leads-api/) — The Leads API from Artem / A2A Sandbox — 1 operation(s) for leads.
- [Artem / A2A Sandbox Metrics API](https://apis.io/apis/elonsusk-com/elonsusk-com-metrics-api/) — The Metrics API from Artem / A2A Sandbox — 1 operation(s) for metrics.
- [Artem / A2A Sandbox Payments API](https://apis.io/apis/elonsusk-com/elonsusk-com-payments-api/) — The Payments API from Artem / A2A Sandbox — 1 operation(s) for payments.
- [Artem / A2A Sandbox Showcase API](https://apis.io/apis/elonsusk-com/elonsusk-com-showcase-api/) — The Showcase API from Artem / A2A Sandbox — 5 operation(s) for showcase.
- [Artem / A2A Sandbox Tasks API](https://apis.io/apis/elonsusk-com/elonsusk-com-tasks-api/) — The Tasks API from Artem / A2A Sandbox — 3 operation(s) for tasks.
- [Artem / A2A Sandbox .well Known API](https://apis.io/apis/elonsusk-com/elonsusk-com-well-known-api/) — The .well Known API from Artem / A2A Sandbox — 5 operation(s) for .well known.
- [Artem / A2A Sandbox X402 API](https://apis.io/apis/elonsusk-com/elonsusk-com-x402-api/) — The X402 API from Artem / A2A Sandbox — 1 operation(s) for x402.

### Published properties

Each property below is a page on APIs.io carrying the machine-readable artifact and what it says.

#### MCP servers (1)

Model Context Protocol servers that expose the API to agents.

- [elonsusk-com-sandbox-contractor](https://apis.io/servers/elonsusk-com/elonsusk-com-sandbox-contractor/)

#### Agentic access (1)

Which operations an agent can call, which act, and which need a human in the loop.

- [Elonsusk Com Agentic Access](https://apis.io/agentic-access/elonsusk-com/elonsusk-com-agentic-access/)

#### Overlays (1)

OpenAPI overlays, including conversational phrasing for each operation.

- [Elonsusk Com Openapi Overlay](https://apis.io/overlays/elonsusk-com/elonsusk-com-openapi-overlay/)

#### Security (2)

Authentication, trust centre, and vulnerability disclosure.

- [Elonsusk Com Authentication](https://apis.io/security/elonsusk-com/elonsusk-com-authentication/)
- [Elonsusk Com Domain Security](https://apis.io/security/elonsusk-com/elonsusk-com-domain-security/)

#### Plans and pricing (1)

Published plans, tiers and prices.

- [Elonsusk Com Plans Pricing](https://apis.io/plans/elonsusk-com/elonsusk-com-plans-pricing/)

#### Rate limits (1)

Published request limits.

- [Elonsusk Com Rate Limits](https://apis.io/rate-limits/elonsusk-com/elonsusk-com-rate-limits/)

## Where to find this API

Links to the company's own pages. This repository publishes no copy of their specifications — the canonical document is theirs and lives at the URLs below.

- [Website](https://a2a.elonsusk.com/)
- [Documentation](https://a2a.elonsusk.com/docs)
- [API reference](https://a2a.elonsusk.com/redoc)
- [Pricing](https://a2a.elonsusk.com/)

## API Evangelist rating

**Kin Score 31.9** — thin · rubric 0.24.0 · scored 2026-10-17

| Facet | Score |
|---|---|
| Discoverability | 69.6 |
| Contract quality | 35.0 |
| Contract governance | 18.2 |
| Operational transparency | 0.0 |
| Developer ergonomics | 30.4 |
| Access clarity | 42.1 |

**Agent readiness 32.2** — agent-ready

| Agent-readiness dimension | Result |
|---|---|
| Spec Presence | yes |
| Agentic Access | derived (partial credit) |
| Reversibility Documented | — |
| MCP Server | — |
| Auth Clarity | bearer (partial credit) |
| Idempotency | — |
| Error Semantics | verified |
| OpenAPI Examples | — |
| Rate Limit Signal | documented (partial credit) |
| Event Surface Described | — |
| Agent Skills | derived (partial credit) |
| Well Known Catalog | — |
| Consent Identity | — |
| Agent Card | conformant |
| Dry Run Mode | — |
| Delegated Identity | — |
| Protected Resource Metadata | — |
| Dynamic Client Registration | — |
| Agentic Commerce | — |

**Regulatory alignment 16.7** — Horizontal (data, software, accessibility, platform)

The rubric is published at [github.com/api-evangelist/kin-score](https://github.com/api-evangelist/kin-score). The per-check breakdown behind these numbers — which checks were earned, partial or missed — along with score history and how this provider compares to its peers, is available at [apis.io/providers/elonsusk-com/](https://apis.io/providers/elonsusk-com/).

## How this profile is made

API Evangelist profiles a company's public API surface the way a developer would find it: the website, developer portal and documentation, the specifications it publishes, its public repositories, and its pricing, status and changelog pages. From that it derives the properties above — contracts split per API, workflows, schemas, collections, governance rules, plans and rate limits — and scores them against the published [Kin Score rubric](https://github.com/api-evangelist/kin-score).

The artifacts are published on [APIs.io](https://apis.io), not in this repository. This repository is the public record for Artem / A2A Sandbox: the place to say something is wrong, missing or out of date, and to ask for a re-score or a removal.

## Open an issue

- **Something about this listing** — a wrong description, a missing API, a stale artifact or a question about the rating: [open an issue on this repository](https://github.com/api-evangelist/elonsusk-com/issues/new).
- **A new API, or one that is not in the catalog yet** — [submit it on APIs.io](https://apis.io/add/).
- **Anything else** — [the APIs.io inbox](https://github.com/api-search/inbox/issues/new) or [info@apievangelist.com](mailto:info@apievangelist.com).
