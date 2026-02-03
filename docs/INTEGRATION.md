# Integration Guide (Build a Web3 Casino Game)

This guide explains how to integrate the smart contracts in this repo into a **casino game** frontend or backend.

---

## Recommended architecture

- **Frontend**: wallet-based UI (Phantom for Solana, MetaMask for EVM)
- **Indexing** (optional): store game history via on-chain event/log indexing
- **Monitoring**: alerts for large bets/payouts, failure rates, oracle outages

This repository focuses on on-chain logic; your product UI and operational services can live in a separate repo.

---

## Solana integration (Anchor)

Typical steps:

1. `anchor build` to generate IDLs
2. Use `@coral-xyz/anchor` in your client
3. For each game:
   - initialize config (once)
   - place bet
   - settle / cashout

---

## EVM integration (ethers / viem)

Typical steps:

1. Deploy contracts (Foundry scripts)
2. Set treasury + limits via `initialize(...)`
3. Call game-specific functions
4. Listen for events like `GamePlayed(...)`

---

## UX / SEO tips (for your website)

If you publish a marketing site for your casino games, create one landing page per query intent:

- “casino game smart contracts”
- “web3 casino game”
- “solana casino game”
- “blockchain casino game”

Then link those pages to your GitHub repo and the `docs/GAMES.md` page for deep technical proof.

---

## Related docs

- API: [`API.md`](./API.md)
- Games: [`GAMES.md`](./GAMES.md)
- VRF: [`VRF.md`](./VRF.md)
