# Install Instructions

Agent OS installation is work for an implementation agent. The agent should inspect the target repository, create a local adapter, wire only supported commands, and validate the result against the project's real stack.

## Installation Flow

1. Inspect the target repository.
2. Identify the stack, package manager, languages, framework surfaces, and existing automation.
3. Identify active source roots, generated roots, archive roots, protected surfaces, and human-owned project-decision locations.
4. Select optional plugins and evidence producers that the repository can actually support.
5. Create the project adapter with source groups, source policy, capabilities, enabled plugins, project-control routing, and validation profile.
6. Wire commands or scripts needed for the adapter and selected evidence producers.
7. Add project-control files that route Agent OS into local authority without moving project-specific decisions into core.
8. Validate the install with available checks and a small set of representative context/evidence operations.
9. Report unsupported plugins, missing tooling, and unresolved boundaries explicitly.

## Installation Modes

- **Greenfield**: install Agent OS before much project structure exists. Keep the adapter small, mark unknowns honestly, and avoid inventing architecture decisions.
- **Reference installation**: use an existing working Agent OS installation as source context. Extract reusable material deliberately and keep project-specific paths, commands, and decisions local.
- **Messy adoption**: install into a repo with mixed history, unclear ownership, generated clutter, or partial conventions. Prioritize source policy, archive/generated boundaries, and conservative validation before adding plugins.

Install instructions should not promise universal support. A correct install can say that a plugin is disabled, a capability is unavailable, or a repository needs a project decision before Agent OS can route confidently.
