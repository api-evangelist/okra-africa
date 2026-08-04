# Okra (okra-africa)

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

> **Status: RETIRED / DISCONTINUED.** Okra (Okra.ng), the Lagos-based open
> finance / open banking infrastructure company, quietly ceased operations in
> **May 2025** and wound the business down. As of this review (2026-07-12) the
> API and developer hosts — `api.okra.ng`, `dash.okra.ng`, `docs.okra.ng`,
> `identity-api.okra.ng` — no longer resolve, and the `okra.ng` domain now
> serves an unrelated parked page (an expired TLS certificate issued to
> `fggcowerrioga.com`). **The API is no longer callable.** This entry documents
> the historical API surface for the record, grounded in Okra's official
> `okraHQ/okra-node` SDK and archived documentation. Endpoint paths and the
> base URL are confirmed from that SDK; request/response schemas are *modeled*
> from the SDK and archived docs and flagged as such.

Okra was an open finance infrastructure provider for Africa (primarily Nigeria).
Businesses embedded the **Okra Widget** so an end user could securely link their
bank account, producing a `record` object. With the resulting authenticated
connection, a business could pull banking data and run financial workflows
through Okra's REST API: account and identity details, real-time balances,
categorized transactions, income/affordability signals, Nigerian KYC checks
(BVN, NUBAN, TIN, RC), and bank-to-bank payments plus recurring direct-debit
authorizations. Okra raised ~$16.5M and was, for a period, one of Africa's most
visible open-banking startups before shutting down.

