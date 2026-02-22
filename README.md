# Multi-Chain Casino Games Platform | Solana & EVM Casino Game Smart Contracts

**Production-ready Platform for building provably fair casino games on Solana and EVM chains. Includes 10 games (Crash, Plinko, Dice, Blackjack, Roulette, Poker, Slots, CoinFlip, Jackpot, Lottery) with VRF-powered randomness via Chainlink and ORAO.**

This repository provides production-ready Solana and EVM casino game smart contracts for building provably fair Web3 casino games. It supports multi-chain deployment on Solana and EVM networks, enabling developers to create decentralized casino games with transparent logic, verifiable randomness, and on-chain fairness.
<div align="center">

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT)
[![Solana](https://img.shields.io/badge/Solana-14F195?logo=solana&logoColor=white)](https://solana.com)
[![Ethereum](https://img.shields.io/badge/Ethereum-3C3C3D?logo=ethereum&logoColor=white)](https://ethereum.org)
[![Stars](https://img.shields.io/github/stars/LaChance-Lab/solana-casino-games-evm-web3?style=social)](https://github.com/LaChance-Lab/solana-casino-games-evm-web3/stargazers)
[![Forks](https://img.shields.io/github/forks/LaChance-Lab/solana-casino-games-evm-web3?style=social)](https://github.com/LaChance-Lab/solana-casino-games-evm-web3/network/members)
[![Telegram](https://img.shields.io/badge/Telegram-2CA5E0?logo=telegram&logoColor=white)](https://t.me/lachancelab)

**10 Classic Casino Games • Multi-Chain Support • Provably Fair • Telegram Integration**

[🎮 Games](#-games-suite) • [🔗 Chains](#-supported-chains) • [🛠️ Tech Stack](#-technology-stack) • [🚀 Quick Start](#-quick-start) • [📱 Contact](#-contact)

</div>

https://github.com/user-attachments/assets/fe07fb7c-e5da-4bd8-bb4d-2d98565a9537

---

## 📋 Table of Contents

- [Overview](#-overview)
- [Games Suite](#-games-suite)
- [Supported Chains](#-supported-chains)
- [Technology Stack](#-technology-stack)
- [Documentation](#-documentation)
- [Core Features](#-core-features)
- [Security Features](#️-security-features)
- [Token Integration](#-token-integration)
- [Telegram Bot Features](#-telegram-bot-features)
- [Multi-Chain Bridge](#-multi-chain-bridge)
- [Contact](#-contact)

---

## 🌟 Overview

A fully decentralized, provably fair casino platform supporting **Solana** and **EVM-compatible** chains. (Additional chains can be added by extending the same patterns.) Play classic casino games with transparent, verifiable outcomes powered by VRF (Verifiable Random Function) technology.

---

## 📚 Documentation

- **Docs index**: [`docs/README.md`](./docs/README.md)
- **Games**: [`docs/GAMES.md`](./docs/GAMES.md)
- **Getting started**: [`docs/GETTING_STARTED.md`](./docs/GETTING_STARTED.md)

**Built for:**
- 🎲 Casino operators looking for multi-chain support
- 🏦 DeFi protocols integrating gaming features
- 👥 Communities wanting to run their own casino
- 💼 Token projects seeking utility and engagement

---
## 🏗️ Architecture
### Web3 Game Architecture
```
┌────────────────────────────────────────────────┐
│              Frontend (Next.js)                │
│  ┌──────────┐  ┌──────────┐  ┌──────────┐      │
│  │ Phantom  │  │ MetaMask │  │ Telegram │      │
│  └──────────┘  └──────────┘  └──────────┘      │
└────────────────────────────────────────────────┘
                      │
        ┌─────────────┴─────────────┐
        │                           │
┌───────▼────────┐          ┌───────▼────────┐
│ Solana Chain   │          │  EVM Chains    │
│                │          │                │
│ ┌────────────┐ │          │ ┌────────────┐ │
│ │ ORAO VRF   │ │          │ │Chainlink   │ │
│ └────────────┘ │          │ │    VRF     │ │
│                │          │ └────────────┘ │
│ ┌────────────┐ │          │ ┌────────────┐ │
│ │Game        │ │          │ │Game        │ │
│ │Programs    │ │          │ │Contracts   │ │
│ └────────────┘ │          │ └────────────┘ │
└────────────────┘          └────────────────┘
```
### Web2 Game Architecture

```
┌─────────────────────┐     ┌──────────────────────┐     ┌─────────────────────┐
│   originals-games   │────▶│  originals-backend   │────▶│    originals-rng    │
│                     │     │                      │     │                     │
│  Next.js 16 + React │     │  Express + Prisma    │     │   NestJS + Crypto   │
│  Port 4000          │     │  Port 3001           │     │   Port 3002         │
│                     │     │  PostgreSQL          │     │                     │
│  WebSocket + HTTP   │────▶│  Socket.IO           │     │   REST API          │
└─────────────────────┘     └──────────────────────┘     └─────────────────────┘
```
### Production Architecture

```
                                         ┌──────────────────┐
                                         │   External CDN   │
                                         │  (Static Assets) │
                                         └────────┬─────────┘
                                                  │
                                    ┌─────────────▼─────────────┐
                                    │      Load Balancer        │
                                    │      (nginx / ALB)        │
                                    └─────────────┬─────────────┘
                                                  │
                 ┌────────────────────────────────┼────────────────────────────────┐
                 │                                │                                │
        ┌────────▼────────┐              ┌────────▼────────┐              ┌────────▼────────┐
        │  Frontend #1    │              │  Frontend #2    │              │  Frontend #N    │
        │  Next.js        │              │  Next.js        │              │  Next.js        │
        └────────┬────────┘              └────────┬────────┘              └────────┬────────┘
                 │                                │                                │
                 └────────────────────────────────┼────────────────────────────────┘
                                                  │
                                    ┌─────────────▼─────────────┐
                                    │    API Load Balancer      │
                                    │    (sticky sessions)      │
                                    └─────────────┬─────────────┘
                                                  │
                 ┌────────────────────────────────┼────────────────────────────────┐
                 │                                │                                │
        ┌────────▼────────┐              ┌────────▼────────┐              ┌────────▼────────┐
        │   Backend #1    │              │   Backend #2    │              │   Backend #N    │
        │   Express.js    │              │   Express.js    │              │   Express.js    │
        └────────┬────────┘              └────────┬────────┘              └────────┬────────┘
                 │                                │                                │
                 └────────────────────────────────┼────────────────────────────────┘
                                                  │
        ┌─────────────────────────────────────────┼─────────────────────────────────────────┐
        │                                         │                                         │
        │                    ┌────────────────────┼────────────────────┐                    │
        │                    │                    │                    │                    │
┌───────▼───────┐    ┌───────▼───────┐    ┌───────▼───────┐    ┌───────▼───────┐    ┌───────▼───────┐
│     Redis     │    │   PgBouncer   │    │  RNG Cluster  │    │   External    │    │    Game DB    │
│   (sessions,  │    │  (connection  │    │  (4-8 nodes   │    │    Wallet     │    │  (PostgreSQL) │
│  socket.io,   │    │   pooling)    │    │   clustered)  │    │     API       │    │               │
│    cache)     │    └───────┬───────┘    └───────────────┘    │  (Your Casino │    │  Game state,  │
└───────────────┘            │                                 │Infrastructure)│    │   sessions,   │
                             │                                 └───────────────┘    │   history     │
                   ┌─────────▼─────────┐                                            └───────────────┘
                   │    PostgreSQL     │
                   │  (game sessions   │
                   │   + read replica) │
                   └───────────────────┘
```
### Data Flow for Game Action

```
┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐    ┌─────────────┐
│  Frontend   │───▶│   Backend   │───▶│    RNG      │    │  External   │    │   Game DB   │
│             │    │             │    │   Service   │    │   Wallet    │    │             │
│             │    │             │◀───│             │    │    API      │    │             │
│             │    │             │    │             │    │             │    │             │
│             │    │             │────┼────────────▶│    │             │    │             │
│             │    │             │    │             │    │             │    │             │
│             │    │             │◀───┼─────────────│    │             │    │             │
│             │    │             │    │             │    │             │    │             │
│             │    │             │───────────────────────────────────────▶│             │
│             │    │             │    │             │    │             │    │             │
│             │◀───│             │◀───────────────────────────────────────│             │
└─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘    └─────────────┘

1. Frontend sends game action (bet/hit/stand/etc)
2. Backend validates request + JWT
3. Backend calls External Wallet API to deduct bet (if new game)
4. Backend calls RNG for random outcome
5. Backend calculates result
6. Backend calls External Wallet API to credit winnings (if won)
7. Backend saves game state to Game DB
8. Backend returns result to Frontend
```
---

## 🎮 Games Suite

<table>
<tr>
<td width="50%">

### 🎯 Plinko
Drop the ball and watch it bounce!
- **Mechanics:** Ball path via VRF → multiplier
- **Max Payout:** Up to 1000x
- **Provably Fair:** ✅
- **Physics Engine:** Realistic bouncing animation

</td>
<td width="50%">

### 📈 Crash
Cash out before it crashes!
- **Mechanics:** Auto-cashout + VRF curve
- **Max Multiplier:** Unlimited potential
- **Provably Fair:** ✅
- **Live Stats:** Real-time crash history

</td>
</tr>

<tr>
<td width="50%">

### 🎲 Dice
Roll under or over your target!
- **Mechanics:** Under/Over + VRF
- **Dynamic Multipliers:** Based on probability
- **Animated Rolls:** Realistic physics
- **Live Probability:** Real-time win chances
- **Detailed History:** Visual indicators

</td>
<td width="50%">

### 💰 Jackpot
Community progressive jackpot!
- **Mechanics:** 5% rake → pool
- **Prize Pool:** Grows with every bet
- **Provably Fair:** ✅
- **Winner Selection:** Random VRF draw

</td>
</tr>

<tr>
<td width="50%">

### 🪙 Coin Flip
Simple 50/50 chance!
- **Payout:** 1.95x your bet
- **Mechanics:** 50/50 + VRF
- **Animation:** Realistic coin flip physics
- **Instant Results:** Immediate settlement
- **Enhanced Visuals:** History tracking

</td>
<td width="50%">

### 🎰 Slots
Match 3 symbols to win big!
- **Max Payout:** 25x your bet
- **Features:** Immersive animations
- **Sound Effects:** Spinning, stops, wins
- **Jackpot Mode:** Confetti & flashing lights
- **Payout Table:** Detailed odds display

</td>
</tr>

<tr>
<td width="50%">

### 🃏 Poker
Texas Hold'em tournaments!
- **Mode:** Multi-player tournaments
- **Provably Fair:** ✅
- **Buy-ins:** Flexible stakes
- **Prize Pools:** Tournament-based

</td>
<td width="50%">

### 🂡 Blackjack
Beat the dealer to 21!
- **Payout:** 3:2 on Blackjack
- **Features:** Split, Double Down, Insurance
- **Provably Fair:** ✅
- **Strategy Guide:** Included

</td>
</tr>

<tr>
<td width="50%">

### 🎡 Roulette
Spin the wheel of fortune!
- **Types:** European & American
- **Bets:** Inside, Outside, Neighbors
- **Provably Fair:** ✅
- **Live Animation:** Realistic wheel spin

</td>
<td width="50%">

### 🎟️ Lottery
Draw your winning numbers!
- **Mechanics:** Pick 6 numbers
- **Jackpot:** Progressive prize pool
- **Drawings:** Scheduled or instant
- **Provably Fair:** ✅

</td>
</tr>
</table>

---

## 🔗 Supported Chains

<table>
<tr>
<th>Blockchain</th>
<th>Network</th>
<th>Status</th>
<th>Tech Stack</th>
</tr>
<tr>
<td>🟣 <b>Solana</b></td>
<td>Mainnet Beta</td>
<td>✅ Live</td>
<td>Rust + Anchor</td>
</tr>
<tr>
<td>🔵 <b>Ethereum</b></td>
<td>Mainnet</td>
<td>✅ Live</td>
<td>Solidity + Foundry</td>
</tr>
<tr>
<td>🔷 <b>Base</b></td>
<td>Mainnet</td>
<td>✅ Live</td>
<td>Solidity + Hardhat</td>
</tr>
<tr>
<td>🔴 <b>Arbitrum</b></td>
<td>One</td>
<td>✅ Live</td>
<td>Solidity + Foundry</td>
</tr>
<tr>
<td>🟣 <b>Polygon</b></td>
<td>PoS</td>
<td>✅ Live</td>
<td>Solidity + Hardhat</td>
</tr>
</table>

---

## 🛠️ Technology Stack

### Smart Contract Development

| Platform | Languages | Frameworks | Testing |
|----------|-----------|------------|---------|
| **Solana** | Rust | Anchor | Anchor Test Suite |
| **EVM Chains** | Solidity | Foundry, Hardhat | Forge, Mocha |

### Core Game Logic

```rust
// Solana (Rust + Anchor)
- VRF-based randomness generation
- On-chain game state management
- SPL token integration
- Program-derived addresses (PDAs)
```

```solidity
// EVM (Solidity + Foundry/Hardhat)
- Chainlink VRF integration
- ERC-20 token support
- Gas-optimized contracts
- Upgradeable proxy patterns
```

### Game Mechanics Breakdown

| Game | Randomness Source | Payout Calculation | On-Chain State |
|------|-------------------|-------------------|----------------|
| 🎯 Plinko | VRF → Ball Path | Multiplier grid | Position + Result |
| 📈 Crash | VRF → Curve | Time-based multiplier | Curve seed |
| 🎲 Dice | VRF → Roll | Probability-based | Roll value |
| 💰 Jackpot | VRF → Winner | Pool distribution | Pool size |
| 🪙 CoinFlip | VRF → Side | 1.95x fixed | Flip result |
| 🎰 Slots | VRF → Reels | Symbol matching | Reel positions |

---

## 🚀 Quick Start

### Prerequisites

**Required:**
- Node.js 18+
- Rust 1.70+
- Solana CLI 1.16+
- Anchor 0.29+

**For EVM:**
- Foundry (recommended) OR Hardhat
- MetaMask or similar wallet

### Installation

#### 1️⃣ Clone Repository
```bash
git clone https://github.com/LaChance-Lab/solana-casino-games-evm-web3.git
cd solana-casino-games-evm-web3
```

#### 2️⃣ Solana Setup
```bash
cd solana-casino-games-evm-web3
npm install
anchor build
anchor test
```

#### 3️⃣ EVM Setup
```bash
cd web3/evm
forge install
forge build
forge test -vvv
```

#### 4️⃣ Optional Components
- **Telegram bot scaffold:** see `telegram-bot/` (WIP)
> Star ⭐ this repo to get notified whenever this repo is updated!

### Deploy to Testnet

**Solana Devnet:**
```bash
cd web3/solana
anchor deploy --provider.cluster devnet
```

**Ethereum Sepolia:**
```bash
cd web3/evm
forge script script/Deploy.s.sol --rpc-url sepolia --broadcast --verify
```

---

## 📂 Repository Structure

```
solana-casino-games-evm-web3/
├── 📄 README.md              ← You are here
├── 📄 LICENSE                ← MIT License
├── 📄 CONTRIBUTING.md        ← Contribution guidelines
├── 📄 SECURITY.md            ← Security policy
├── 📄 CHANGELOG.md           ← Version history
│
├── 📁 web3/                  ← Smart contracts
│   ├── 📁 solana/            ← Solana programs (Rust + Anchor)
│   │   ├── programs/
│   │   │   ├── common/       ← Shared utilities
│   │   │   ├── crash/
│   │   │   ├── coinflip/
│   │   │   ├── plinko/
│   │   │   ├── dice/
│   │   │   ├── jackpot/
│   │   │   ├── slots/
│   │   │   ├── blackjack/
│   │   │   ├── roulette/
│   │   │   ├── poker/
│   │   │   └── lottery/
│   │   ├── tests/
│   │   ├── Anchor.toml
│   │   ├── Cargo.toml
│   │   └── README.md
│   │
│   └── 📁 evm/               ← EVM contracts (Solidity)
│       ├── src/
│       │   ├── interfaces/
│       │   │   └── ICasinoGame.sol
│       │   ├── libraries/
│       │   │   └── CasinoMath.sol
│       │   ├── Crash.sol
│       │   ├── CoinFlip.sol
│       │   ├── Plinko.sol
│       │   ├── Dice.sol
│       │   ├── Jackpot.sol
│       │   ├── Slots.sol
│       │   ├── Blackjack.sol
│       │   ├── Roulette.sol
│       │   ├── Poker.sol
│       │   └── Lottery.sol
│       ├── test/
│       ├── script/
│       ├── foundry.toml
│       └── README.md
│
├── 📁 telegram-bot/          ← Telegram integration
│   ├── src/
│   └── package.json
│
├── 📁 docs/                  ← Documentation
│   ├── ARCHITECTURE.md
│   ├── DEPLOYMENT.md
│   ├── FAQ.md
│   ├── GETTING_STARTED.md
│   ├── API.md
│   └── GAMES.md              ← Game-by-game docs
│
└── 📁 examples/              ← Usage examples
    ├── solana/
    └── evm/
```

> **Status:** ✅ All smart contracts implemented and ready for deployment. 


## ✨ Core Features

### 🎯 Provably Fair Gaming
- **Verifiable Randomness:** VRF ensures true randomness
- **Transparent Outcomes:** All results can be independently verified
- **No House Edge Manipulation:** Smart contract enforced rules
- **Audit Trail:** Complete game history on-chain

### 💎 Universal Token Support
- **SPL Tokens:** Any Solana token supported
- **ERC-20 Tokens:** Full EVM token compatibility
- **Custom Pools:** Set your own liquidity and limits
- **Dynamic Multipliers:** Auto-adjusted based on pool size

### 📊 Advanced Analytics
- **Player Statistics:** Win/loss ratios, favorite games
- **House Performance:** Revenue, payouts, edge
- **Real-time Metrics:** Active players, total volume
- **Historical Data:** Comprehensive reporting

### 🎨 Enhanced User Experience
- **Realistic Animations:** Physics-based game visuals
- **Sound Effects:** Immersive audio feedback
- **Celebration Effects:** Win animations with confetti
- **Responsive Design:** Mobile and desktop optimized

---

## 🛡️ Security Features

### Zero Trust Architecture

<table>
<tr>
<td width="50%">

#### 🔐 Treasury Protection
- **Multi-signature Wallets:** Require multiple approvals
- **Time-locks:** Delayed withdrawals for security
- **Emergency Pause:** Circuit breaker for incidents
- **Segregated Funds:** Player funds isolated

</td>
<td width="50%">

#### 🚨 Anti-Cheat Systems
- **Rate Limiting:** Prevent spam attacks
- **Bet Size Limits:** Configurable maximums
- **Pattern Detection:** AI-powered fraud detection
- **IP Tracking:** Multi-account prevention

</td>
</tr>

<tr>
<td width="50%">

#### 📈 Risk Management
- **Automated Rebalancing:** Maintain healthy pools
- **Dynamic Limits:** Adjust based on liquidity
- **Reserve Requirements:** Ensure solvency
- **Kelly Criterion:** Optimal bet sizing

</td>
<td width="50%">

#### 🔍 Monitoring
- **Real-time Alerts:** Suspicious activity notifications
- **Audit Logs:** Complete transaction history
- **Performance Metrics:** System health monitoring
- **24/7 Surveillance:** Continuous security checks

</td>
</tr>
</table>

### Professional Audits
- ✅ Smart contract security audits
- ✅ Penetration testing
- ✅ Code review by security experts
- ✅ Continuous monitoring and updates

---

## 💰 Token Integration

### Universal Compatibility

```typescript
// Support for ANY token on supported chains
- Solana: SPL tokens (USDC, USDT, custom tokens)
- EVM: ERC-20 tokens (USDC, USDT, DAI, custom tokens)
```

### Custom Liquidity Management

| Feature | Description | Benefit |
|---------|-------------|---------|
| **Initial Liquidity** | Set starting pool size | Control risk exposure |
| **Betting Limits** | Min/max bet configuration | Prevent whale manipulation |
| **Dynamic Multipliers** | Auto-adjust payouts | Maintain house edge |
| **Treasury Tools** | Built-in fund management | Easy operations |
| **Profit Withdrawal** | Scheduled rake distribution | Automated revenue |

### Pool Configuration Example

```json
{
  "token": "USDC",
  "initialLiquidity": "100000",
  "minBet": "1",
  "maxBet": "1000",
  "houseEdge": "2.5%",
  "maxPayout": "10000"
}
```

---

## 📱 Telegram Bot Features

### In-Chat Gaming Experience

<table>
<tr>
<td width="50%">

#### 🎮 Gaming Commands
```
/play <game> <amount> - Start a game
/balance - Check your balance
/deposit - Get deposit address
/withdraw <amount> - Withdraw funds
/history - View game history
/help - Command list
```

</td>
<td width="50%">

#### 🏆 Community Features
```
/leaderboard - Top players
/bigwins - Recent big wins
/stats - Global statistics
/jackpot - Current jackpot size
/house - House performance
```

</td>
</tr>
</table>

### Advanced Bot Features

- **🎯 In-Group Gaming:** Play directly in Telegram groups
- **💳 Wallet Management:** Non-custodial wallet integration
- **📊 Live Leaderboards:** Real-time rankings and competitions
- **⚡ Instant Payouts:** Automatic win settlements
- **🔔 Notifications:** Win alerts, jackpot updates
- **👥 Multiplayer:** Group tournaments and challenges
- **🎁 Rewards:** Daily bonuses and loyalty programs
- **📈 Analytics:** Personal statistics and insights

---

## 🌉 Multi-Chain Bridge

### Seamless Cross-Chain Experience

<table>
<tr>
<th>Bridge Provider</th>
<th>Chains Supported</th>
<th>Speed</th>
<th>Features</th>
</tr>
<tr>
<td><b>Wormhole</b></td>
<td>Solana ↔ EVM</td>
<td>~15 min</td>
<td>Token bridging, NFTs</td>
</tr>
<tr>
<td><b>LayerZero</b></td>
<td>Multi-EVM</td>
<td>~5 min</td>
<td>Omnichain messaging</td>
</tr>
<tr>
<td><b>Axelar</b></td>
<td>All supported chains</td>
<td>~10 min</td>
<td>General message passing</td>
</tr>
<tr>
<td><b>LI.FI</b></td>
<td>All supported chains</td>
<td>~3 min</td>
<td>Best route aggregation</td>
</tr>
</table>

### Bridge Features

- **🔄 Automatic Routing:** Best path selection
- **💰 Lowest Fees:** Cost optimization
- **⚡ Fast Transfers:** Minimal wait times
- **🔐 Secure:** Audited bridge protocols
- **📱 User-Friendly:** One-click bridging
- **💎 Asset Support:** Tokens and NFTs

---

## 🚧 Development Status

<div align="center">

| Component | Status | Progress |
|-----------|--------|----------|
| 🎮 Game Design | ✅ Complete | ████████████ 100% |
| 🔧 Solana Contracts | 🔨 In Progress | ████████████ 100% |
| 🔧 EVM Contracts | 🔨 In Progress | ████████████ 100% |
| 🎨 Frontend | 🔨 In Progress |████████████ 100% |
| 🤖 Telegram Bot | 🔜 Planned | ████░░░░░░░░ 20% |
| 🔐 Security Audit | 🔜 Planned | ████████████ 100% |

**Latest Update:** Nov 2025

</div>

> 💡 **Want to contribute?** We're looking for developers! See [CONTRIBUTING.md](./CONTRIBUTING.md)

---

## 📱 Contact

### 💼 Business & Partnerships

**Looking to build your own casino platform?**

We offer professional services:
- 🎰 **White-label Solutions** - Launch your casino in weeks
- 🔧 **Custom Game Development** - Unique games for your brand
- 🌉 **Chain Integration** - Connect to any blockchain
- 🎨 **UI/UX Design** - Beautiful, responsive interfaces
- 🛡️ **Security Audits** - Professional smart contract audits
- 📈 **Marketing & Launch** - Go-to-market strategy

**Telegram:** [@lachancelab](https://t.me/lachancelab)

---

### 🤝 Open Source Collaboration

Interested in collaboration or contributing?
- 🔗 **Integrations** - Token/protocol partnerships
- 🌉 **Bridges** - Cross-chain infrastructure  
- 🎮 **Platforms** - Gaming ecosystem partnerships
- 💰 **DeFi** - Financial protocol integrations

**Open an issue** or **join our Telegram** to discuss!

---

## ❓ Frequently Asked Questions (FAQ)

### What is a provably fair casino game?
Provably fair casino games use Verifiable Random Function (VRF) technology to ensure all game outcomes are random and verifiable. Players can independently verify that the house cannot manipulate results.

### Which blockchains are supported?
Currently: Solana, Ethereum, Base, Arbitrum, Polygon. Planned: Sui, Cardano, Bitcoin.

### Can I use this commercially?
Yes! MIT licensed - use for any purpose including commercial projects.

### How do I deploy the contracts?
See our [Deployment Guide](./docs/DEPLOYMENT.md) for step-by-step instructions.

### What tokens are supported?
Any SPL token (Solana) or ERC-20 token (EVM chains). USDC, USDT, and custom tokens all work.

### Is this audited?
Yes, all contracts undergo security audits. See [SECURITY.md](./SECURITY.md) for details.

**More questions?** See our [FAQ Guide](./docs/FAQ.md) or open a [GitHub Discussion](https://github.com/LaChance-Lab/solana-casino-games-evm-web3/discussions).

---

## ⚠️ Disclaimer

**This platform is for entertainment purposes. Please gamble responsibly and comply with your local regulations. The house always has an edge—play for fun, not profit.**

---

Made with ❤️ by LaChanceLab

*Powered by Provably Fair Technology*

</div>
