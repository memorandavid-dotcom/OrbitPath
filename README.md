# OrbitPath — Full-Stack Consumer Wallet Gateway

OrbitPath acts as an intelligent routing layer and secure cross-border remittance gateway built on the **Stellar Network** and **Soroban Smart Contracts**. It is designed to look, feel, and operate like a modern consumer fintech wallet (similar to GCash, Maya, or GoTyme).

By programmatically scanning multi-asset liquidity paths and automating swap settlements, OrbitPath eliminates standard correspondent banking intermediary markups and provides migrant workers with guaranteed real-time payout delivery to mobile money and local bank targets (SEP-31).

---

## 🚀 Key Functional Architecture

```
[Onboarding Sign Up] ──► [Generates On-Chain Cryptographic Keypair]
        │
        ▼
[Secure Sign In (MPIN)] ──► [Initiates Active Session Token]
        │
        ▼
[User Applet] (Single-View Responsive Layout / Mobile Bottom Nav)
        │
        ▼ (Initiates Send with Session-Isolated Profile)
[Express Proxy /api/execute-transfer] (Reads User Session)
        │
        ▼ (Observer Relayer Script Logs Books)
[Horizon testnet.strictReceivePaths] ────► [DEX & AMM Liquidity Pools]
        │
        ▼ (Soroban Smart Contract)
[Soroban Trustless Slippage Check]
        │
        ▼ (Stellar Multi-Asset Atomic Swap)
[PathPaymentStrictReceive Operation]
        │
        ▼ (Settlement Outflow)
[SEP-31 Local Fiat Anchor Payout] ────► [Recipient Bank / GCash Payout]
```

---

## 🛠️ Onboarding, Security, & Architecture Features

### 1. Dedicated Authentication Flow (Sign Up / Sign In / Log Out)
* **Welcome Screen:** Beautiful onboarding portal supporting toggling between Login and Registration.
* **On-Chain Keypair Initialization:** Registration instantly spawns a randomized Stellar keypair (public & private key) on the server, establishing a secure on-chain wallet behind the scenes.
* **6-Digit MPIN Security:** Returning users can access their balance securely via a 6-digit passcode.
* **Terms of Service Compliance:** Before finalizing account creation, users must review and explicitly agree to the digital wallet agreement (`TERMS_OF_SERVICE.md`).

### 2. Strict Account Isolation & Data Privacy
* **Privacy Rule:** Under no circumstances should internal database User IDs, raw Stellar Public Keys, or Soroban Contract IDs be exposed anywhere in the user-facing interface.
* **Secured Backend:** All keys remain strictly contained within the backend server database. The client-side is given only session tokens and represented using masked placeholder indicators (e.g., `OrbitPath User ****ICE2` or `Account Connected`).

### 3. Multi-Device Layout Optimization
* **Mobile Viewports (Phones):** Features a single-column thumb-reachable design, anchored by a persistent bottom navigation bar (Home, Scan QR, History, Profile) with `min-h-[44px]` touch targets.
* **Tablet & Desktop Viewports:** Seamlesly expands the screen into a balanced, dual-pane layout:
  - **Left Pane:** Branding, Profile, Balance Card, Quick Actions.
  - **Right Pane:** Remittance Form, Camera QR Scanner Simulator, Live Transaction feeds.

### 4. Dynamic QR Code Module & Transaction Specifics
* **Receiving Portal:** Renders a visual dynamic canvas (SVG) pixel-block matrix. Corner finder markers are painted dynamically, and interior patterns shift based on input amount, asset, and memo parameters.
* **Viewfinder Scanner:** An interactive scanner simulator that automatically parses standard Stellar pay URIs (`stellar:pay?amount=...`) to pre-fill the remittance confirmation sheet instantly.

---

## 💻 Tech Stack & Setup

* **Frontend**: React (v19) + Vite + Tailwind CSS (v4) + Motion
* **Backend**: Node.js + Express (Session Manager & Proxy to Horizon Testnet API)
* **SDKs**: `@google/genai` (Server-side model generation), `stellar-sdk` (DEX and Horizon connectivity)
* **Licensing**: Open Source Remittance Architecture

---

## 🤝 Getting Started

1. Set your `STELLAR_PRIVATE_KEY` inside `.env` to sign actual transactions on testnet.
2. Run development servers with:
   ```bash
   npm run dev
   ```
3. Open the app on `http://localhost:3000` to register, log in, and simulate dynamic QR payments!
