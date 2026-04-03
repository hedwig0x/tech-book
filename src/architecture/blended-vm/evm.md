# EVM

Fluent integrates with the EVM by leveraging special EVM precompiled contracts.
These contracts facilitate the execution of EVM bytecode,
enabling the deployment and operation of smart contracts designed for the EVM ecosystem.
This allows developers to deploy applications built for EVM platforms using languages like Solidity or Vyper.

The EVM executor, a Rust-based smart contract, provides two key functions:

1. **`deploy`**: Deploys the EVM application and stores the bytecode state.
2. **`main`**: Executes the already deployed EVM application.

During deployment, a specialized rWasm proxy is deployed under the smart contract address.
This proxy redirects all deployment and execution calls to the EVM executor.

The deployment and interaction model is intended to stay close to Ethereum-compatible expectations.
In practice, this provides a smooth migration path for most EVM apps.

> **Status note:** Fluent still applies runtime-routing and host-governed execution boundaries,
> so implementation details can differ in some edge cases versus vanilla upstream EVM nodes.

