# Dependency-Boundary Plugin Example

Dependency-boundary is the first generic Agent OS plugin example. It describes a possible evidence producer for dependency direction, import boundaries, module relationships, or equivalent architecture constraints.

This example is not dependency-cruiser-specific. It does not require JavaScript, TypeScript, pnpm, monorepos, dependency-cruiser, or any specific dependency graph implementation.

## Purpose

A dependency-boundary evidence producer can help agents inspect questions such as:

- which source areas import or depend on other source areas;
- whether declared boundary rules were checked;
- which files or modules participated in a dependency graph;
- whether a dependency-boundary check succeeded, was disabled, was unavailable, or failed.

The evidence is bounded support for reasoning. It does not decide architecture quality, ownership, intended layering, or whether a change is correct.

## Possible Implementations

A repository might implement dependency-boundary evidence with:

- a dependency graph tool;
- a language-native analyzer;
- a build-system query;
- a static import scanner;
- a hand-maintained boundary document plus validation check;
- source/config reads performed without a dedicated tool.

The adapter should declare the actual provider and route for the installed repository.

## Expected States

The dependency-boundary evidence producer should report:

- `success`: dependency-boundary evidence was produced within the declared source/config bounds.
- `disabled`: the adapter or project intentionally does not use dependency-boundary evidence.
- `unavailable`: required tooling, config, permissions, source shape, or compatible project structure is missing.
- `failed`: the configured producer was expected to run but execution, parsing, validation, or retrieval failed.

## Expected Metadata

Dependency-boundary evidence should include:

- provenance: provider name, tool, command, file, service, or manual source used;
- config or source input when applicable: source roots, config files, boundary docs, query inputs, ignored paths, or generated artifacts used;
- freshness or observed time when applicable: run time, generated-at time, cache time, or known staleness;
- limitations: unsupported languages, omitted paths, generated files excluded, parse limits, dynamic import limits, unresolved aliases, or partial graph coverage.

## Evidence Limits

Absence from dependency-boundary evidence is not proof of absence in source/config. A relationship may be missing because the producer did not scan the relevant paths, could not parse a file, omitted generated output, ignored dynamic behavior, or used stale input.

Agents should use dependency-boundary evidence alongside source reads, config reads, adapter routes, and project authority when boundary correctness matters.
