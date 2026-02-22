# Deployment Guide (Solana + EVM)

This guide covers deploying the **Solana casino game programs** and **EVM casino game smart contracts** in this repo.

> Reminder: deploying gambling software has regulatory implications. Make sure you comply with local laws.

---

## Solana (Anchor) deployment

### Prerequisites

- Solana CLI
- Anchor
- Rust toolchain
- A funded deployer keypair (devnet or mainnet)

### Build

```bash
cd web3/solana
npm install
anchor build
```

### Test (local)

```bash
cd web3/solana
anchor test
```

### Deploy to devnet

```bash
cd web3/solana
solana config set --url devnet
anchor deploy --provider.cluster devnet
```

### Notes on program IDs

Each program declares an ID in its `lib.rs` (example: Crash). When you deploy, Anchor updates IDs/metadata under `target/`. Keep your deployed program IDs in sync with your client.

---

## EVM (Foundry) deployment

### Prerequisites

- Foundry installed
- An RPC URL (e.g., Sepolia/Base/Arbitrum/etc.)
- A funded deployer key (testnet ETH)

### Build + test

```bash
cd web3/evm
npm install
forge build
forge test -vvv
```

### Deploy (example: Sepolia)

```bash
cd web3/evm
forge script script/Deploy.s.sol --rpc-url sepolia --broadcast --verify
```

> If verification fails, confirm your Etherscan-style API key and the target chain settings.

---

## Post-deploy checklist (casino game ops)

- **Treasury funded**: payouts must be solvent.
- **Limits configured**: min/max bet and payout constraints.
- **Pause controls verified**: you should be able to halt games in emergencies.
- **Randomness provider configured**: VRF integration must be live on target chain.
- **Monitoring**: alert on large bets, large payouts, and abnormal failure rates.

---

## Related docs

- **Architecture**: [`ARCHITECTURE.md`](./ARCHITECTURE.md)
- **API / interaction surface**: [`API.md`](./API.md)
- **Games landing page** : [`GAMES.md`](./GAMES.md)
