# AGENTS.md

This repository has a local Agent OS installation.

For non-trivial implementation, documentation, review, refactor, or repository-maintenance work, load the installed Agent OS bootloader first:

```text
<local-agent-os-install>/core/agent-os-bootloader.md
```

Then follow the local project adapter before assuming repository paths, project-control routes, active tools, plugins, or validation commands.

The local project adapter owns:

- project-control routing;
- active-tool routing;
- source, generated, archive, and protected surface policy;
- validation profile;
- enabled, disabled, and unavailable plugins or evidence producers.

This file is an entry contract only. It does not own product decisions, architecture decisions, source authority, command semantics, or plugin availability.

If the installed bootloader, adapter, project-control map, or tool map is missing or unavailable, report that honestly and proceed with ordinary source reads, search, and project checks supported by this repository.
