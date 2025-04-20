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

## User Flow

### Joining the Pool

1. User calls `join()` with RETH and/or WETH.
2. Contract transfers and approves tokens to the Vault.
3. Liquidity is added and BPT is minted.
4. Any unused tokens are refunded.

### Exiting the Pool

1. User calls `exit()` with the amount of BPT to redeem.
2. Contract transfers BPT to the Vault.
3. RETH is redeemed and sent to the user.

---

