# Install Instructions

Agent OS installation is implementation-agent work. The agent should inspect the target repository, classify the install mode, install or verify a pinned upstream Agent OS snapshot, create a local adapter, wire only supported tools and plugins, place local route templates, and validate the result against the project's real stack.

The default pinned layout separates upstream-owned content from target-owned adaptation:

- `.agent-os/upstream/` is the pinned Agent OS snapshot. It is read-only from the target repository.
- `.agent-os/adapter/` is the target-owned adapter layer for repository paths, project-control routes, active tools, validation, plugins, capability notes, and install state.

## Installation Flow

1. Inspect the target repository.
2. Classify the install mode: greenfield, reference-installation, or messy adoption.
3. Verify or place the pinned upstream snapshot, usually at `.agent-os/upstream/`.
4. Create or update target-owned adapter files, usually under `.agent-os/adapter/`.
5. Identify source, generated, archive, and protected surfaces, including upstream-owned Agent OS content.
6. Identify project-control authority surfaces, including project decisions, architecture docs, local policies, schema/config/source authority, install state, and local tool maps.
7. Choose active tools and plugins actually supported by the repository.
8. Create adapter docs or config with source groups, source policy, project-control routing, active tools, validation profile, plugins, and capability notes.
9. Place local entry and routing templates, usually `AGENTS.md`, `.agent-os/adapter/project-setup-map.md`, `.agent-os/adapter/tool-map.md`, and `.agent-os/adapter/install-state.md`.
10. Validate with available checks and representative evidence operations.
11. Report unsupported capabilities, disabled plugins, missing tooling, missing upstream snapshot content, and unresolved boundaries honestly.

## Outputs

A basic install should leave the target repository with:

- an adapter document or adapter config;
- a root `AGENTS.md` entry contract;
- a project-control route map;
- an active tool map;
- a validation profile;
- an install-state record with the pinned upstream identifier and availability status;
- explicit notes for unavailable capabilities.

Initial templates live in [templates/](templates/):

- [AGENTS.md](templates/AGENTS.md);
- [project-setup-map.md](templates/project-setup-map.md);
- [install-state.md](templates/install-state.md);
- [tool-map.md](templates/tool-map.md).

See [installation-modes.md](installation-modes.md) for mode-specific priorities.
See [pinned-consumption.md](pinned-consumption.md) for the upstream snapshot and adapter ownership contract.

## Boundaries

Install instructions should not promise universal support. A correct install can say that a plugin is disabled, a capability is unavailable, or a repository needs a project decision before Agent OS can route confidently.

Installation should not copy reference project-control files verbatim, make any specific plugin mandatory, or turn local project decisions into reusable core guidance.

Installation should not adapt Agent OS by editing `.agent-os/upstream/**`. Target-specific binding belongs in `.agent-os/adapter/**`; reusable Agent OS changes belong upstream and should be consumed through an explicit pin update.
