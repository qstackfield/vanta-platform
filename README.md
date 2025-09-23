# VANTA OS – Autonomous Capital Intelligence Stack 📊🔐

<p align="center">
  <img src="https://i.postimg.cc/QdV16pcB/IMG-4837.jpg" width="800"/>
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Python-3.10+-blue" />
  <img src="https://img.shields.io/badge/Build-passing-brightgreen" />
  <img src="https://img.shields.io/badge/Coverage-85%25-green" />
  <img src="https://img.shields.io/badge/Dependencies-up%20to%20date-success" />
  <img src="https://img.shields.io/badge/Code%20Style-black-black" />
  <img src="https://img.shields.io/badge/License-All%20Rights%20Reserved-red" />
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Secure-By%20Design-blue" />
  <img src="https://img.shields.io/badge/Audit-Immutable%20Logs-orange" />
  <img src="https://img.shields.io/badge/Uptime-99.9%25-brightgreen" />
  <img src="https://img.shields.io/badge/Monitoring-Enabled-blue" />
  <img src="https://img.shields.io/badge/Drift%20Detection-<24h-red" />
</p>

---

## 📑 Table of Contents
- [Overview](#overview)
- [Vault Layer](#vault-layer)
- [Execution Flow](#execution-flow)
- [Revenue Engine](#revenue-engine)
- [API Packet Onboarding](#api-packet-onboarding)
- [Transparency & Auditability](#transparency--auditability)
- [System Status](#system-status)
- [Contributors](#contributors)

---

## 🔎 Overview
VANTA OS is a **production-grade autonomous capital intelligence system**. Unlike “signal groups” or “screenshot scrapers,” VANTA is a **closed-loop execution OS**: signals → vaults → allocations → broker execution → replayable audit DAGs.

- **Mirrored Vaults** → Users don’t “copy trades” — they connect broker APIs and VANTA mirrors vault allocations deterministically.  
- **Revenue model** → No “subscriptions for screenshots.” Fees are capital-aligned (performance share or flat).  
- **Transparency** → Every order, fee, and realized PnL is auditable.

---

## 🔐 Vault Layer
Authoritative JSONs live in `/opt/vanta/memory/`:
- `vault.json` → global vault registry & defaults  
- `vault_overlay.json` → runtime modifiers (flip mode, persona boosts, maintenance)  
- `vault_allocation.json` → target weights (intent)  
- `portfolio.json` → broker holdings (truth)  
- `pnl_summary.json` → realized & MTM PnL  
- `autotrade_queue.json` → staged orders for execution  

**Design Rule:** Allocation drives intent → portfolio drives truth → queues bridge the two.

### Example `vault.json`
```json
{
  "vaults": [
    {
      "vault_id": "V_CORE",
      "label": "Core Discretionary",
      "base_currency": "USD",
      "crypto_enabled": true,
      "fiat_enabled": true,
      "personas": ["risk_averse","contrarian","aggressive"],
      "risk": {
        "max_drawdown": 0.12,
        "max_single_pos_pct": 0.08
      },
      "mirroring": {
        "mode": "proportional",
        "min_account_equity": 5000,
        "fee": {
          "type": "performance_or_flat",
          "flat_usd": 2000,
          "perf_share": 0.20
        }
      }
    }
  ]
}