# TakumiPay — Monad Metropolis Hackathon 2026

> **Consumer Cross-Border Remittances & QRIS Merchant Settlement Powered by Monad**  
> *Seedless onboarding with Mera biometric passkeys, sub-second settlement with Agora AUSD, and AI-driven remittance via Takumi Agent.*

- **Team:** Planckify Labs
- **Track Entered:** Track 02 — Consumer Products & Payments
- **Targeted Sponsor Bounties:**
  - **Mera Bounty:** Passkey account layer as the entire onboarding experience (zero seed phrase)
  - **Agora Bounty:** Full on-chain Agora AUSD stablecoin integration
  - **Kimi Bounty:** Multi-agent orchestrator powered by Kimi K2.6 driving conversational remittance
- **License:** [GNU General Public License v3.0 (GPLv3)](./LICENSE)

---

## The Vision

Cross-border remittance is the definitive consumer application where on-chain rails provide immediate, tangible superiority over traditional banking:
- Migrant workers in Southeast Asia routinely endure 2–5 day settlement delays and 5–10% hidden foreign exchange markups.
- Crypto solutions historically failed these users because of UX friction: seed phrases, gas asset confusion, and the inability to spend received tokens locally.

TakumiPay delivers a friction-free consumer financial experience by combining:
1. **Mera Passkeys:** One-tap biometric sign-up (Face ID / Fingerprint) deriving a secp256k1 EOA via WebAuthn PRF. No seed phrases or recovery phrases ever shown to the user.
2. **Monad Speed & Scale:** ~600ms block finality and sub-cent gas fees make remittances instant and affordable.
3. **Agora AUSD Stablecoin:** Dollars held safely in cash-and-treasury-backed AUSD (`0x00000000eFE302BEAA2b3e6e1b18d08D69a9012a`).
4. **Immediate Spendability (QRIS / UMKM):** Recipients do not need to off-ramp to fiat. They can spend their balance directly at 44M+ merchants across Indonesia via national QR rails.
5. **Takumi Agent (Kimi K2.6):** Users can simply speak or text to send money: *"Send $50 to my mom in Jakarta"*.

---

## Repositories & Architecture

All code repositories are open source under the **GNU General Public License v3.0 (GPLv3)** and carry full commit histories:

