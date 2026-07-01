# Install Instructions

Agent OS installation is implementation-agent work. The agent should inspect the target repository, classify the install mode, create a local adapter, wire only supported tools and plugins, place local route templates, and validate the result against the project's real stack.

## Installation Flow

1. Inspect the target repository.
2. Classify the install mode: greenfield, reference-installation, or messy adoption.
3. Identify source, generated, archive, and protected surfaces.
4. Identify project-control authority surfaces, including project decisions, architecture docs, local policies, schema/config/source authority, install state, and local tool maps.
5. Choose active tools and plugins actually supported by the repository.
6. Create adapter docs or config with source groups, source policy, project-control routing, active tools, validation profile, plugins, and capability notes.
7. Place local entry and routing templates, usually `AGENTS.md`, a project-control map, and a tool map.
8. Validate with available checks and representative evidence operations.
9. Report unsupported capabilities, disabled plugins, missing tooling, and unresolved boundaries honestly.

## Outputs

A basic install should leave the target repository with:

- an adapter document or adapter config;
- a root `AGENTS.md` entry contract;
- a project-control route map;
- an active tool map;
- a validation profile;
- explicit notes for unavailable capabilities.

Initial templates live in [templates/](templates/):

- [AGENTS.md](templates/AGENTS.md);
- [project-setup-map.md](templates/project-setup-map.md);
- [tool-map.md](templates/tool-map.md).

See [installation-modes.md](installation-modes.md) for mode-specific priorities.

## Boundaries

Install instructions should not promise universal support. A correct install can say that a plugin is disabled, a capability is unavailable, or a repository needs a project decision before Agent OS can route confidently.

Installation should not copy reference project-control files verbatim, make any specific plugin mandatory, or turn local project decisions into reusable core guidance.
