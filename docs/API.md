# API Reference (Smart Contracts)

This repository is a **casino game smart contract** suite (Solana + EVM). Instead of a single REST API, you interact with:

- **Solana programs (Anchor / Rust)** via **IDL + instructions**
- **EVM contracts (Solidity)** via **ABI + public functions**

If you’re building a **Web3 casino game** frontend, these are the canonical entrypoints.

---

## Solana (Anchor) program APIs

- **Programs live in**: `web3/solana/programs/*/src/lib.rs`
- **Build outputs IDLs into**: `web3/solana/target/idl/` (after `anchor build`)

### Common instruction patterns

Most games follow a similar shape:

- **`initialize(...)`**: creates / configures a game `Config` account (authority, treasury, min/max bet, house edge)
- **`place_bet(...)`**: validates bet, transfers tokens to treasury, creates a per-player `GameState`
- **`settle_*` / `cashout`**: finalizes outcome and pays winnings (if any)
- **`pause` / `unpause`**: circuit breaker controlled by authority

Example (Crash program instructions):

- `initialize(min_bet, max_bet, house_edge_bps)`
- `place_bet(bet_amount, auto_cashout)`
- `cashout(current_multiplier)`
- `settle_crashed()`
- `pause()`, `unpause()`

Source: `web3/solana/programs/crash/src/lib.rs`

---

## EVM (Solidity) contract APIs

- **Contracts live in**: `web3/evm/src/*.sol`
- **Shared interface**: `web3/evm/src/interfaces/ICasinoGame.sol`

### `ICasinoGame` (common surface)

All games implement (or are expected to align with) a small management interface:

- **`initialize(treasury, minBet, maxBet, houseEdgeBps)`**
- **`pause()` / `unpause()`**
- **Event**: `GamePlayed(player, gameId, betAmount, result, payout)`

This interface is a good “minimal ABI” to start with when integrating multiple **blockchain casino games** behind one UI.

---

## Integration quickstart

### Solana client (Anchor)

1. `cd web3/solana && anchor build`
2. Load the program’s IDL (`target/idl/<program>.json`)
3. Use `@coral-xyz/anchor` to invoke instructions and read accounts

### EVM client (ethers / viem)

1. Compile + deploy from `web3/evm`
2. Import the generated ABI (or use `ICasinoGame` for management calls)
3. Call game-specific methods (see each contract in `web3/evm/src/`)

---

## Where to go next

- **Game-by-game overview**: [`GAMES.md`](./GAMES.md)
- **Deployment guide**: [`DEPLOYMENT.md`](./DEPLOYMENT.md)
- **FAQ**: [`FAQ.md`](./FAQ.md)
