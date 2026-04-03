# ZK Proof System

Fluent’s blended execution architecture is designed with proving in mind from the start.

## Core objective

Represent state transitions from heterogeneous execution environments in one coherent model, instead of proving many isolated execution domains with heavy emulation boundaries.

## Architectural consequences

This objective impacts multiple layers:

- rWasm execution representation,
- interruption/resume control flow,
- syscall determinism,
- gas/fuel accounting consistency,
- deterministic commit semantics.

In other words, proving is a first-class architecture constraint, not an optional optimization.

## Practical note

Exact proving pipeline details (circuits, proving backends, recursion strategy, batching) may change over time.
This chapter focuses on architecture intent and constraints, not a frozen implementation spec.
