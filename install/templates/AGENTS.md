# AGENTS.md

This repository has a local Agent OS installation.

For non-trivial implementation, documentation, review, refactor, or repository-maintenance work, load the installed Agent OS bootloader first:

```text
.agent-os/upstream/core/agent-os-bootloader.md
```

Then follow the local project adapter before assuming repository paths, project-control routes, active tools, plugins, or validation commands:

```text
.agent-os/adapter/adapter.md
```

Ownership:

- `.agent-os/upstream/` is the pinned upstream Agent OS snapshot. Read it for guidance, but do not edit it from this target repository.
- `.agent-os/adapter/` is the target-owned Agent OS adapter layer. It owns local routes, tools, validation, plugin states, capability notes, and install state.

The local project adapter owns:

- project-control routing;
- active-tool routing;
- source, generated, archive, and protected surface policy;
- validation profile;
- enabled, disabled, and unavailable plugins or evidence producers.

This file is an entry contract only. It does not own product decisions, architecture decisions, source authority, command semantics, or plugin availability.

If `.agent-os/upstream/` or the bootloader is missing, partial, or unavailable, check `.agent-os/adapter/install-state.md` for the recorded pin and restoration guidance. If the upstream snapshot cannot be restored within the current task, report Agent OS upstream guidance as unavailable and proceed only with ordinary source reads, search, and project checks supported by this repository.

If the adapter, project-control map, or tool map is missing or unavailable, report that honestly and proceed with ordinary source reads, search, and project checks supported by this repository.
