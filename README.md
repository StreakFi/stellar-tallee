# 🧾 Tallee

**Every tab, tallied. Built on Stellar.**

Buy-now-pay-later for local shops and installment purchases, powered by Soroban smart contracts and settled in USDC on the Stellar network.

[![Built on Stellar](https://img.shields.io/badge/Built%20on-Stellar-brightgreen?style=flat-square&logo=stellar)](https://stellar.org/)
[![Soroban Smart Contracts](https://img.shields.io/badge/Soroban-Smart%20Contracts-dea584?style=flat-square&logo=rust)](https://soroban.stellar.org/)
[![TypeScript](https://img.shields.io/badge/TypeScript-Next.js-3178c6?style=flat-square&logo=typescript)](https://nextjs.org/)
[![License: MIT](https://img.shields.io/badge/License-MIT-green.svg?style=flat-square)](LICENSE)
[![Stellar Wave](https://img.shields.io/badge/Stellar-Wave%20Program-blue?style=flat-square)](https://www.drips.network/wave/stellar)

---

## Why Stellar?

Tallee is built entirely on the **Stellar network** because Stellar is purpose-built for what we're doing:

- **Near-zero transaction fees** — settling a ₦500 tab costs fractions of a cent. No merchant or customer is priced out.
- **USDC on Stellar** — stable, dollar-denominated payments without bank accounts. Customers and merchants transact in a currency that doesn't lose value overnight.
- **Soroban smart contracts** — programmable logic for credit limits, installment schedules, late fees, and ownership certificates — all enforced on-chain, not by trust.
- **5-second finality** — settlements confirm before the customer leaves the shop. No pending transactions, no "it's still processing."
- **Stellar anchors** — future integration with local on/off ramps means customers can fund wallets with mobile money (M-Pesa, OPay, Flutterwave) and settle tabs without ever touching crypto directly.
- **Global reach** — Stellar's cross-border rails mean a merchant in Lagos and a customer who relocated to London can still maintain and settle a tab seamlessly.

Every contract, every settlement, every receipt in Tallee lives on Stellar.

---

## The Problem

Millions of people across Africa, Latin America, and Southeast Asia buy on credit at their local shop every day — a running "tab" settled at month end. Sellers also offer installment plans for phones, laptops, and electronics ("Easy Buy" / "pay small small"). Today, all of this runs on **paper notebooks and handshakes**. Disputes are common. Records get lost. Trust breaks down.

## The Solution

Tallee puts informal credit on the **Stellar blockchain**. Merchants register their shop, add customers by phone number, and record purchases. **Soroban smart contracts** track every balance, enforce credit limits, and handle **USDC settlements on Stellar**. Both merchant and customer see the same transparent ledger — no more "I already paid" arguments.

---

## Features

### 📒 Credit Tabs

Merchants record daily purchases on a customer's tab. The running balance updates in real time with configurable credit limits. Settlement happens in **USDC on Stellar** — full, partial, or auto-deducted when the customer deposits.

### 🛒 Easy Buy (Installment Purchases)

Customers buy high-value items (phones, electronics, furniture) and pay in monthly installments — the "pay small small" model used across Nigerian markets. A **Soroban contract** tracks every payment, enforces due dates, applies late fees after a grace period, and issues an **on-chain ownership certificate on Stellar** when fully paid. If the customer defaults, the merchant gets verifiable on-chain proof for repossession.

### 🔔 Payment Reminders

Automated SMS and push notifications: 3 days before, 1 day before, and on the due date. Overdue alerts for merchants. Settlement confirmations for both sides.

### ⚖️ Dispute Resolution

Either party can raise a dispute. The **on-chain transaction history on Stellar** serves as immutable evidence. Optional third-party arbitration for unresolved cases.

### 🧾 On-Chain Receipts

Every settlement generates a structured receipt stored as a **Soroban event on the Stellar ledger** — audit-ready, tax-ready, dispute-proof.

---

## How It Works

```
Merchant creates shop → Adds customer (phone number)
     ↓
[CREDIT TAB]                         [EASY BUY]
Records daily purchases              Creates installment plan
     ↓                                    ↓
Balance tracked on Soroban           Customer accepts + pays down payment
     ↓                                    ↓
Customer settles in USDC             Monthly payments tracked on Stellar
     ↓                                    ↓
Receipt on Stellar ledger            All paid → Ownership certificate on-chain
                                     Default → Repossession claim (on-chain proof)
```

**All transactions settle on the Stellar network. All contract logic runs on Soroban.**

---

## Tech Stack

| Layer               | Technology                    | Role                                                                       |
| ------------------- | ----------------------------- | -------------------------------------------------------------------------- |
| **Smart Contracts** | **Rust / Soroban**            | Tab logic, settlements, Easy Buy, disputes — deployed on **Stellar**       |
| **Settlement**      | **USDC on Stellar**           | All payments flow through Stellar's native USDC asset                      |
| **Backend API**     | Rust / Axum                   | REST API, **Stellar Horizon + RPC** integration, phone auth, notifications |
| **Frontend**        | TypeScript / Next.js          | PWA with **Stellar wallet connection** (Freighter / Lobstr)                |
| **Database**        | PostgreSQL / SQLx             | Off-chain indexing, user profiles, session management                      |
| **Network**         | **Stellar Testnet → Mainnet** | Testnet for development, mainnet for production                            |

---

## Soroban Contracts

Five smart contracts deployed on the **Stellar network via Soroban**:

| Contract            | What It Does                                                                      |
| ------------------- | --------------------------------------------------------------------------------- |
| `tallee-registry`   | Shop profiles, customer onboarding, phone-to-Stellar-address mapping              |
| `tallee-ledger`     | Tab entries, running balances, credit limits, transaction history                 |
| `tallee-settlement` | Full/partial USDC payments on Stellar, auto-settle on deposit, receipt generation |
| `tallee-disputes`   | Dispute lifecycle — raise, submit evidence, resolve, escalate                     |
| `tallee-easybuy`    | Installment plans, payment schedules, late fees, on-chain ownership certificates  |

---

## Quick Start

### Prerequisites

- Rust 1.77+ with [`soroban-cli`](https://soroban.stellar.org/docs/getting-started/setup)
- Node.js 20+
- PostgreSQL 15+
- [Stellar Testnet account](https://laboratory.stellar.org/#account-creator?network=test) — fund with friendbot

### Setup

```bash
# Clone
git clone https://github.com/your-org/stellar-tallee.git
cd stellar-tallee

# Build Soroban contracts
cargo build --workspace

# Deploy contracts to Stellar Testnet
./scripts/deploy-testnet.sh

# Start backend
cd backend && cargo run

# Start frontend (new terminal)
cd frontend && npm install && npm run dev
```

App runs at `http://localhost:3000` — connect your **Freighter wallet** (Stellar) to interact.

---

## Project Structure

```
stellar-tallee/
├── contracts/              # 5 Soroban smart contracts (Rust) — deployed on Stellar
│   ├── tallee-registry/
│   ├── tallee-ledger/
│   ├── tallee-settlement/
│   ├── tallee-disputes/
│   └── tallee-easybuy/
├── backend/                # REST API (Rust + Axum) — Stellar RPC + Horizon integration
├── frontend/               # PWA (Next.js) — Stellar wallet connection
├── docs/                   # Architecture & API docs
└── scripts/                # Stellar testnet deploy scripts
```

---

## Contributing

Tallee is part of the **Stellar Wave Program** on Drips — a monthly bounty cycle for growing the Stellar open-source ecosystem. Contributors earn real rewards for solving issues.

1. Browse open issues labeled `Stellar Wave`
2. Apply via the [Drips Wave app](https://www.drips.network/wave/stellar)
3. Read [`docs/contributing.md`](docs/contributing.md) for code standards

Issues are tagged by complexity:

- **Trivial** (100 pts) — small fixes, minor features
- **Medium** (150 pts) — standard features, API endpoints
- **High** (200 pts) — complex Soroban contract logic, core architecture

---

## Roadmap

- [x] Core tab contracts on Soroban (registry, ledger, settlement)
- [x] Backend API with Stellar RPC integration
- [x] Easy Buy installment contract on Soroban
- [ ] Dispute resolution contract
- [ ] PWA with offline support
- [ ] Multi-asset support (XLM, USDC, Stellar-based local stablecoins)
- [ ] Merchant analytics dashboard
- [ ] SMS-only mode (no smartphone required)
- [ ] Credit scoring from on-chain payment history
- [ ] Stellar anchor integration for mobile money on/off ramps
- [ ] Multi-language support (Yoruba, Igbo, Hausa, Pidgin)

---

## Stellar Resources

- [Stellar Developer Docs](https://developers.stellar.org/)
- [Soroban Smart Contracts](https://soroban.stellar.org/)
- [Stellar Laboratory](https://laboratory.stellar.org/)
- [Freighter Wallet](https://freighter.app/)
- [Stellar Wave Program](https://www.drips.network/wave/stellar)

---

## License

MIT — use it, fork it, build on it.
