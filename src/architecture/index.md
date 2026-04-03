# Architecture

Fluent is an Ethereum Layer L2 rollup designed to natively execute EVM, SVM and Wasm-based programs.
Fluent exists as a unified state machine,
where all contracts can call each other, regardless of which VM they were originally built for.

As a rollup, Fluent supports scalable and efficient execution by committing state changes to Ethereum L1.
This process involves compressing the state changes using ZK proofs, specifically SNARKs.

<p align="center">
   <img src="../images/fluent-arch.png" alt=""/>
   <br/>
   <i>The base architecture of Fluent</i>
</p>

Fluent currently operates on a modified [Reth](https://github.com/fluentlabs-xyz/reth) stack,
with Fluent-specific execution/runtime integration.
It maintains compatibility with core Ethereum data formats (for example transactions and blocks),
while extending runtime behavior for blended execution.

Furthermore,
Fluent is designed around a fork-less runtime upgrade model
by keeping critical execution logic in upgradable runtime paths.

> **Implementation note:** exact fork-level compatibility policy (for example Prague-era assumptions)
> is release-dependent and should be validated against the active runtime/release branch rather than treated as a permanent invariant in this chapter.