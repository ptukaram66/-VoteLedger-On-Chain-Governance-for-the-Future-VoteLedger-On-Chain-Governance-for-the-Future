# ⬡ VoteLedger — On-Chain Governance for the Future

> Decentralized, unstoppable polling powered by **Stellar Soroban Smart Contracts**. Every vote is immutable, transparent, and tamper-proof on-chain.

[![CI/CD Pipeline](https://github.com/shritesh263/Nexsuspoll/actions/workflows/ci.yml/badge.svg)](https://github.com/shritesh263/Nexsuspoll/actions/workflows/ci.yml)
[![Test Suite](https://github.com/shritesh263/Nexsuspoll/actions/workflows/test.yml/badge.svg)](https://github.com/shritesh263/Nexsuspoll/actions/workflows/test.yml)
[![Deploy](https://github.com/shritesh263/Nexsuspoll/actions/workflows/deploy.yml/badge.svg)](https://github.com/shritesh263/Nexsuspoll/actions/workflows/deploy.yml)
[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://nexsuspoll.vercel.app)
[![Mobile Ready](https://img.shields.io/badge/mobile-ready-blue)](https://nexsuspoll.vercel.app)

---

## 🎬 Demo Video (1 Minute)

> A full walkthrough of the NexusPoll dApp — wallet connection, poll creation, on-chain stats, and the poll broadcast interface.

<video src="media/demo3.mp4" controls width="100%"></video>

**▶️ [Download / Watch Demo Video](media/demo3.mp4)**

The demo covers:
- Live governance stats dashboard (Total Polls, Votes Cast, Treasury XLM, Trust Score)
- Freighter & Albedo wallet connection flow on Stellar Testnet
- Navigating the "Deploy a New Poll" form (Question + Option A/B inputs)
- Hovering the **Broadcast to Chain** button — triggering the inter-contract call UI
- Responsive layout and full-page mobile-optimized design

---

## 🌐 Production Dashboard
**🔗 [Open Live](https://nexsuspoll.vercel.app)**

## 📱 Mobile Quick Access
Scan this QR code to open the VoteLedger protocol on your mobile device instantly. The UI is 100% optimized for mobile browsers.

<div align="center">
  <img src="https://api.qrserver.com/v1/create-qr-code/?size=160x160&data=https://nexsuspoll.vercel.app" alt="NexusPoll QR Code" width="160"/>
  <br/>
  <b><a href="https://nexsuspoll.vercel.app">nexsuspoll.vercel.app</a></b>
</div>

---

## 🌟 Features
| Feature | Implementation |
|---|---|
| **Inter-Contract Architecture** | `NexusPoll` contract calls `Vault` contract via cross-contract invocation |
| **Multi-Wallet Support** | Integrated with **Freighter Mobile** and **Albedo** |
| **Soroban Logic** | Core governance logic powered by Rust-based Soroban engine |
| **Cosmic Glass UI** | Deep space aesthetic with high-intensity glassmorphism & aurora gradients |
| **Trust Scoring** | Real-time security calculation via client-side Rust WASM |
| **Mobile UX** | Optimized touch targets and responsive grid layout |

---

## 📁 Project Structure
```
.
├── index.html              # Core application interface (NexusPoll)
├── app.js                  # Application logic & blockchain integration
├── style.css               # Production-grade cyberpunk neon styles
├── wasm_utils.wasm         # Compiled Rust logic for trust scores
│
├── contract/               # Soroban Smart Contracts (Rust)
│   ├── src/lib.rs          # NexusPoll (Core) & Vault (Treasury) implementation
│   ├── Cargo.toml          # Dependency management
│   └── deploy.sh           # Testnet deployment automation
│
├── wasm_utils/             # Rust utility source
├── media/                  # Screenshots & assets
└── .github/workflows/      # CI/CD Pipelines (ci.yml, test.yml, deploy.yml)
```

---

## ⛓️ Advanced Architecture: Inter-Contract Calls
NexusPoll implements a modular dual-contract architecture:
- **NexusPoll (Core)**: Handles poll lifecycle, voting authentication, and event emission.
- **Vault (Treasury)**: Acts as a central protocol treasury for creation fees.
- **The Flow**: When a new poll is deployed, `NexusPoll` triggers an **Inter-Contract Call** to `Vault::deposit`, charging a protocol creation fee and demonstrating real cross-contract state transitions on Soroban.

---

## 🧪 Smart Contract Tests — Results

The contract includes **4 automated tests** covering all critical paths. Run locally with:

```bash
cd contract
cargo test
```

### Test Results

| # | Test Name | What It Verifies | Expected Result | Status |
|---|-----------|-----------------|-----------------|--------|
| 1 | `test_inter_contract_call` | Creating a poll triggers the Vault inter-contract call, depositing 10 units. Both `stats.treasury_balance` and `vault.get_balance()` equal 10. | `assert_eq!(stats.treasury_balance, 10)` and `assert_eq!(vault.get_balance(), 10)` | ✅ PASS |
| 2 | `test_vote_increments_correctly` | Voting option A increments `votes_a` to 1; voting option B from a different address increments `votes_b` to 1. | `votes_a == 1`, `votes_b == 1` | ✅ PASS |
| 3 | `test_double_vote_prevention` | The same voter address cannot cast a second ballot on the same poll — the contract panics with `"Already voted"`. | `#[should_panic(expected = "Already voted")]` | ✅ PASS |
| 4 | `test_invalid_choice_rejected` | Attempting to vote with a symbol other than `"A"` or `"B"` (e.g. `"C"`) panics with `"Invalid choice"`. | `#[should_panic(expected = "Invalid choice")]` | ✅ PASS |

### Sample Test Output
```
running 4 tests
test test::test_inter_contract_call       ... ok
test test::test_vote_increments_correctly ... ok
test test::test_double_vote_prevention    ... ok
test test::test_invalid_choice_rejected   ... ok

test result: ok. 4 passed; 0 failed; 0 ignored; 0 measured; 0 filtered out
```

---

## ⚙️ CI/CD Pipelines

Three GitHub Actions workflows run automatically on every push and pull request:

### Workflow 1 — `ci.yml` · Main CI/CD Pipeline
**Trigger:** Push or PR to `main`/`master`

| Job | What It Does |
|-----|-------------|
| `test-contract` | Installs Rust, caches Cargo deps, runs `cargo test --verbose`, then builds the WASM binary |
| `test-wasm-utils` | Installs Rust, runs `cargo test` on the WASM utilities module |
| `lint` | Enforces `cargo fmt` formatting and runs `cargo clippy` with zero warnings |
| `deploy-preview` | Deploys a Vercel preview URL on every Pull Request |

**Badge:** [![CI/CD Pipeline](https://github.com/shritesh263/Nexsuspoll/actions/workflows/ci.yml/badge.svg)](https://github.com/shritesh263/Nexsuspoll/actions/workflows/ci.yml)

---

### Workflow 2 — `test.yml` · Full Test Suite
**Trigger:** Push to `main`, `master`, or `develop`; PR to `main`/`master`

| Job | What It Does |
|-----|-------------|
| `contract-tests` | Runs all 4 Soroban unit tests (`cargo test --verbose`), saves `test_results.txt` as a GitHub artifact |
| `wasm-tests` | Builds and tests the WASM utilities module |
| `integration-tests` | Validates HTML structure, checks JavaScript syntax with Node.js, and verifies all project assets exist |

**Badge:** [![Test Suite](https://github.com/shritesh263/Nexsuspoll/actions/workflows/test.yml/badge.svg)](https://github.com/shritesh263/Nexsuspoll/actions/workflows/test.yml)

---

### Workflow 3 — `deploy.yml` · Production Deploy
**Trigger:** Push to `main`/`master`

| Job | What It Does |
|-----|-------------|
| `deploy` | Installs Vercel CLI and deploys the latest build to production (`vercel --prod`) using a secure `VERCEL_TOKEN` secret |

**Badge:** [![Deploy](https://github.com/shritesh263/Nexsuspoll/actions/workflows/deploy.yml/badge.svg)](https://github.com/shritesh263/Nexsuspoll/actions/workflows/deploy.yml)

---

## ✅ Level 4 Performance Checklist
- [x] **Production Grade Architecture** — Dual-contract system with 6+ state-changing functions.
- [x] **Inter-Contract Connectivity** — Automated fee deposits to the Vault treasury on-chain.
- [x] **Portfolio & Assets** — Native XLM balance dashboard with secure transfer functionality.
- [x] **Enterprise CI/CD** — 3 automated GitHub workflows (ci.yml, test.yml, deploy.yml) for testing, build, and deployment.
- [x] **Contract Tests** — 4 unit tests covering inter-contract calls, vote counting, double-vote prevention, and invalid input rejection — all documented above with expected vs. actual results.
- [x] **Demo Video** — 1-minute walkthrough of the live dApp linked above.
- [x] **Premium UI/UX** — Cosmic Glass design system optimized for modern browsers.
- [x] **Mobile Optimization** — 100% responsive interface with mobile-friendly links.

---

## 🚀 Deployment Guide

### 1. Deploy to Vercel
1. Go to [Vercel](https://vercel.com/import/git) and connect your GitHub repo.
2. Vercel will auto-detect settings. Click **Deploy**.
3. Copy your URL and update the Live Demo link above.

### 2. CI/CD Pipeline
Three GitHub Actions workflows are included:
- `ci.yml` — Main build, lint & deploy-preview pipeline
- `test.yml` — Smart contract test runner (`cargo test`) + integration tests
- `deploy.yml` — Automated Vercel production deployment

### 3. Smart Contract Deployment
```bash
cd contract
stellar contract deploy --wasm target/wasm32-unknown-unknown/release/contract.wasm \
  --source <your-key> --network testnet
```

---

<p align="center">
  <strong>Built for the Stellar Development Challenge · 2026 · NexusPoll Protocol</strong>
</p>
