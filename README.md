
⸻


# VANTA Platform – Vault Mirroring & Capital-Aligned Revenue Engine 🚀🔐

<p align="center">
  <img src="https://i.postimg.cc/QdV16pcB/IMG-4837.jpg" width="700"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Vaults-Live-blue" />
  <img src="https://img.shields.io/badge/Mirroring-Deterministic-brightgreen" />
  <img src="https://img.shields.io/badge/Revenue-Capital%20Aligned-orange" />
  <img src="https://img.shields.io/badge/API-Packet%20Onboarding-purple" />
  <img src="https://img.shields.io/badge/Fees-Performance%20Share%20Enabled-red" />
  <img src="https://img.shields.io/badge/Execution-Broker%20Integrated-yellow" />
</p>

---

## 📑 Table of Contents
- [Overview](#-overview)
- [Vault Engine](#-vault-engine)
- [Execution Flow](#-execution-flow)
- [API Packet Onboarding](#-api-packet-onboarding)
- [Revenue Engine](#-revenue-engine)
- [DB Schemas](#-db-schemas)
- [Failure Modes](#-failure-modes)
- [Observability & Security](#-observability--security)
- [Why This Wins](#-why-this-wins)

---

## 🔎 Overview
VANTA Platform is not a signal seller, not a copy-trade bot, not a Discord screenshot farm.  
It is a **closed-loop vault mirroring OS**: followers connect their **own brokerage accounts** via API, mirror allocations in real-time, and fees are charged **only when profits are realized**.  

Every action is:
- **Deterministic** → allocations computed from conviction stack → vault JSON → execution queues.  
- **Auditable** → replay DAGs, immutable logs, and JSON memory snapshots.  
- **Capital-Aligned** → revenue tied directly to realized PnL, not hype.  

---

## 🏦 Vault Engine
Authoritative JSONs (Markets/Alpha shared via NFS):

- `/opt/vanta/memory/vault.json` → global vault registry & defaults  
- `/opt/vanta/memory/vault_overlay.json` → runtime modifiers (personas, flip mode, maintenance)  
- `/opt/vanta/memory/vault_allocation.json` → target weights (intent)  
- `/opt/vanta/memory/portfolio.json` → actual broker holdings (truth)  
- `/opt/vanta/memory/pnl_summary.json` → realized & MTM PnL  
- `/opt/vanta/memory/autotrade_queue.json` → staged orders for execution  

**Design Rule**: *allocation drives intent; portfolio drives truth; queues bridge the two.*

Example `vault.json`:

```json
{
  "vaults": [
    {
      "vault_id": "V_CORE",
      "base_currency": "USD",
      "crypto_enabled": true,
      "personas": ["risk_averse","contrarian","aggressive"],
      "risk": {
        "max_drawdown": 0.12,
        "max_single_pos_pct": 0.08
      },
      "mirroring": {
        "mode": "proportional",
        "min_account_equity": 5000,
        "fee": {"type":"performance_or_flat","flat_usd":2000,"perf_share":0.20}
      }
    }
  ]
}


⸻

⚡ Execution Flow

Mermaid sequence (signal → vault → broker):

sequenceDiagram
  participant Signals
  participant Vault
  participant Executor
  participant Broker
  participant Follower

  Signals->>Vault: conviction_score.json
  Vault->>Executor: vault_allocation.json
  Executor->>Broker: autotrade_queue.json
  Broker->>Follower: child orders filled
  Executor->>Vault: update portfolio.json
  Vault->>Ledger: write pnl_summary.json

Steps:
	1.	Signals → conviction stack produces targets.
	2.	Vault Engine → allocation vs portfolio diff.
	3.	Executor → builds broker orders.
	4.	Mirroring Engine → child orders fanned to followers.
	5.	PnL Engine → reconciles and logs realized PnL.

Every hop is logged, replayable, deterministic.

⸻

🧩 API Packet Onboarding

Users don’t “buy subs.” They drop an API packet:
	•	API packet = broker keys + persona prefs + fee agreement.
	•	Example:

{
  "user_id": "F_1042",
  "brokers": {
    "equities": {"adapter": "alpaca", "account_ref": "alpaca_F1042"},
    "crypto":   {"adapter": "coinbase", "account_ref": "cb_F1042"}
  },
  "persona": "risk_averse",
  "mirroring_mode": "proportional",
  "scale": 0.25,
  "fee_model": {"perf_share": 0.20}
}


⸻

💰 Revenue Engine

VANTA doesn’t sell screenshots. It enforces capital-aligned fees:
	•	Performance Share: default 20% of realized PnL.
	•	Flat Institutional: e.g., $2,000/mo for enterprises.
	•	Hybrid: greater of performance share or flat.

Fee Flow:
	1.	NAV snapshot at cycle start.
	2.	Manager orders executed → child orders mirrored.
	3.	Cycle-end → realized PnL reconciled.
	4.	Ledger entry written + Stripe/BTCPay auto-collect.

Example ledger entry:

{
  "user_id":"F_1042",
  "vault_id":"V_CORE",
  "fee_type":"perf_share",
  "pnl_gross":5000,
  "fee_usd":1000,
  "asof":"2025-09-23T00:00:00Z"
}

Transparency: followers see PnL vs fees side-by-side in dashboards.

⸻

🗄 DB Schemas

Postgres (canonical):

CREATE TABLE mirror_registry (
  id uuid PRIMARY KEY,
  follower_id uuid,
  vault_id text,
  mode text,
  scale numeric,
  max_pos_usd bigint,
  kill_switch boolean DEFAULT false
);

CREATE TABLE pnl_ledger (
  id bigserial PRIMARY KEY,
  user_id uuid,
  vault_id text,
  pnl_gross numeric,
  fee_usd numeric,
  created_at timestamptz DEFAULT now()
);


⸻

🚨 Failure Modes
	•	Broker outage → queues back-pressure, retry w/ exponential backoff.
	•	Crypto fragmentation → auto-bridging via USD⇄USDC stable rails.
	•	Drift → reconciliation aligns follower portfolio to target.
	•	Flip Mode TTL → chaos branches expire, auto-revert to baseline.

⸻

🔒 Observability & Security
	•	RBAC → Alpha (overlay), Markets (targets), Executor (orders).
	•	Kill switches → global or per follower.
	•	Audit DAGs → every signal → order → fill replayable.
	•	Immutable Logs → trade_log.jsonl append-only.
	•	Secrets → broker keys in Vault, never in JSON.
	•	Determinism → NAV snapshot ensures consistent scaling across followers.

⸻

🏆 Why This Wins
	•	Not subscription-based hype → PnL-based trust.
	•	Not copy-trade bots → deterministic, auditable mirroring.
	•	Not screenshots → JSON, DAGs, replay logs.
	•	Capital routes across fiat + crypto seamlessly (USD⇄USDC⇄BTC).
	•	Followers earn, managers earn, VANTA earns — aligned at the ledger.

This is years ahead of retail bots.
It is the institutional-grade vault mirroring OS.

