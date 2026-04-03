# rWASM

rWASM (reduced WebAssembly) is a Wasm-derived intermediary representation (IR) used by Fluent’s blended execution architecture.

It is designed to simplify and constrain execution representation for deterministic runtime behavior and proving efficiency,
while keeping practical compatibility with WebAssembly development flows.

## Key Features

- **ZK-friendliness**: a flatter and more constrained binary model than unrestricted Wasm module structure.
- **Developer continuity**: keeps a Wasm-oriented workflow, so existing language/tooling ecosystems remain practical.
- **Deterministic execution intent**: representation choices are made to support reproducible state-transition behavior.

## Important Notice

rWASM is a protocol execution representation, not a generic drop-in replacement for every host Wasm use case.
Always use current Fluent runtime/translator tooling and validation paths when producing or executing rWASM artifacts.
