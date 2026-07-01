# Plugins And Evidence Producers

Plugins are optional capability packages or integrations that can extend an Agent OS installation. A plugin may expose one or more evidence producers, active tools, or both.

Plugins are not required for core operation. Adapters decide which plugins are enabled, disabled, unavailable, or failed for a specific installed repository.

## Contract Foundation

This directory defines the first reusable contract foundation for plugin and evidence-producer work:

- [plugin-contract.md](plugin-contract.md) defines what a plugin is, what it may expose, and how adapters should route it.
- [evidence-producer-contract.md](evidence-producer-contract.md) defines common evidence-producer states, evidence principles, and expected metadata.
- [dependency-boundary/README.md](dependency-boundary/README.md) is the first generic plugin example.

These documents are documentation contracts, not runtime schemas or implementation code.

## Evidence Role

Plugin output is bounded evidence for agent reasoning. It can help answer questions such as "what changed?", "what imports what?", or "which files match this query?"

Evidence is not semantic authority. Plugins and evidence producers must not decide meaning, ownership, product intent, architecture quality, project policy, or whether a change should be made.

Absence from plugin evidence is not proof of absence in source, config, generated output, or project documentation. Agents should treat missing evidence as a limit of the evidence surface and inspect source/config directly when correctness depends on it.

## Active Tool Relationship

When a plugin exposes an active tool, the adapter should still declare the local route:

- logical capability or tool ID;
- command, callable surface, or integration route;
- expected evidence output;
- state and fallback behavior;
- limitations;
- validation or health check when relevant.

The plugin supplies a capability. The adapter decides whether that capability is supported in the installed repository and how agents should invoke, ignore, or report it.

## Dependency-Boundary Example

Dependency-boundary evidence is an example evidence type, not a dependency-cruiser requirement. A repository might use dependency-cruiser, another dependency graph tool, a language-native analyzer, a hand-maintained boundary check, source/config reads, or no dependency-boundary tool at all.

Agent OS must not require dependency-cruiser, JavaScript, TypeScript, pnpm, monorepos, or any specific dependency graph tool as universal assumptions.
