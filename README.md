<p align="center">
  <img src="https://i.postimg.cc/QdV16pcB/IMG-4837.jpg" alt="VANTA Platform Banner" width="90%" />
</p>

👋 New to VANTA Platform?

- 🧠 Looking for the core intelligence engine? Visit the [VANTA OS Repository](https://github.com/qstackfield/vanta-capital-intelligence-os).  
- 📖 Want the high-level overview of the whole project? Start with the [Investor Landing Page](https://qstackfield.github.io/vanta-capital-intelligence-os/).  
- 💬 All design, roadmap, and Q&A are open → [Join the VANTA Discussions](../../discussions).  

---

<p align="center">
  <strong>VANTA Platform – Subscriptions & Vault Mirroring</strong><br>
  <em>The user-facing layer for governed, replayable autonomous capital.</em>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Build-passing-brightgreen" />
  <img src="https://img.shields.io/badge/License-All%20Rights%20Reserved-red" />
  <img src="https://img.shields.io/badge/Version-Platform%20v1.0-blue" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Auth-OIDC%2FJWT-purple" />
  <img src="https://img.shields.io/badge/Payments-Stripe%20%2B%20Crypto-green" />
  <img src="https://img.shields.io/badge/Mirroring-Deterministic%20%2B%20Governed-orange" />
</p>

---

## 🌟 Funding & Support

Help fuel the next stage of **autonomous capital intelligence**.  
Support development directly:

[![Strategic Partner](https://img.shields.io/badge/Strategic%20Partner-%F0%9F%8E%AF-blue?style=for-the-badge)](https://buy.stripe.com/eVqdR96ahdqIb69cSVbZe03)  
[![Partner](https://img.shields.io/badge/Partner-%F0%9F%A4%9D-green?style=for-the-badge)](https://buy.stripe.com/cNi9AT56d5Yg4HL8CFbZe04)  
[![Sponsor](https://img.shields.io/badge/Sponsor-%F0%9F%9A%80-purple?style=for-the-badge)](https://buy.stripe.com/7sY00jbuBaew3DHcSVbZe05)  

Or contribute via **Bitcoin**:  
`bc1qagw2a6zz2qck8kqaaxtpe0tv28n0fu9xm3c2e0`

---

## 👋 Introduction  

VANTA Platform is the **user-facing control plane** for the VANTA ecosystem.  
Where **VANTA OS** is the autonomous brain, **VANTA Platform** productizes it - turning vaults, mirroring, and governance into a **subscription-based, investor-ready service**.  

It handles:
- Subscriptions & billing (Stripe + crypto)
- Vault mirroring (custody-safe, manager→follower execution)
- Entitlements & feature flags
- Broker/webhook orchestration
- API & dashboard endpoints for users, partners, and enterprises

---

## 📑 Table of Contents  

- [👋 Introduction](#-introduction)  
- [🌌 Overview](#-overview)  
- [👥 Tenancy & Personas](#-tenancy--personas)  
- [🧩 Platform Components](#-platform-components)  
- [🗂 Data Model](#-data-model)  
- [🔌 API Surface](#-api-surface-selected)  
- [🔄 Mirroring Orchestrator](#-mirroring-orchestrator-state-machine)  
- [🌐 Deep Crypto Awareness](#-deep-crypto-awareness)  
- [📜 Entitlements & Plans](#-entitlements--plans)  
- [🔐 Security & Governance](#-security--governance)  
- [📈 Observability & SLOs](#-observability--slos)  
- [🗄️ Storage Layout](#-storage-layout-platform)  
- [🚀 Deployment & Isolation](#-deployment--isolation)  
- [🛡️ Failure Modes & Guards](#-failure-modes--guards)  
- [🌍 Public Webhook & API Specs](#-public-webhook--api-specs)  
- [🔄 End-to-End Mirroring](#-end-to-end-mirroring-manager--followers)  
- [💰 Pricing & Monetization](#-pricing--monetization)  
- [🛣️ Roadmap](#-roadmap)  
- [📖 Glossary](#-glossary)  
- [🚀 Why This Is From the Future](#-why-this-is-from-the-future)  
- [🔗 Explore More](#-explore-more)  

---

## 🌌 Overview  

The **VANTA Platform** is the **product layer** of the VANTA ecosystem.  
It transforms the autonomous intelligence of **VANTA OS** into a **scalable, investor-ready platform** with subscriptions, mirroring, governance, and custody-safe execution.

Key functions:  
- **Subscriptions & Entitlements**  
  - Tiered plans unlock vaults, personas, flip-mode access, and replay/audit features.  
  - Billing managed via Stripe (fiat) and BTC (crypto).  

- **Vault Mirroring**  
  - Followers keep funds in their **own broker accounts**.  
  - The platform mirrors manager vaults deterministically (proportional or capped).  
  - Zero custody — VANTA never touches user capital.  

- **Cross-Rail Capital**  
  - Supports **fiat + crypto vaults**.  
  - Routes USD⇄USDC⇄assets as part of execution intent.  

- **Explainable Automation**  
  - Every decision links to **reason vectors + audit logs**.  
  - All actions are replayable for compliance and transparency.  

- **Separation of Concerns**  
  - **OS = brain** (signal → allocation → intent).  
  - **Platform = productization** (subscriptions, mirroring, user experience).  

> 💡 **Instead of selling signals, VANTA Platform productizes capital intelligence itself.**

---

## 👥 Tenancy & Personas  

The VANTA Platform is designed as a **multi-tenant control plane**, separating roles, users, and mirroring participants with clear governance.  

### Tenancy Model  
- **Tenants** → one tenant per customer org (e.g., manager, enterprise client).  
- **Users** → members of a tenant (roles: owner, ops, auditor).  
- **Followers** → external user records tied to broker accounts (mirroring vaults).  

### Personas (from OS layer)  
- **Athena** → risk-averse, defensive allocator.  
- **Apollo** → aggressive, growth-seeking allocator.  
- **Ares** → contrarian, chaos-driven allocator.  
- **Nemesis** → hedged, risk-balancing persona.  

### Flip Mode  
- Followers can temporarily enable **alternate execution branches**.  
- Parameters:  
  - TTL (time-to-live) enforced (e.g., 30–60 minutes).  
  - Amplify factor (e.g., +0.35 weighting).  
  - Auto-revert after TTL expiration.  

### Why This Matters  
- **Governed Access:** Tenancy ensures clean separation of orgs and roles.  
- **Persona Diversity:** Followers gain differentiated exposure without code or models.  
- **Safety Nets:** Flip Mode guarantees experiments are **bounded, reversible, and auditable**.  

---

## 🧩 Platform Components  

The VANTA Platform control plane is composed of modular services:  

- **Web App (Next.js)** → user interface for onboarding, subscriptions, and dashboards.  
- **API Gateway** → JWT verification, scopes, idempotency keys, and rate limiting.  
- **AuthN/Z Service** → OIDC + RBAC for tenants, users, and followers.  
- **Subscription & Billing Service** → Stripe integration (plans, upgrades, invoices, refunds).  
- **Entitlements Service** → central feature flags (core, pro, institutional), cached in Redis.  
- **Vault Registry Service** → authoritative vault metadata and follower bindings; references OS JSONs.  
- **Mirroring Orchestrator** → expands manager orders into follower child orders, applies caps/scales.  
- **Webhook Dispatcher** → HMAC-signed POSTs to followers; retries with backoff.  
- **Broker Adapters** → direct adapters for Alpaca, Tradier, Coinbase, etc.  
- **Event Bus (Kafka/NATS)** → async messaging backbone for mirroring events.  
- **Storage Layer**:  
  - Postgres → tenants, users, vaults, followers, audit logs.  
  - Redis → idempotency keys and in-flight state.  
  - S3/Minio → immutable artifacts, logs, and exports.  

---

## 🗂 Data Model  

The VANTA Platform persists state across Postgres, Redis, and object storage. Core tables and their purpose:

- **tenants**  
  - `tenant_id (uuid)` · `name` · `created_at` · `status`  

- **users**  
  - `user_id (uuid)` · `tenant_id` · `email` · `role (owner|ops|auditor)` · `oidc_sub`  

- **subscriptions**  
  - `subscription_id` · `tenant_id` · `plan_id` · `status` · `entitlements (jsonb)` · `renewal_at`  

- **vaults**  
  - `vault_id` · `tenant_id (manager)` · `label` · `rails {fiat,crypto}` · `personas[]` · `risk_profile (jsonb)` · `public (bool)`  

- **followers**  
  - `follower_id` · `tenant_id (manager)` · `vault_id` · `mode (proportional|capped|shadow)`  
  - `scale (decimal)` · `max_pos_usd (decimal)` · `kill_switch (bool)`  
  - `webhook {url,hmac_key_ref}` OR `bridged_brokers {equities_ref, crypto_ref}`  

- **manager_orders**  
  - `mo_id` · `vault_id` · `symbol` · `venue` · `side` · `qty` · `tif` · `meta (jsonb)` · `state` · `created_at`  

- **follower_orders**  
  - `fo_id` · `mo_id` · `follower_id` · `symbol` · `qty` · `cap_applied (bool)` · `state` · `broker_order_ref`  
  - `dispatch_attempts` · `last_error` · `audit (jsonb)`  

- **audit_events**  
  - `event_id` · `entity (manager_order|follower_order|vault|subscription)` · `actor` · `payload (jsonb)` · `ts`  

---

## 🔌 API Surface (selected)

### Auth
- **POST /v1/auth/token** → OIDC code-exchange (handled by gateway).  
- **Scopes**:
  - `vault:read`
  - `mirror:manage`
  - `orders:read`
  - `follower:manage`
  - `billing:read`

---

### Vaults
- **GET /v1/vaults** → list visible vaults (entitlement filtered).  
- **GET /v1/vaults/{vault_id}** → metadata + risk + personas (redacted).  
- **POST /v1/vaults/{vault_id}/overlay** → apply flip mode/persona boosts (**TTL enforced**).  

---

### Followers & Mirroring
- **POST /v1/vaults/{vault_id}/followers** → register follower (webhook or bridged).  
- **PATCH /v1/followers/{follower_id}** → update caps/scale/kill_switch.  
- **GET /v1/followers/{follower_id}/preview?asof=...** → sizing preview based on latest NAV.  
- **GET /v1/manager-orders?since=...** → read manager intents.  
- **GET /v1/follower-orders?follower_id=...&since=...** → audit child orders.  

---

### Webhooks (follower-side)

- **POST /v1/hooks/mirror/dispatch** → HMAC signed delivery.  
- **Headers:**
  - `X-Vanta-Signature: sha256=HEX`
  - `X-Vanta-Timestamp`

#### Example Body

```json
{
  "ts": "2025-05-27T22:09:00Z",
  "follower_id": "F_1042",
  "vault_id": "V_CORE",
  "symbol": "AAPL",
  "side": "buy",
  "qty": 7,
  "time_in_force": "day",

  "reason_vector": [
    "SEC Form 4 Insider Buy",
    "Dark Pool Sweep > $5M",
    "Retail Surge (Reddit/WSB)",
    "Options Skew (calls >> puts)"
  ],

  "conviction": {
    "score": 0.87,
    "band": "A",
    "persona": "Apollo",
    "overrides": {
      "risk_averse": -0.05,
      "contrarian": +0.10
    }
  },

  "meta": {
    "manager_order_id": "M-98421",
    "scale": 0.20,
    "max_pos_usd": 2500,
    "kill_switch": false
  },

  "audit": {
    "dag_id": "DAG-472910",
    "dispatch_attempts": 1,
    "last_error": null,
    "state": "sent"
  },

"provenance": {
  "collector": "reddit_stealth.py",
  "enriched_at": "2025-05-27T22:08:32Z",
  "os_node": "Markets",
  "features_used": [
    "insider_cluster_embedding",
    "darkpool_flow_score",
    "retail_sentiment_spike"
  ]
}
```
---

## 🔄 Mirroring Orchestrator (State Machine)

The **Mirroring Orchestrator** is the control loop that transforms manager vault orders into **deterministic child orders** across all followers.  
It guarantees proportionality, risk caps, retry policies, and replayable audit logs.

### Flow

1. **[INGEST_MANAGER_ORDER]**  
   - Input from OS (`autotrade_queue.json`) or manager API.  
   - Sanity checks: vault open, no maintenance, no halt.  

2. **[EXPAND_TO_FOLLOWERS]**  
   - Load all registered followers for the vault.  
   - Apply entitlement rules (plan, persona overlay, flip mode).  

3. **[SIZE_CHILD_ORDERS]**  
   - Compute child qty = `floor(manager_qty × follower.scale)`.  
   - Enforce `max_pos_usd` caps per follower.  
   - Respect persona overlays (e.g., contrarian may invert or scale).  

4. **[DISPATCH]**  
   - Deliver to follower endpoint (webhook) or broker adapter (bridged mode).  
   - Signed with HMAC; retried with exponential backoff.  
   - States: `sent` → `ack` → `confirmed` OR → `retry`.  

5. **[CONFIRM]**  
   - Update state upon broker fill or webhook ack.  
   - Track partial fills + reconcile NAV.  

6. **[AUDIT]**  
   - Append to `trade_log.jsonl` and `audit_events`.  
   - DAG reference persisted: manager order → child orders → fills → audit.  

---

### Guards & Controls
- **Hard Kill Paths**: vault overlay = `maintenance.enabled` OR follower.kill_switch = true.  
- **Deterministic Sizing**: always based on manager NAV snapshot, avoids drift.  
- **Retry Policy**: 1s → 5s → 15s → 60s → DLQ (`mirror_dispatch_dlx`).  
- **Reconciliation**: periodic reconciliation ensures child NAV matches manager NAV.  

---

### Why It Matters
- Followers get **provable fairness**: everyone sees the same proportional intent.  
- Managers get **governance**: vault-level guardrails, persona overlays, kill-switch.  
- Auditors get **immutability**: replayable DAG logs show the *exact path* of every mirrored order.  

---
## 🌐 Deep Crypto Awareness

VANTA Platform is natively crypto-aware, bridging fiat and digital rails with deterministic execution logic.  
It ensures smooth routing, minimal fees, and resilient cross-rail allocations.

### 🔄 Bridging Logic
When a target vault requires crypto execution but a follower is on fiat rails:
1. Convert **USD → USDC** (fiat bridge).
2. Place **crypto order** (BTC, ETH, or supported asset).
3. Reconcile fills → update portfolio snapshot.

### 💸 Fee Model
- Venue-aware lookups choose the **cheapest execution path**.  
- Compares **CEX vs direct spot** routes within latency SLOs.  
- Optimized for both cost and speed.

### 🪙 Stablecoin Buffer
- Minimum buffer maintained in USDC to reduce churn.  
- Configurable at vault-level for institutional followers.  
- Protects against unnecessary conversions during high-frequency execution.

---

## 📜 Entitlements & Plans

Access to VANTA Platform is gated through **subscription plans** and enforced by entitlements.  
These entitlements are pushed as feature flags to the API/UI and verified server-side on every call.

### 📦 Core Plan
- 🔑 Access to **1 vault**  
- 📊 **Proportional mirroring only**  
- 🚫 No flip-mode  
- 👀 Audit logs read-only  

### 🚀 Pro Plan
- 🔑 Access to **multiple vaults**  
- 🎭 Persona boosts enabled  
- 🔄 **Flip-mode follow** (short-TTL overlays)  
- 📊 Replay dashboards for follower-level audits  

### 🏦 Institutional Plan
- 🛠️ Custom vault caps  
- 📡 **Dedicated webhook signing keys**  
- ⚡ Priority latency SLA  
- 🔗 API pull feed (direct data integration)  
- 👥 Multi-seat org onboarding  

### ✅ Enforcement
- Every entitlement is checked in the **Entitlement Service** before mirroring or API execution.  
- Stored as `jsonb` in `subscriptions` table with feature-level granularity.  
- Validated on every call — **no client-side trust**.  

---
## 🔐 Security & Governance

VANTA Platform is designed with **institutional-grade security** - every mirrored trade, webhook, and entitlement is protected and auditable.

### 🔑 Authentication
- **OIDC (Auth0/Okta/Keycloak)** for all tenants.  
- Short-lived **JWT access tokens**, with refresh via OIDC flows.  
- Scoped roles: `owner`, `ops`, `auditor`, `follower`.

### 🛂 Authorization
- **RBAC** (role-based access control) for tenant roles.  
- **ABAC** (attribute-based access control) ensures vault-level + follower-level scoping.  
- Persona overlays and flip-modes are enforced through entitlement checks.

### 🔒 Secrets & Storage
- **KMS / HashiCorp Vault** for all secret material.  
- Configs hold only secret references — never raw credentials.  
- Broker accounts stored as **opaque references** (never raw API keys in DB).

### 📡 Webhook Security
- All follower webhooks are **HMAC SHA-256 signed**.  
- Signature = `sha256(secret, timestamp + "." + raw_body)`.  
- Headers:  
  - `X-Vanta-Signature`  
  - `X-Vanta-Timestamp`  
- Replay protection: **5-minute validity window**.

### 🧾 Compliance & Audit
- **Append-only audit logs** for all actions.  
- Vaults, orders, and entitlements tied to immutable `audit_events`.  
- Export-ready for regulators, external auditors, or institutional partners.  

---
## 📈 Observability & SLOs

VANTA Platform includes **full-stack observability** - so every mirrored trade, webhook, and entitlement can be traced, measured, and audited.

### 📊 Metrics
- `mirror.dispatch.latency_ms` → P50 / P95 dispatch latency  
- `mirror.error.rate` → error ratio per vault/follower  
- `broker.submit.success_rate` → broker adapter confirmation success %  
- `webhook.retry.count` → retries per webhook/follower  

### 📑 Logs
- Structured JSON logs with correlation IDs `{mo_id, fo_id, follower_id}`.  
- Dedicated `mirror_dispatch.log` for webhook delivery + retry cycles.  
- All logs are immutable and rolled into object store daily.  

### 🔍 Tracing
- End-to-end tracing: `gateway → orchestrator → dispatcher → broker`.  
- OpenTelemetry instrumentation for latency + error attribution.  
- Visual dashboards (Grafana/Jaeger) for real-time visibility.  

### 🎯 Service-Level Objectives (SLOs)
- **Dispatch latency:** manager order → follower dispatch ≤ **2s (P95)**.  
- **Webhook reliability:** success rate ≥ **99.5%** (with retries).  
- **Audit durability:** 11x9s retention in object store (S3/MinIO).  
- **Availability:** 99.9% uptime target for API + mirroring core.

---

## 🗄️ Storage Layout (Platform)

The VANTA Platform is designed with **clear separation of state**, ensuring performance, reliability, and immutability across all components.

### 📂 Postgres (authoritative state)
- **Tenants** → org-level records, ownership, lifecycle.  
- **Users** → identity, roles, OIDC subs.  
- **Subscriptions** → Stripe state, entitlements JSON.  
- **Vault metadata** → labels, rails, personas, configs.  
- **Followers** → bindings, webhook URLs, kill switches.  
- **Orders** → manager + follower orders, state machines.  
- **Audit events** → immutable reference logs.

### ⚡ Redis (short-lived state)
- Idempotency keys for all POST/PATCH requests.  
- In-flight order state (before confirmation).  
- Rate-limit tokens (per IP, per user).  
- Session caches for entitlement lookups.  

### ☁️ Object Store (S3/MinIO)
- Immutable artifacts (audit exports, trade_log.jsonl rollups).  
- Daily vault snapshots.  
- Replay bundles for regulator/investor inspection.  
- Dead-letter queues (mirror_dispatch_dlx).  

### 🔗 Bridges to OS
- Reads directly from `/opt/vanta/memory/*.json` or via signed internal API.  
- Cached locally for latency, refreshed on demand.  
- Guarantees **OS → Platform determinism**: allocations flow into mirroring without drift.  

---

## 🚀 Deployment & Isolation

The VANTA Platform runs as a **multi-service containerized stack** with strict isolation between environments and components.  
The design prioritizes **HA (high availability)**, **low latency**, and **regulatory-grade auditability**.

### 🛠️ Services
- **API Gateway** → single ingress, WAF, TLS termination, JWT validation.  
- **Core Services** → Auth, Subscriptions, Vault Registry, Mirroring Orchestrator, Webhook Dispatcher.  
- **Adapters** → Broker adapters (Alpaca, Tradier, Coinbase, CEX/DEX bridges).  
- **Data Services** → Postgres, Redis, Object Store (S3/MinIO).  

### 🗂️ Namespaces & Environments
- **Dev** → fast iteration, feature flags enabled.  
- **Staging** → pre-production, mirrors prod infra but with shadow OS feeds.  
- **Prod** → hardened with RBAC, network policies, Vault-injected secrets.  

### 🔒 Network Isolation
- **East-West traffic** → private VPC-only (services talk over gRPC/HTTPS inside).  
- **Public ingress** → API Gateway only, behind Cloudflare WAF.  
- **Webhook egress** → outbound-only, via controlled egress gateway with allowlist.  

### 🌀 High Availability (HA)
- Stateless services (API, Orchestrator, Dispatcher) run ≥2 replicas.  
- Postgres in HA setup (primary + read replicas).  
- Redis cluster with sentinel for failover.  
- Object store with versioning and cross-region replication.  

### 🧩 Disaster Recovery (DR)
- PITR (point-in-time recovery) enabled for Postgres.  
- Snapshots of Redis every 5 minutes; restore tested weekly.  
- Object store replication across regions with lifecycle policies.  
- Infra as Code (Terraform + Helm charts) ensures **reproducible infra** on rebuild.  

---
## 🛡️ Failure Modes & Guards

The VANTA Platform is designed with **resilience-first principles**: every failure path is anticipated, logged, and controlled with guardrails.  
This ensures **determinism**, **safety for capital**, and **auditable recovery**.

### ⚠️ Broker / Exchange Outages
- Orders queue inside **Mirroring Orchestrator**.  
- Retries with exponential backoff → 1s, 5s, 15s, 60s.  
- If DLQ (dead-letter queue) reached, alerts raised to operator.  
- Followers unaffected; NAV reconciliation runs once broker recovers.

### 📡 Webhook Failures
- **4xx responses** → no retry (treated as terminal error, flagged in audit).  
- **5xx responses** → retried with backoff.  
- All attempts logged in `mirror_dispatch.log` with correlation IDs.  
- DLQ: `mirror_dispatch_dlx` ensures no intent is lost.

### 🔄 Drift & Reconciliation
- Periodic reconciliation compares **follower NAV vs manager NAV snapshot**.  
- If divergence > threshold, auto-fix-up orders generated (within caps).  
- Guarantees proportional mirroring even after missed orders or broker issues.

### ⏱️ Flip Mode Expiry
- Flip overlays always **time-bounded (TTL)**.  
- On expiry → vault overlay reverts automatically to baseline allocation.  
- Prevents indefinite high-risk allocations or chaos states.

### 🚨 Kill Switches
- **Vault-level:** `vault_overlay.maintenance.enabled=true` freezes dispatch globally.  
- **Follower-level:** `kill_switch=true` disables a single follower instantly.  
- Both enforceable via CLI or API (`PATCH /followers/{id}`).

### 🧯 Rate Limits & Safety Nets
- API Gateway → 60 RPM baseline per client, burstable at open.  
- Protects against bot floods and abuse.  
- Critical system calls require **Idempotency-Key headers** for replay safety.  

---
## 🌍 Public Webhook & API Specs

The VANTA Platform exposes a **secure API surface** and **signed webhooks** so followers and partners can integrate safely.  
All endpoints are idempotent, HMAC-signed, and fully audit-logged.

### 🔑 Webhook Signatures
- Every webhook is signed with **HMAC-SHA256** using a shared secret.  
- Headers include:
  - `X-Vanta-Timestamp` – request timestamp  
  - `X-Vanta-Signature` – signed digest of (timestamp + body)  

### 📡 Core API Routes

**Followers**
- `POST /v1/vaults/{vault_id}/followers` → register a follower  
- `PATCH /v1/followers/{follower_id}` → update scale, caps, or kill switch  
- `GET /v1/followers/{follower_id}/preview` → preview sizing on last NAV snapshot  

**Vaults**
- `GET /v1/vaults` → list available vaults  
- `GET /v1/vaults/{vault_id}` → vault metadata & personas (redacted)  
- `POST /v1/vaults/{vault_id}/overlay` → apply flip mode / persona boosts  

**Orders**
- `GET /v1/manager-orders?since=...` → stream manager intents  
- `GET /v1/follower-orders?follower_id=...` → audit follower child orders  

**Billing**
- `GET /v1/subscriptions/me` → return active plan + entitlements  
- `POST /v1/subscriptions/change-plan` → initiate Stripe checkout session  

### 🔒 Security
- All POST/PATCH routes require **Bearer JWT** + **Idempotency-Key** header.  
- Webhook events expire if not processed within 5 minutes.  
- Every request is written to `audit_events` with correlation IDs.  

---
## 🔄 End-to-End Mirroring (Manager → Followers)

The VANTA Platform ensures every **manager order** is deterministically expanded into **child orders** across all followers, with full fairness, governance, and replayable audit trails.

### Flow Overview

Manager Orders → Mirroring Orchestrator → Follower Accounts

1. Manager order generated (`autotrade_queue.json`)
2. Orchestrator expands order to all registered followers
3. Child orders sized by scale and capped per follower
4. Orders dispatched via HMAC webhooks or broker adapters
5. Fills confirmed, reconciled, and logged
6. Full DAG (manager → child → fills) is persisted for replay

### Key Properties
- **Proportional** – followers mirror allocations fairly based on scale.  
- **Capped** – per-position max enforced automatically.  
- **Replayable** – logs enable complete reconstruction.  
- **Safe** – kill switches + persona overlays respected.  
- **Transparent** – every step visible to auditors and partners.  

---

## 💰 Pricing & Monetization

VANTA Platform is designed with **aligned incentives** - we only succeed when our users and followers succeed.

### Revenue Streams
- **Performance Fees**  
  - % of profits (with high-water marks for fairness).  
  - Transparent: followers see PnL vs fees side-by-side.  

- **Subscription Plans**  
  - Core, Pro, and Institutional tiers.  
  - Unlocks vaults, personas, flip-mode, and audit dashboards.  

- **Institutional Add-Ons**  
  - Dedicated feeds, latency SLAs, custom adapters.  
  - Priority support and private vault strategies.  

### Fee Model Principles
- **Alignment:** no “pay for hype” — fees tied to actual capital outcomes.  
- **Transparency:** every fee logged alongside performance.  
- **Scalability:** works from a single retail follower to thousands of mirrored accounts.  

---
## 🛣️ Roadmap

The VANTA Platform is continuously evolving to push the frontier of autonomous capital intelligence.

### Near-Term
- White-label follower portal with self-serve onboarding.  
- Broker linking via secure API packets (Alpaca, Coinbase, Tradier).  
- Multi-vault persona strategies (Athena, Apollo, Ares).  
- Real-time dashboards for conviction bands & attribution.  

### Mid-Term
- Multi-region webhook PoPs for low-latency mirroring.  
- Federated policies for institutional tenants (custom caps & personas).  
- Replay Studio: follower-level “what-if” backtests on historic orders.  

### Long-Term
- Fully autonomous capital marketplace: vault managers + followers at scale.  
- Cross-rail liquidity routing (fiat ⇄ stablecoins ⇄ crypto ⇄ equities).  
- Partner vaults & institutional integrations with SLA governance.  

---
## 📖 Glossary

- **Vault** → Capital container with encoded risk rails, allocations, personas, and compounding rules.  
- **Follower** → External account (broker/crypto) that mirrors a vault under proportional or capped rules.  
- **Persona** → Named reasoning lens (e.g., Athena, Apollo, Ares) that biases allocations and strategy overlays.  
- **Flip Mode** → Short-TTL alternate execution path with amplified risk/reward, auto-reverts on expiry.  
- **Entitlement** → Feature rights tied to a subscription plan (e.g., access to vaults, flip mode, replay dashboards).  
- **Mirroring Orchestrator** → Engine that transforms manager orders into deterministic child orders for followers.  
- **Overlay** → Runtime adjustments applied to vaults (maintenance, persona boosts, flip branches).  
- **Audit DAGs** → Append-only logs that capture the full path: signal → conviction → allocation → trade → mirror.  
- **Manager Order** → Primary trade intent emitted by a vault.  
- **Child Order** → Scaled order dispatched to a follower based on mode and caps.  
- **Bridge** → Cross-rail capital routing logic (e.g., USD ⇄ USDC ⇄ BTC).  
- **Replay Studio** → Planned feature allowing historical “what-if” simulation for followers on past cycles.  

---
## 🚀 Why This Is From the Future

VANTA Platform is not an incremental tool - it’s a **new category of financial infrastructure**.  

- **Deterministic Mirroring** → Every follower sees the exact proportional intent, with auditable DAGs.  
- **Crypto-Aware Capital Routing** → Native support for USD ⇄ stablecoins ⇄ crypto execution.  
- **Separation of Concerns** → VANTA OS generates intent; VANTA Platform productizes it safely at scale.  
- **Governance by Design** → Kill-switches, caps, persona overlays, and flip-mode ensure safety.  
- **Replayable Autonomy** → Any order, vault, or follower path can be reconstructed for compliance or learning.  

> **This isn’t a bot. It’s the operating system capital markets will run on.**  

---

## 🔗 Explore More  

- **[VANTA OS - Autonomous Capital Intelligence Stack](https://github.com/qstackfield/vanta-capital-intelligence-os)**  
  Technical deep dive into the intelligence engine, vault logic, architecture, and server mapping.  

- **[VANTA Investor Landing Page](https://qstackfield.github.io/vanta-capital-intelligence-os/)**  
  High-level overview of the VANTA vision, value proposition, and funding opportunities.  