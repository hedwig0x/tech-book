# Native Precompiled Contracts

Fluent allows extending contract behavior through precompiled modules.
For example, by implementing a multicall-style precompile,
contracts can support batched execution patterns via selector-based routing.
This extension mechanism avoids modifying original contract code.

> **Status note:** exact precompile set, selector routing strategy, and activation policy are release-dependent.
> Treat this chapter as architecture pattern guidance and confirm active precompiles in current runtime docs.

## Architecture

The implementation is based on function selector matching during bytecode execution.
When the BlendedRuntime executes bytecode,
it checks the first four bytes of the input data (function selector) against known precompiled contract selectors.
If there's a match, execution is redirected to the corresponding precompiled contract.

### Precompile Address

Each precompiled contract has a deterministic address generated from: `keccak256("precompile")[..16] + function_selector[..4]`

## Available Precompiles (example)

### Multicall (example pattern)

Multicall enables batching multiple calls into a single transaction for any contract in the system.
The implementation is compatible with OpenZeppelin's [Multicall](https://github.com/OpenZeppelin/openzeppelin-contracts/blob/master/contracts/utils/Multicall.sol).

The key feature is
that multicall works with any contract address—the system automatically detects the multicall selector
and routes the call through the precompiled contract while preserving the original contract's context.

#### Interface

```rust
#[function_id("multicall(bytes[])")] // 0xac9650d8 
pub fn multicall(&mut self, data: Vec<Bytes>) -> Vec<Bytes> {}
```

Parameters:

- `data`: Array of encoded function calls to be executed
- `results`: Array of return data from each call

#### How It Works

When a call with the Multicall selector (0xac9650d8) is made to any contract:

1. System detects the selector in the first four bytes of input data
2. Redirects execution to the Multicall precompile
3. Uses delegate_call for each batched call to preserve the original contract's context
4. Reverts the entire transaction if any call fails
5. Returns results from all calls on success
