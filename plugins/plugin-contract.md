# Plugin Contract Foundation

This file defines the first reusable documentation contract for Agent OS plugins. It is not a final machine schema and should not be treated as executable configuration.

A plugin is an optional capability package or integration that may expose evidence producers, active tools, or both. Plugins extend what an installed Agent OS can observe or invoke, but they do not replace adapter routing, project authority, source/config truth, or human judgment.

## Required Meaning

A plugin should declare:

- plugin ID;
- capability purpose;
- exposed evidence producers, active tools, or both;
- expected adapter routing requirements;
- supported states for each exposed capability;
- required input sources or config, when applicable;
- expected evidence output;
- limitations;
- validation or health check behavior, when relevant.

## Adapter Relationship

Adapters own repository-specific enablement. A plugin being available in the reusable Agent OS repository does not mean it is enabled or compatible with every installed repository.

In a pinned installation, reusable plugin contracts or examples may be read from `.agent-os/upstream/`, but target-specific plugin enablement belongs in `.agent-os/adapter/`. Agents should not edit upstream plugin files to enable, disable, or configure a plugin for one target repository.

An adapter should declare whether a plugin capability is:

- enabled and usable for the repository;
- disabled by adapter or project choice;
- unavailable because dependencies, config, source shape, permissions, or compatible project structure are missing;
- failed during execution or validation.

If an adapter does not declare a plugin route, agents should treat that plugin capability as absent.

If expected upstream plugin content is missing from the pinned snapshot, agents should report that capability as unavailable unless the adapter declares another local provider.

## Active Tools

A plugin may expose an active tool when it provides a command, callable surface, service integration, or scripted operation that agents can invoke.

An active tool route should include:

- logical tool ID;
- provider plugin;
- invocation surface;
- expected evidence output or side effect;
- required inputs;
- limitations;
- unavailable, disabled, and failed behavior;
- validation or health check, when relevant.

Active tools are not automatically authoritative. If an active tool produces evidence, that evidence remains bounded by the tool contract and should be compared with source/config truth when needed.

## Evidence Producers

A plugin may expose one or more evidence producers. Evidence producers should follow [evidence-producer-contract.md](evidence-producer-contract.md).

Evidence producers may be implemented by command-line tools, local scripts, language analyzers, service APIs, generated artifacts, or human-maintained files. The reusable contract describes the evidence surface, not a mandatory implementation.

## Shape Sketch

This sketch is Markdown/YAML-like for readability only.

```yaml
plugin:
  id: example-plugin
  purpose: Bounded evidence or active capability for an installed repository.
  capabilities:
    - id: example-evidence
      type: evidence-producer
      states:
        - success
        - disabled
        - unavailable
        - failed
      requiredInputs:
        - source paths or config when applicable
      expectedMetadata:
        - provenance
        - config or source input when applicable
        - freshness or observed time when applicable
        - limitations
    - id: example-tool
      type: active-tool
      invocation: adapter-declared command or callable surface
      expectedEvidence: bounded evidence output
      limitations: Known limits and unsupported cases.
```
