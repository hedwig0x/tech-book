# Blended Execution

Blended Execution is Fluent’s approach to executing smart contracts from diverse VMs inside one shared state machine.

It does this by using a unified execution representation (rWasm) and a host-governed control model,
so different runtime styles can compose natively without being split into isolated domains.

This system enables verification of state transitions in one execution environment,
reducing the emulation overhead that usually appears in nested multi-VM designs.

Because applications share one execution space, Fluent supports native composability across supported runtime families.
Compilation/translation tooling is used to bring different bytecode formats into Fluent’s execution model while preserving developer ergonomics.

Ultimately, blended execution acts as a unified state-transition representation model,
streamlining development and expanding what builders can compose on Ethereum L2.

## BlendedVM vs MultiVM

**MultiVM** is an execution layer that provides multiple VM engines side-by-side.
It gives flexibility, but also introduces operational complexity:

- separate VM assumptions,
- different ISA-level constraints,
- increased surface for metering and security mistakes.

**BlendedVM** takes a different path.
Instead of keeping isolated VM silos, it uses one execution/control model to represent multiple runtime behaviors through translation/runtime routing.

This architecture improves composability and makes security boundaries easier to centralize,
while still allowing extension to additional VMs/EEs over time.
