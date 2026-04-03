# Introduction

> **Note:** This document is a work in progress. Its structure is not finalized, and parts of the content may still change.

Fluent is a [blended execution network](https://mirror.xyz/fluentlabs.eth/8IelEprNblwr1HENCzbp9WFEc7FieEapD5SAiBNUBGA):
an Ethereum L2 and framework that blends Wasm, EVM, and (roadmap) SVM-style smart-contract execution into one shared execution environment.

Smart contracts from different VM targets can directly call each other on Fluent.
Fluent is in public devnet and currently supports apps composed of Solidity, Vyper, and Rust contracts.

## Reading this book safely

This tech-book combines architecture intent and implementation examples.
When you need exact current behavior, always cross-check with:

- `fluentlabs-xyz/fluentbase` docs,
- the active `fluentlabs-xyz/reth` patched release branch.