| Repository | Description | Tech Stack |
|---|---|---|
| [`monad-submission-mobile-app`](https://github.com/Planckify-Labs/monad-submission-mobile-app) | Consumer mobile wallet: biometric passkey onboarding, dedicated Monad rails, non-blocking settlement timeline, Takumi Agent UI | React Native, Expo 54, viem, NativeWind |
| [`monad-submission-contract`](https://github.com/Planckify-Labs/monad-submission-contract) | TakumiPay 2.1.0 UUPS proxy settlement contract, `MockAUSD.sol`, Foundry scripts, and test suites | Solidity, Foundry (EVM) |
| [`monad-submission-api`](https://github.com/Planckify-Labs/monad-submission-api) | Backend API: Monad network & token catalog seeds, EIP-712 merchant quote signing service, intent settlement state machine | NestJS, Prisma, PostgreSQL, Redis |
| [`monad-submission-agent-api`](https://github.com/Planckify-Labs/monad-submission-agent-api) | Multi-agent orchestrator: Kimi K2.6 intelligence, intent classification, and capability tool execution envelopes | TypeScript, Vercel AI SDK, Moonshot Kimi |

---

## Monad On-Chain Deployments

TakumiPay smart contracts are deployed live on **Monad Mainnet** (real AUSD remittance rail) and **Monad Testnet** (merchant-spend verification rail):

### 1. Monad Mainnet (`chainId: 143`) — Production Remittance Rail

| Component | Detail | Address / Hash | Explorer |
|---|---|---|---|
| **TakumiPay Proxy (UUPS)** | Main Treasury & Settlement Contract (v2.1.0) | `0x479B0843C3e0627f36551660506dEd5b349Fa968` | [MonadVision Proxy](https://monadvision.com/address/0x479B0843C3e0627f36551660506dEd5b349Fa968) |
| **Implementation** | `TakumiPay.sol` logic contract | `0x1aC593085Fa34c651E805085da4b2cabAC676F99` | Implementation Logic |
| **Proxy Deploy Tx** | Contract creation | `0x0c50d974055f91c9b093d45026d4ab214f7b0f67e30627976f8bc66f6128f8c7` | Verified broadcast |
| **Implementation Deploy Tx**| Implementation deploy | `0x051d16f8b67b71945231f82550060a565496883a02f95404e5c4152b01f83525` | Verified broadcast |
| **Allowed Token (Agora AUSD)** | Real Agora AUSD (ERC-20, 6 decimals) | `0x00000000eFE302BEAA2b3e6e1b18d08D69a9012a` | [MonadVision AUSD](https://monadvision.com/address/0x00000000eFE302BEAA2b3e6e1b18d08D69a9012a) |
| **Enable AUSD Tx** | `addAllowedPaymentToken` | `0x8d12ec7d42afd22e9f436a0832fb1814ea047f7e7cf9dbcdd7b6feafbc37d0a2` | Configuration step |
| **Backend Signer** | Authorized merchant quote signer | `0x299E4E56e9F05A21414A62479DA1514C20aA61e8` | EIP-712 recovery target |

### 2. Monad Testnet (`chainId: 10143`) — Merchant Spend Verification Rail

| Component | Detail | Address / Hash | Explorer |
|---|---|---|---|
| **TakumiPay Proxy (UUPS)** | Main Treasury & Settlement Contract (v2.1.0) | `0x9EEC5aD4FC092fD468A8114007e541238F4Ba5ee` | [Testnet Explorer](https://testnet.monadvision.com/address/0x9EEC5aD4FC092fD468A8114007e541238F4Ba5ee) |
| **Implementation** | `TakumiPay.sol` logic contract | `0xbB074ED383dA5C99756D72b62f7Fdff97A8c9022` | Implementation Logic |
| **Proxy Deploy Tx** | Contract creation | `0x6eed45f5b5bac2652706f8f7bd765887dd278d8df0a54edd1476f8578b4386d6` | Verified broadcast |
| **Implementation Deploy Tx**| Implementation deploy | `0x76b3f2c44af2fd9ba31cb9d81eb2f79eb316d2effbc5e2d04649c718c3234e0e` | Verified broadcast |
| **Open-Mint MockAUSD** | 6-decimal testnet stand-in (`src/MockAUSD.sol`) | `0x1aC593085Fa34c651E805085da4b2cabAC676F99` | [Testnet MockAUSD](https://testnet.monadvision.com/address/0x1aC593085Fa34c651E805085da4b2cabAC676F99) |
| **MockAUSD Deploy Tx** | Mock contract deployment | `0xdca51260a5709ccbadbd39f86dbd2e7ef6046647d9ff2e3a64882dacf1f4aa01` | Token deploy |

---

## Originality & Hackathon Build Window Disclosure

*(Mandatory disclosure under Section 4.1 Clause 4 of Metropolis Hackathon Rules)*

1. **Pre-Existing Foundation (Prior to September 1, 2026):**
   Foundational mobile UI design system, cryptographic signing utilities, and payment gateway primitives originated prior to the hackathon.
2. **Substantial Work Built During Hackathon Window (September 16 – September 28, 2026):**
   *The entire consumer remittance, passkey, and settlement product was engineered specifically for the Monad ecosystem:*
   - **Dedicated Monad Consumer Architecture:** Engineered a streamlined user journey centered exclusively on Monad Mainnet (`143`) and Testnet (`10143`), eliminating network switching, chain dropdowns, and onboarding friction for everyday users.
   - **Mera Passkey Account Layer:** WebAuthn PRF key derivation enabling seedless, biometric Face ID/Fingerprint onboarding tailored for non-crypto consumers.
   - **Monad Network & Agora AUSD Integration:** Configured Monad execution parameters, sub-cent fee handling, and Agora AUSD contract integration.
   - **TakumiPay 2.1.0 Monad Deployments:** Deployed and verified UUPS contracts on Monad Mainnet (`0x479B0843C3e0627f36551660506dEd5b349Fa968`) and Monad Testnet (`0x9EEC5aD4FC092fD468A8114007e541238F4Ba5ee`).
   - **Non-Blocking Settlement UX:** Built a streaming visual settlement hero (`Preparing` → `Confirming` → `Paid`) engineered to take advantage of Monad's ~600ms block finality.
   - **Takumi Agent (Kimi K2.6):** Conversational remittance orchestrator allowing users to send AUSD over Monad in natural language.
3. **AI Tools Disclosure:**
   Assisted by Claude (Sonnet/Opus) and Gemini for design synthesis, test generation, and documentation.

---

## Quick Start

```bash
# 1. Mobile App
git clone https://github.com/Planckify-Labs/monad-submission-mobile-app.git
cd monad-submission-mobile-app && pnpm install && pnpm start

# 2. Smart Contracts
git clone https://github.com/Planckify-Labs/monad-submission-contract.git
cd monad-submission-contract/evm && forge test

# 3. Backend API
git clone https://github.com/Planckify-Labs/monad-submission-api.git
cd monad-submission-api && pnpm install && pnpm start:dev

# 4. Agent Orchestrator
git clone https://github.com/Planckify-Labs/monad-submission-agent-api.git
cd monad-submission-agent-api && pnpm install && pnpm dev
```

---

<sub>Built with pride by Planckify Labs for the Monad Metropolis Hackathon, September 2026.</sub>
