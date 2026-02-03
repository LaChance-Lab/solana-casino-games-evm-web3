# EVM Examples (Foundry / ethers)

These examples describe the typical flow to integrate an **EVM casino game** contract into a client:

- Deploy contracts
- Call `initialize(...)` (common across games)
- Execute game-specific methods
- Listen for `GamePlayed(...)` events

## Build + test (local)

```bash
cd web3/evm
npm install
forge build
forge test -vvv
```

## Common interface

For management actions (initialize/pause/unpause), see:

- `web3/evm/src/interfaces/ICasinoGame.sol`

For game-specific interactions, refer to each contract in:

- `web3/evm/src/`
