# Agent OS

Agent OS is reusable, agent-installable infrastructure for helping implementation agents orient, select context, route authority, and use evidence inside a repository. It is not plug-and-play magic, a universal project template, or a replacement for product and architecture judgment.

The reusable repository is organized around four visible layers:

- **Core**: bootloader, task modes, behaviors, lenses, skills, execution guidance, and evidence-vs-authority rules.
- **Adapters**: per-repository bindings that tell Agent OS where source, generated output, archive material, local capabilities, project-control files, validation commands, and enabled evidence producers live.
- **Plugins and evidence producers**: optional deterministic integrations that produce bounded evidence for agents.
- **Install instructions**: implementation-agent guidance for inspecting a target repository, creating an adapter, wiring commands, choosing supported plugins, and validating the installation.

Field Platform is the current reference installation. It demonstrates a working local Agent OS, adapter, project-control routing model, and first evidence-producer pattern. It is not the universal template, and Field Platform paths, domain language, package scripts, validation profile, app architecture, and project decisions must remain Field Platform-specific unless a later extraction task explicitly generalizes them.

Tools and evidence help agents inspect reality. They do not decide meaning, authority, ownership, product intent, architectural quality, or whether a change is correct. Those decisions stay with the user request, project authority, source/config truth, and explicit human-owned project decisions.

## Current Scope

This branch creates the repository foundation only. It does not copy the Field Platform Agent OS files, implement CLI packages, implement plugins, publish npm metadata, promise universal support, or require dependency-cruiser.
