# WebAssembly

Fluent offers near-native support for Wasm, with the primary distinction being that, during deployment, it's compiled
into rWasm.
A Wasm application can use Fluent system-call interfaces, subject to the same host-governed execution and metering rules as other runtime paths.

During the deployment process,
Fluent enhances the rWasm codebase with additional checks for gas measurement and modifies certain instructions or
segment structures when necessary.
For more details, refer to the [rWasm section](rwasm.md).