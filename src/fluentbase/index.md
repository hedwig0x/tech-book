# Fluentbase Framework

Fluentbase is a framework offering an SDK and a proving system for Fluent STF.
Developers can leverage this framework to create shared applications (smart contracts), dedicated applications, system precompile contracts, or custom STFs.

> **WARNING: Don't use in production!**
>
> *Fluentbase is under experimental development and remains a work in progress. The bindings, methods, and naming conventions within the codebase are not yet standardized and may undergo significant changes. Furthermore, the codebase has not been audited or thoroughly tested, which could result in vulnerabilities or crashes.*

## Modules

- **`bin`**: Binary tools used in build/runtime workflows.
- **`crates`**: Houses Fluentbase modules. The exact set evolves, but major crate families include:
  - **`codec` / `codec-derive`**: ABI codec and derive support.
  - **`contracts`**: system/runtime contracts.
  - **`crypto`**: cryptographic helpers.
  - **`evm` / `revm`**: EVM execution and Fluent-specific REVM integration.
  - **`genesis`**: genesis-generation utilities/assets.
  - **`runtime`**: core runtime execution layer.
  - **`sdk` / `sdk-derive`**: developer SDK, macros, and runtime bindings.
  - **`types`**: shared primitive/protocol types.
  - **`node`**: node integration components.
  - Additional runtime-family and testing support crates (for example SVM-related and harness crates).
- **`e2e`**: end-to-end tests for execution behavior and compatibility paths.
- **`examples`**: contract/application examples built with Fluentbase SDK.

> **Note:** older references to crate names such as `core`, `poseidon`, or `zktrie` may appear in historical discussions.
> Always treat the current `crates/*` tree in the repository as the source of truth.

## Build and Testing

To build Fluentbase, a Makefile is available in the root folder that builds all required dependencies and examples.
Run the `make` command to build all contracts, examples, and genesis files.
The resulting files can be found in:
- **`crates/contracts/assets`**: WASM and rWASM binaries for all precompiled contracts and system contracts.
- **`crates/genesis/assets`**: Reth/geth compatible genesis files with injected rWASM binaries (used by reth).
- **`examples/*`**: Each folder contains `lib.wasm` and `lib.wat` files matching the compiled example bytecode.

For testing, the complete EVM official testing suite, which consumes significant resources, is included. Increase the Rust stack size to 20 MB for testing:

```bash
RUST_MIN_STACK=20000000 cargo test --no-fail-fast
```

**Note:** test status evolves continuously. Check current CI and repository test reports for authoritative pass/fail state.

## Examples

Fluentbase SDK can be used to develop various applications, generally using the same interface. Below is a simple application developed using Fluentbase:

```rust
#![cfg_attr(target_arch = "wasm32", no_std)]
extern crate fluentbase_sdk;

use fluentbase_sdk::{basic_entrypoint, derive::Contract, SharedAPI};

#[derive(Contract)]
struct GREETING<SDK> {
  sdk: SDK,
}

impl<SDK: SharedAPI> GREETING<SDK> {
  fn deploy(&mut self) {
    // any custom deployment logic here
  }
  fn main(&mut self) {
    // write "Hello, World" message into output
    self.sdk.write("Hello, World".as_bytes());
  }
}

basic_entrypoint!(GREETING);
```

## Supported Languages

Fluentbase SDK currently supports writing smart contracts in:
- Rust
- Solidity
- Vyper

## Fluentbase Operation

Fluentbase operates around Fluent's rWASM VM (reduced WebAssembly) and runtime integration layers.
rWASM is Wasm-derived and optimized for Zero-Knowledge (ZK)-oriented execution/proving constraints,
with a reduced/reshaped representation compared with unrestricted host Wasm binaries.

## Limitations and Future Enhancements

As of now, Fluentbase does not support floating-point operations.
However, this feature is on the roadmap for future enhancements.