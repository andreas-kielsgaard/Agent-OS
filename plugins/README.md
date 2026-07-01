# Plugins And Evidence Producers

Plugins and evidence producers are optional deterministic integrations that produce bounded evidence for agents. They help answer questions such as "what changed?", "what imports what?", or "which files match this query?" without taking over project judgment.

Plugins are evidence-only. They must not decide meaning, authority, ownership, product intent, architectural quality, or whether a change should be made. Agents can use plugin output as support, but the user request, project authority, source/config truth, and human-owned project decisions remain higher authority.

Each plugin should expose explicit behavior for:

- enabled and configured;
- disabled by adapter choice;
- unavailable because dependencies, config, or compatible project structure are missing;
- failed execution with enough metadata for an agent to report the limit honestly.

## First Known Candidate

`dependency-cruiser` is the first known plugin candidate because Field Platform already uses dependency-cruiser evidence to inspect active source boundaries. It should remain optional. Agent OS must not require dependency-cruiser, JavaScript, TypeScript, pnpm, monorepos, or any specific dependency graph tool as universal assumptions.

Future plugin work should define the evidence-producer contract before adding more integrations.
