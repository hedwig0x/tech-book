# L2 Rollup

Fluent is built as an Ethereum L2 execution layer with a blended execution architecture.

At the rollup level, the system combines:

- execution inside Fluent’s runtime model,
- deterministic state transition outputs,
- proof/data pipelines anchored to Ethereum.

## Why this matters for architecture

Many design choices in Fluent’s execution layer are shaped by rollup constraints:

- deterministic execution for reproducible proofs,
- explicit host/runtime boundaries for verifiable state transitions,
- predictable metering and side-effect ordering.

So rollup concerns are not “outside” architecture—they are one of its core inputs.

## Scope

The chapters below describe the high-level context for:

- proof systems,
- data availability.

They are intentionally architecture-oriented and may evolve as proving/DA implementation details evolve.
