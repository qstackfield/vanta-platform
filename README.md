<p align="center">
  <img src="https://i.postimg.cc/QdV16pcB/IMG-4837.jpg" alt="VANTA Platform Banner" width="90%" />
</p>

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
Where **VANTA OS** is the autonomous brain, **VANTA Platform** productizes it — turning vaults, mirroring, and governance into a **subscription-based, investor-ready service**.  

It handles:
- Subscriptions & billing (Stripe + crypto)
- Vault mirroring (custody-safe, manager→follower execution)
- Entitlements & feature flags
- Broker/webhook orchestration
- API & dashboard endpoints for users, partners, and enterprises

---

## 📑 Table of Contents

- [🌌 Overview](#-overview)
- [👥 Tenancy & Personas](#-tenancy--personas)
- [🧩 Core Components](#-core-components)
- [🗂 Data Model](#-data-model)
- [📡 API Surface](#-api-surface)
- [⚙️ Mirroring Orchestrator](#-mirroring-orchestrator)
- [₿ Deep Crypto Awareness](#-deep-crypto-awareness)
- [🔑 Entitlements & Plans](#-entitlements--plans)
- [🔒 Security & Governance](#-security--governance)
- [📊 Observability & SLOs](#-observability--slos)
- [💾 Storage Layout](#-storage-layout)
- [🚀 Deployment & Isolation](#-deployment--isolation)
- [🛡️ Failure Modes & Guards](#-failure-modes--guards)
- [🔗 File ↔ Repo Mapping](#-file-↔-repo-mapping)
- [💰 Pricing & Monetization](#-pricing--monetization)
- [🛠 Roadmap](#-roadmap)
- [📚 Glossary](#-glossary)
- [🔗 Related Repositories](#-related-repositories)

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
}(```
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
- **Hard Kill Paths**: vault overlay = maintenance.enabled OR follower.kill_switch=true.  
- **Deterministic Sizing**: always based on manager NAV snapshot, avoids drift.  
- **Retry Policy**: 1s → 5s → 15s → 60s → DLQ (`mirror_dispatch_dlx`).  
- **Reconciliation**: periodic reconciliation ensures child NAV matches manager NAV.  

---

### Why It Matters
- Followers get **provable fairness**: everyone sees the same proportional intent.  
- Managers get **governance**: vault-level guardrails, persona overlays, kill-switch.  
- Auditors get **immutability**: replayable DAG logs show the *exact path* of every mirrored order.  