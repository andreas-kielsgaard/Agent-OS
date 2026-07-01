# Plugins And Evidence Producers

Plugins and evidence producers are optional deterministic integrations that produce bounded evidence for agents. They help answer questions such as "what changed?", "what imports what?", or "which files match this query?" without taking over project judgment.

Plugins are evidence-only. They must not decide meaning, authority, ownership, product intent, architectural quality, or whether a change should be made. Agents can use plugin output as support, but the user request, project authority, source/config truth, and human-owned project decisions remain higher authority.

Plugins and evidence producers can provide active tools or evidence surfaces. Adapters enable, disable, configure, and route those capabilities for each installed repository. Plugin absence is valid and should be explicit in the adapter.

Each plugin should expose explicit behavior for:

- enabled and configured;
- disabled by adapter choice;
- unavailable because dependencies, config, or compatible project structure are missing;
- failed execution with enough metadata for an agent to report the limit honestly.

## Active Tool Relationship

When a plugin provides an active tool, the adapter should still declare the local route:

- logical tool ID;
- command or callable surface;
- expected evidence output;
- limitations;
- disabled or unavailable behavior;
- validation or health check when relevant.

The plugin supplies bounded evidence. The adapter decides whether that evidence producer is available for this repository and how agents should invoke or ignore it.

## Dependency-Boundary Evidence

Dependency-boundary evidence is an example evidence type, not a mandatory dependency-cruiser requirement. A repository might use dependency-cruiser, another dependency graph tool, a language-native analyzer, a hand-maintained boundary check, or no dependency-boundary tool at all.

Agent OS must not require dependency-cruiser, JavaScript, TypeScript, pnpm, monorepos, or any specific dependency graph tool as universal assumptions.

Future plugin work should define the evidence-producer contract before adding more integrations.
