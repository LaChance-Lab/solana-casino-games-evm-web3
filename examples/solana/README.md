# Solana Examples (Anchor)

These examples show the typical flow to call a **Solana casino game** program from a client:

- Load IDL
- Construct accounts
- Send transactions for `initialize`, `place_bet`, and settlement instructions

## Suggested next steps

1. Build IDLs:

```bash
cd web3/solana
anchor build
```

2. Use the generated IDL(s) from `web3/solana/target/idl/`.

3. Start from the instruction shapes described in [`docs/API.md`](../../docs/API.md) and the game overview in [`docs/GAMES.md`](../../docs/GAMES.md).
