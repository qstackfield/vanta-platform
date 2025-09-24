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

