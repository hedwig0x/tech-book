# Data Availability

Data availability (DA) is a fundamental part of rollup correctness.

## Why it matters

Even if execution is correct, verification requires access to the data needed to reconstruct and validate state transitions.

For Fluent, DA constraints influence:

- what transition artifacts must be committed,
- how verifiers can reconstruct state updates,
- how proving and execution pipelines stay auditably connected.

## Architecture relationship

DA should be considered together with execution and proving design:

- execution defines what data is produced,
- proving defines what must be attested,
- DA defines what must remain accessible for independent validation.

## Scope note

This chapter is intentionally high-level.
For concrete DA pipeline implementation and current deployment settings, use current network/runtime documentation.
