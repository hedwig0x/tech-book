# Account Trie

The account structure in rWASM-oriented execution is designed to be as simple as possible, containing only the most essential fields.
It is aligned with Ethereum account fundamentals, while Fluent can apply additional runtime metadata/routing semantics where needed.

```rust
pub struct Account {
    pub address: Address,
    pub balance: U256,
    pub nonce: u64,
    pub code_hash: B256,
    pub code_size: u64,
}
```

Fields description:
- **`address`**: This transient field holds the account address. Currently, a 20-byte address is used to ensure compatibility with the EVM account structure. However, there is a possibility of extending this to 32 bytes in the future to align with the state trie account path, thereby enhancing interoperability.
- **`balance`**: Represents the account balance as a 256-bit element. This is consistently expressed as a 256-bit Big Endian value, although future changes may be considered.
- **`nonce`**: Indicates the number of transactions initiated by this account. It increments with each transaction, call, or contract creation, regardless of the operation's success.
- **`code_hash`**: Represents the account code hash in the active execution/account representation.
  In routed/runtime-managed flows this may involve Fluent-specific transformations, while EVM-facing compatibility paths may expose Ethereum-expected behavior.
- **`code_size`**: Denotes size information for the code representation used by the active runtime/account path.

## State Trie

Fluent operates with state tries through a pure functional approach,
where every smart contract and root-STF can be represented as a function.
In this model, the input provides a list of dependencies,
and the output yields an execution result along with a number of logs.

However, this isn't entirely feasible due to cold storage reads and external storage dependencies,
such as CODEHASH-like EVM opcodes.
To address this, Fluent employs an interruption system to "request" missing information from the root-STF.
This is particularly useful for operations involving cold storage or invalidated warm storage.

The same concept is also used to handle nested calls without incurring additional simulation overhead.