**APIs.json:** [https://raw.githubusercontent.com/api-evangelist/okra-africa/refs/heads/main/apis.yml](https://raw.githubusercontent.com/api-evangelist/okra-africa/refs/heads/main/apis.yml)

## Access Model (historical)

- **Base URL:** `https://api.okra.ng/v2` (production). Sandbox used
  `https://api.okra.ng/v2/sandbox/`. Confirmed from the `okraHQ/okra-node` SDK.
- **Authentication:** Bearer **Okra Secret key** — `Authorization: Bearer <secret>`.
  The secret was issued in the Okra dashboard at `https://dash.okra.ng/settings/api-keys`.
  Confirmed from the SDK's request wrapper.
- **Style:** REST over HTTPS, JSON request/response. Endpoints were predominantly
  `POST` (including reads, which took a JSON filter body). No public WebSocket API.
- **Account linking:** the Okra Widget (client-side link flow) produced the
  `record`/`customer` identifiers that most data endpoints operate against;
  app callbacks/webhooks delivered link and refresh events.

## Tags

- Open Banking
- Open Finance
- Financial Data
- Payments
- Fintech
- Account Linking
- Bank Data
- Africa
- Nigeria
- Financial Infrastructure
- Retired

## Timestamps

- **Created:** 2026-07-12
- **Modified:** 2026-07-12

## APIs

All base URLs below are historical (`https://api.okra.ng/v2`) and no longer
resolve. Documentation links point to the Internet Archive (Wayback Machine).

### Okra Auth API

Retrieves the authentication data tied to a linked bank account — account and
NUBAN details established when a customer connects a bank through the Okra
Widget (`POST /products/auths`, plus retrieval by id, customer, bank, and date).

- **Human URL:** [https://docs.okra.ng/reference/api/Auth](https://docs.okra.ng/reference/api/Auth)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Accounts API

Lists and retrieves the bank accounts a customer has linked
(`POST /products/accounts`; retrieval by id, customer, bank, balance, name).

- **Human URL:** [https://docs.okra.ng/reference/api/Account](https://docs.okra.ng/reference/api/Account)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Balance API

Real-time and cached balances for linked accounts (`POST /balance/check`,
`/balance/refresh`; retrieval by id, account, type, customer, date).

- **Human URL:** [https://docs.okra.ng/reference/api/Balance](https://docs.okra.ng/reference/api/Balance)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Transactions API

Categorized transaction history (`POST /transactions/process`,
`/transactions/refresh`; retrieval by id, account, bank, type, NUBAN, customer,
date; downloadable statement via `/products/transactions/download`).

- **Human URL:** [https://docs.okra.ng/reference/api/Transactions](https://docs.okra.ng/reference/api/Transactions)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Identity API

Verified identity profile attached to a linked account (`POST /products/identities`,
`/products/identity/merge`; retrieval by id, customer, date).

- **Human URL:** [https://docs.okra.ng/reference/api/Identity](https://docs.okra.ng/reference/api/Identity)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Income API

Income and affordability signals derived from linked transactions
(`POST /products/income/process`, `/products/income/get`).

- **Human URL:** [https://docs.okra.ng/reference/api](https://docs.okra.ng/reference/api)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Verification (KYC) API

Nigerian KYC checks via `/products/kyc/*` — `bvn-verify`, `nuban-verify`,
`nuban-name-verify`, `tin-verify`, `rc-tin-verify`, `rc-verify`, `customer-verify`.

- **Human URL:** [https://docs.okra.ng/reference/api](https://docs.okra.ng/reference/api)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Payments API

Bank-to-bank payments and recurring direct-debit authorizations
(`POST /pay/initiate`, `/pay/verify`, `/pay/link/create`, `/authorization/initiate`,
`/pay/authorization/reauth`, `/pay/authorization/cancel`, `/bulkfiles/initiate`).

- **Human URL:** [https://docs.okra.ng/reference/api/Payments](https://docs.okra.ng/reference/api/Payments)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Banks API

Reference list of connectable Nigerian banks (`POST /banks/list`, `/banks/getById`).

- **Human URL:** [https://docs.okra.ng/reference/api/Banks](https://docs.okra.ng/reference/api/Banks)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Customers API

End-user (customer) management (`/customers/list`, `/customers/find-customers-by`,
`/customers/flag`, `/customers/unflag`, `/customers/remove`).

- **Human URL:** [https://docs.okra.ng/reference/api/Customer](https://docs.okra.ng/reference/api/Customer)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Wallet API

Billing wallet that funded API usage (`/wallet/balance/check`, `/wallet/topups`,
`/wallet/autotopup`, `/wallet/threshold`).

- **Human URL:** [https://docs.okra.ng/reference/api/Wallets](https://docs.okra.ng/reference/api/Wallets)
- **Base URL:** `https://api.okra.ng/v2`

### Okra Reports API

Scheduled financial reports compiled from linked data (`/reports/schedule`,
`/reports/details`, `/reports/download`).

- **Human URL:** [https://docs.okra.ng/reference/api](https://docs.okra.ng/reference/api)
- **Base URL:** `https://api.okra.ng/v2`

## Common Properties

- [GitHub Organization](https://github.com/okraHQ)
- [LinkedIn](https://www.linkedin.com/company/okrafinance)
- [Website](https://okra.ng) — now a parked page; not operated by Okra
- [Documentation (Wayback)](https://web.archive.org/web/20240418181836/https://docs.okra.ng/reference/api)
- [Plans](plans/okra-africa-plans-pricing.yml)
- [Rate Limits](rate-limits/okra-africa-rate-limits.yml)
- [Fin Ops](finops/okra-africa-finops.yml)

## Provenance

- **Confirmed** (base URL, auth scheme, endpoint paths): Okra's official Node SDK
  [`okraHQ/okra-node`](https://github.com/okraHQ/okra-node) (archived read-only
  2024-02-09) — `src/okra-client.js`, `src/models/models.js`, `src/utils/req-wrapper.js`.
- **Confirmed** (product surface, docs structure): Wayback Machine snapshots of
  `docs.okra.ng/reference/api/*` (2024–2024).
- **Modeled** (request/response bodies in the OpenAPI): reconstructed from the SDK
  parameter models and archived docs; individual field-level schemas are
  illustrative, not authoritative.
- **Shutdown**: reported by Nairametrics, TechCabal/TheCable, Launch Base Africa,
  and others (Okra ceased operations May 2025).

## Maintainers

**FN:** Kin Lane
**Email:** kin@apievangelist.com
