## Core Functions

### `join(uint256 rethAmount, uint256 wethAmount)`

- Accepts RETH and/or WETH from the caller
- Approves the Balancer Vault
- Calls `_join()` with prepared data
- Returns any leftover tokens to the sender

### `exit(uint256 bptAmount, uint256 minRethAmountOut)`

- Accepts BPT from the caller
- Calls `_exit()` to redeem liquidity
- Sends **only RETH** back to the user

---

## Internal Mechanics

### `_join(address recipient, address[] memory assets, uint256[] memory maxAmountsIn)`

- Calls `IVault.joinPool()` using `EXACT_TOKENS_IN_FOR_BPT_OUT`
- Adds liquidity to the Balancer pool
- Mints BPT to the recipient

### `_exit(uint256 bptAmount, address recipient, address[] memory assets, uint256[] memory minAmountsOut)`

- Calls `IVault.exitPool()` using `EXACT_BPT_IN_FOR_ONE_TOKEN_OUT`
- Removes liquidity from the pool
- Redeems only RETH to the recipient

---

