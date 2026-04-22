# ⬡ VoteLedger — On-Chain Governance for the Future

> Decentralized, unstoppable polling powered by **Stellar Soroban Smart Contracts**. Every vote is immutable, transparent, and tamper-proof on-chain.

[![CI/CD Pipeline](https://github.com/shritesh263/Nexsuspoll/actions/workflows/ci.yml/badge.svg)](https://github.com/shritesh263/Nexsuspoll/actions/workflows/ci.yml)
[![Live Demo](https://img.shields.io/badge/demo-live-brightgreen)](https://nexsuspoll.vercel.app)
[![Mobile Ready](https://img.shields.io/badge/mobile-ready-blue)](https://nexsuspoll.vercel.app)

## 🌐 Production Dashboard
**🔗 [Open  Live](https://nexsuspoll.vercel.app)**

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

## 🧪 Smart Contract Verification
1. **Inter-contract Logic**: Verifies that successful poll creation updates the Vault treasury balance.
2. **Authentication**: `require_auth()` ensures only legitimate voters can cast ballots.
3. **Prevention**: Built-in guards against double-voting and re-initialization.

**Run tests locally:**
```bash
cd contract
cargo test
```

---

## ✅ Level 4 Performance Checklist
- [x] **Production Grade Architecture** — Dual-contract system with 6+ state-changing functions.
- [x] **Inter-Contract Connectivity** — Automated fee deposits to the Vault treasury on-chain.
- [x] **Portfolio & Assets** — Native XLM balance dashboard with secure transfer functionality.
- [x] **Enterprise CI/CD** — 3 automated GitHub workflows for testing, build, and deployment.
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
- `ci.yml` — Main build & lint pipeline
- `test.yml` — Smart contract test runner (`cargo test`)
- `deploy.yml` — Automated Vercel deployment

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
