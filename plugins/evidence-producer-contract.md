# Evidence Producer Contract Foundation

This file defines the first reusable documentation contract for Agent OS evidence producers. It is not a final machine schema and should not be treated as executable configuration.

An evidence producer is a bounded capability that observes a repository, configuration, generated artifact, external service, or other declared input and returns evidence for agent reasoning.

Evidence producers may live inside plugins, project-local tools, adapter-declared commands, or service integrations. They can support decisions, but they do not make those decisions.

In a pinned Agent OS installation, reusable evidence-producer contracts may be consumed from `.agent-os/upstream/`, while target-specific routes and enablement live in `.agent-os/adapter/`. A target repository should not edit upstream evidence-producer contracts to fit local commands or source shape.

## Evidence Principles

Evidence is bounded. Every evidence producer observes only the inputs, time, configuration, and capability surface declared by its contract.

Evidence is not semantic authority. Evidence producers must not decide meaning, ownership, product intent, architecture quality, project policy, or whether a change is correct.

Absence from evidence is not proof of absence in source/config. A missing import, rule, file, symbol, dependency, generated artifact, or policy in evidence output may mean the evidence producer did not observe it, was configured not to include it, failed to parse it, or was stale.

Source/config truth, the user request, human-owned project decisions, and adapter-routed authority remain higher authority than plugin output.

## States

Evidence producers should report one of these states:

- `success`: the evidence producer ran or resolved successfully and returned evidence within its declared bounds.
- `disabled`: the evidence producer is intentionally turned off by adapter, project, user, or policy choice.
- `unavailable`: the evidence producer cannot run because dependencies, permissions, config, source shape, compatible project structure, or required inputs are missing.
- `failed`: the evidence producer was expected to run but execution, parsing, validation, or retrieval failed.

A `disabled`, `unavailable`, or `failed` state is itself useful context. Agents should report the limit honestly and fall back to source/config reads or standard project checks when possible.

Missing upstream contract content should be treated as `unavailable` unless the adapter declares another local contract or provider.

## Expected Metadata

Evidence output should include metadata that helps agents understand what was observed and what was not.

Expected metadata:

- provenance: the plugin, tool, command, service, file, generated artifact, or human-maintained source that produced the evidence;
- config or source input when applicable: relevant config files, source roots, query inputs, target files, or adapter routes used to produce the evidence;
- freshness or observed time when applicable: generation time, execution time, cached-at time, service retrieval time, or known staleness;
- limitations: known blind spots, unsupported source types, omitted paths, parse limits, permission limits, cache behavior, or confidence limits.

## Reporting Guidance

Agents should describe evidence producer output as support, not authority. Prefer wording such as:

- "The dependency-boundary evidence reports..."
- "This producer was unavailable because..."
- "This evidence did not include generated files..."
- "I verified against source/config where correctness depended on it."

Agents should avoid wording that turns bounded evidence into universal truth, such as "there are no imports anywhere" when the producer only scanned configured active-source roots.

## Shape Sketch

This sketch is Markdown/YAML-like for readability only.

```yaml
evidence:
  id: example-evidence
  state: success | disabled | unavailable | failed
  provenance:
    provider: plugin-or-local-tool
    route: adapter-declared route when applicable
  inputs:
    source:
      - paths or query inputs when applicable
    config:
      - config files when applicable
  observedAt: optional timestamp when applicable
  freshness: optional freshness or cache note
  limitations:
    - Known blind spot or unsupported case.
  output:
    summary: Bounded result for agent reasoning.
```
