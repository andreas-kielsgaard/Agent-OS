# Change Impact Checklists

Use these as quick prompts, not exhaustive requirements. Prefer source/config/tooling, `rg`, adapter-declared active tools, plugin evidence producers, and targeted checks over broad documentation churn.

## Domain Concept Change

- Source/config/test surfaces that encode the concept.
- Schema, contracts, validators, fixtures, and persistence source.
- Routes, UI labels, copy, mocks, and tests.
- Adapter-surfaced project decisions only when mature human-owned context is directly relevant.

## Shared Component Change

- Shared or local UI source, styles, primitives, stories, examples, and consumers found with `rg`.
- Adapter-declared affected-surface evidence for affected source.
- Adapter-declared test-relation and verification evidence for verification planning.
- Final response notes for scoped compromises or provisional status.

## Permission Change

- Policy predicates, server guards, guarded screens/components, fixtures, and tests.
- Source literals and call sites found with `rg`.
- Dependency boundaries when policy ownership or UI access changes.

## Route Or Page Change

- Route config, route modules, page shell, module public entrypoints, policy/source checks, URL state, and tests.
- Adapter-declared affected-surface evidence for affected source.
- Adapter-declared verification evidence for final check selection.

## Mock Data Change

- Fixture/mock source, schema/contracts, validators, stories, examples, and tests.
- Source occurrences found with `rg`.
- Known realism caveats reported in the final response when relevant.

## Refactor

- Imports and consumers found with `rg`.
- Adapter-declared affected-surface evidence and dependency-boundary evidence when available.
- Tests and adapter-declared verification evidence.
- Adapter-surfaced project decisions only when a mature human-owned convention changed.
- Final response if staying in scope leaves a real compromise.

## Update Rules

- Update when a recurring review miss appears.
- Update when a new task family needs explicit impact checks.
- Keep each checklist short enough to use during real work.
