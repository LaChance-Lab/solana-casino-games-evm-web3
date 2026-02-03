# Telegram Bot (Scaffold / WIP)

This directory is a starting point for adding Telegram-based UX to a **Web3 casino game** (commands, balance checks, game triggers, notifications).

It is intentionally minimal in this repository, since production bot design depends on your custody model, chain support, and compliance requirements.

## Recommended approach

- Build your casino game UX around on-chain events:
  - **Solana**: subscribe to program logs / account changes
  - **EVM**: subscribe to `GamePlayed(...)` and other game events
- Keep private keys off the bot server when possible.

## Next steps

- Add a real implementation under `telegram-bot/src/`
- Document configuration (BOT_TOKEN, RPCs, contract addresses, program IDs)
