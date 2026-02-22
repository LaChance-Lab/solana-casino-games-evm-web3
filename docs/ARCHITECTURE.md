# Architecture (Solana + EVM Casino Game Smart Contracts)

This repository provides **casino game smart contracts** for:

- **Solana**: Rust + Anchor programs (`web3/solana/programs/*`)
- **EVM**: Solidity contracts (`web3/evm/src/*`)

The goal is to make it straightforward to build a **Web3 casino game** (or a full **blockchain casino game** platform) with provably-verifiable rules and configurable treasury / risk parameters.

---

## High-level components

- **Game program/contract**: core rules + state transitions (bets, outcomes, settlements)
- **Treasury**: receives bets and pays winners
- **Randomness (VRF)**: determines outcomes fairly (provider differs by chain)
- **Config**: min/max bet, house edge, pause controls
- **Per-player game state**: stores bet, timestamps, outcome, payout

---

## Solana architecture (Anchor)

### Layout

- Programs: `web3/solana/programs/<game>/src/lib.rs`
- Shared utilities/errors/state: `web3/solana/programs/common/src/*`

### Typical flow

1. **Initialize** creates a `Config` account (authority, treasury, bet limits, house edge).
2. **Place bet** validates constraints and transfers SPL tokens into the treasury token account.
3. **Settle** computes payout, updates `GameState`, then transfers winnings from treasury to player using PDA signing.
4. **Pause/unpause** acts as a circuit breaker.

### Example: Crash program

The Crash program demonstrates a common pattern:

- `initialize(...)` sets config and treasury
- `place_bet(...)` transfers bet into treasury and creates a `GameState`
- `cashout(...)` settles based on multiplier and pays out
- `settle_crashed()` marks a loss

See: `web3/solana/programs/crash/src/lib.rs`

---

## EVM architecture (Solidity)

### Layout

- Game contracts: `web3/evm/src/*.sol`
- Shared interface: `web3/evm/src/interfaces/ICasinoGame.sol`
- Math helpers: `web3/evm/src/libraries/*`

### Typical flow

1. **Initialize** sets treasury + constraints.
2. **Play** (game-specific) requests randomness / derives outcome.
3. **Settle** emits `GamePlayed(...)` with `result` and `payout`.
4. **Pause/unpause** stops new games during incidents.

---

## “Provably fair” in this repo

At minimum, “provably fair” means:

- Rules are enforced by the smart contract (no hidden server-side logic).
- Randomness comes from a verifiable source (VRF or equivalent).
- Outcomes are reproducible/verifiable given on-chain proofs/logs.

To keep the docs accurate across chains, the per-game VRF wiring lives in code; this page focuses on the consistent architecture. See [`GAMES.md`](./GAMES.md).

---

## Security model (baseline)

- **Config authority**: can pause/unpause (and potentially update parameters depending on game implementation)
- **Treasury**: must be funded for payouts; operational best practice is multi-sig control
- **Limits**: min/max bet + max payout constraints should be enforced to prevent insolvency

Also see: [`SECURITY.md`](../SECURITY.md)
