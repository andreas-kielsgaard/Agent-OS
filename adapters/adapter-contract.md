# Adapter Contract Foundation

This file defines the first reusable documentation contract for Agent OS adapters. It is not a final machine schema and should not be treated as executable configuration.

An adapter is the project-local binding between reusable Agent OS core and one installed repository. It declares what core intentionally does not know: target paths, project-control authority surfaces, supported tools, validation commands, plugin availability, and repository-specific limits.

## Required Meaning

An adapter should declare:

- repository identity;
- installed upstream and adapter paths;
- source groups;
- source policy;
- generated, archive, and protected surfaces;
- project-control routing;
- adapter-declared active tools;
- validation profile;
- enabled plugins and evidence producers;
- capability notes and unavailable capability notes.

## Shape Sketch

This sketch is Markdown/YAML-like for readability only. It is not a final schema.

```yaml
adapter:
  id: local-project-adapter
  repository:
    name: Project Name
    root: .
    remote: origin-or-none
    defaultBranch: main-or-local-default

  installation:
    upstream:
      path: .agent-os/upstream/
      pin: recorded in .agent-os/adapter/install-state.md
      ownership: upstream-owned read-only snapshot
      unavailableBehavior: check install state; report missing upstream content when it cannot be restored
    adapter:
      path: .agent-os/adapter/
      ownership: target-owned binding layer

  sourceGroups:
    - id: active-source
      paths:
        - src/
      role: source-owned implementation
      notes: Primary maintained code for this repository.

  sourcePolicy:
    activeSource:
      - src/
    generated:
      - path: build/
        treatment: evidence-only
    archive:
      - path: archive/
        treatment: historical-context
    protected:
      - path: .agent-os/upstream/
        rule: read-only upstream Agent OS snapshot; update only through explicit pin maintenance
      - path: .agent-os/adapter/
        rule: edit only during explicit Agent OS install or adapter maintenance

  projectControl:
    map: .agent-os/adapter/project-setup-map.md
    routes:
      projectDecisions: <project-decisions-path-or-none>
      architectureDocs: <architecture-docs-path-or-none>
      localPolicies: <policy-path-or-none>
      schemaConfigAuthority: <source-or-config-authority-paths>
      installState: .agent-os/adapter/install-state.md
      localToolMap: .agent-os/adapter/tool-map.md

  activeTools:
    - id: affected-surface
      provider: project-local-or-plugin
      commandOrCallable: <command-or-callable-surface>
      expectedEvidence: bounded affected source surface report
      limitations: <known limits>
      unavailableBehavior: report unavailable; fall back to source reads and rg
      validationCheck: <optional check command>

  validation:
    profile: local-default
    commands:
      - id: format-or-lint
        command: <project command>
        requiredFor: changed source when supported

  evidenceProducers:
    - id: dependency-boundary
      provider: <plugin-or-local-tool>
      state: enabled | disabled | unavailable
      expectedEvidence: bounded dependency-boundary evidence
      notes: Optional; no dependency graph tool is universal.

  capabilityNotes:
    supported:
      - <capability the adapter can route with confidence>
    unavailable:
      - <capability that is absent, disabled, or not yet configured>
```

## Active Tool Routing

An active tool is a project-local or plugin-provided capability that an adapter exposes to Agent OS. Active tools produce bounded evidence for agent reasoning. They do not decide meaning, authority, ownership, product intent, architectural quality, or whether a change is correct.

An active tool route should include:

- logical tool ID;
- invocation command or callable surface;
- expected evidence output;
- limitations;
- unavailable or disabled behavior;
- validation or health check command when relevant.

Logical IDs should describe the evidence need rather than universal command names. Examples:

- `affected-surface` evidence;
- `test-relation` evidence;
- `verification` evidence;
- `repository-health` evidence;
- `dependency-boundary` evidence;
- `context-bundle` evidence.

No Field Platform command, package script, dependency graph tool, or context command is universal. If a repository cannot support an active tool, the adapter should say so explicitly and describe the fallback behavior.

## Pinned Upstream Consumption

When Agent OS is consumed from a pinned snapshot, the adapter is the target-owned binding between that snapshot and the installed repository.

The default upstream snapshot path is `.agent-os/upstream/`. It may be a submodule, vendored copy, generated copy, archived snapshot, or another repository-approved delivery mechanism. Regardless of mechanism, upstream content is read-only from the target repository. Target-specific changes should be made in `.agent-os/adapter/` or other target-owned authority surfaces, not by editing `.agent-os/upstream/**`.

The adapter should either declare the installed paths directly or route agents to install state that records them. If the upstream snapshot is missing, partial, or unavailable, the adapter should tell agents where to find restoration guidance or how to report the missing capability. Agents should not replace a missing pin with remote `HEAD` or a copy from another target repository.

## Project-Control Routing

Project-control routing is the adapter-owned map from Agent OS into target-repository authority surfaces. It can route to:

- project decisions;
- architecture docs;
- local policies;
- schema, config, and source authority;
- install state;
- local tool maps.

Project-control routing is local to the installed repository. It is not part of reusable core, and it does not make project decisions itself. The route tells an agent where to look; the routed documents, source files, config files, or human instructions carry whatever authority they already have in that project.

## Evidence And Limits

Adapter-declared tools and plugin outputs are evidence. Generated output and tool output may support reasoning, but they remain below source/config truth, human-owned project decisions, and the user request.

An adapter should report unsupported capabilities honestly. A correct adapter can say that a plugin is absent, a command is unavailable, a route is unresolved, or a validation profile is partial.
