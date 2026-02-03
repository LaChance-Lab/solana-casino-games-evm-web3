# Casino Games Suite (Solana + EVM) — Web3 Casino Game Smart Contracts

This page is a **game-by-game** overview for developers building a **casino game**, **Web3 casino game**, **Solana casino game**, or broader **blockchain casino game** platform.

The implementation is split by chain:

- **Solana programs (Anchor/Rust)**: `web3/solana/programs/*`
- **EVM contracts (Solidity)**: `web3/evm/src/*`

---

## Included games (10)

### Crash (provably fair)

- **Solana**: `web3/solana/programs/crash`
- **EVM**: `web3/evm/src/Crash.sol`
- **What it is**: Players place a bet and can cash out at a multiplier before “crash”.

### Plinko

- **Solana**: `web3/solana/programs/plinko`
- **EVM**: `web3/evm/src/Plinko.sol`
- **What it is**: Randomized path → landing bucket → payout multiplier.

### Dice

- **Solana**: `web3/solana/programs/dice`
- **EVM**: `web3/evm/src/Dice.sol`
- **What it is**: Roll under/over target with probability-based payout.

### Blackjack

- **Solana**: `web3/solana/programs/blackjack`
- **EVM**: `web3/evm/src/Blackjack.sol`
- **What it is**: Beat the dealer to 21 (rules enforced on-chain).

### Roulette

- **Solana**: `web3/solana/programs/roulette`
- **EVM**: `web3/evm/src/Roulette.sol`
- **What it is**: Wheel spin outcome with standard bet types.

### Poker

- **Solana**: `web3/solana/programs/poker`
- **EVM**: `web3/evm/src/Poker.sol`
- **What it is**: Texas Hold’em style logic and settlement (implementation details per chain).

### Slots

- **Solana**: `web3/solana/programs/slots`
- **EVM**: `web3/evm/src/Slots.sol`
- **What it is**: Reel outcomes mapped to payout table.

### CoinFlip

- **Solana**: `web3/solana/programs/coinflip`
- **EVM**: `web3/evm/src/CoinFlip.sol`
- **What it is**: Simple 50/50 game with configurable edge.

### Lottery

- **Solana**: `web3/solana/programs/lottery`
- **EVM**: `web3/evm/src/Lottery.sol`
- **What it is**: Pooled tickets → winner selection → payout.

### Jackpot

- **Solana**: `web3/solana/programs/jackpot`
- **EVM**: `web3/evm/src/Jackpot.sol`
- **What it is**: Progressive jackpot funded by a rake / portion of bets.

---

## “Provably fair” in practice

For a casino game to be “provably fair”:

- **Rules are on-chain** (no hidden server logic).
- **Randomness is verifiable** (VRF or equivalent).
- **Settlement is auditable** via transactions/logs.

This repo is designed so you can build a **decentralized casino game** UI that points users to on-chain transactions as the ultimate source of truth.

---

## Next steps

- **Getting started**: [`GETTING_STARTED.md`](./GETTING_STARTED.md)
- **API reference**: [`API.md`](./API.md)
- **Deployment**: [`DEPLOYMENT.md`](./DEPLOYMENT.md)
- **FAQ**: [`FAQ.md`](./FAQ.md)
