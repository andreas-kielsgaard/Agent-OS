# Active Tool Map

This is a target-owned active-tool router for an installed Agent OS. It should usually live at `.agent-os/adapter/tool-map.md`.

Tools produce bounded evidence for agent reasoning. They do not decide semantic authority, ownership, product intent, architecture quality, or whether a change is correct.

Tool routes may reference target-repository commands, target-owned scripts, service integrations, or plugins available through the pinned upstream snapshot. They should not require agents to edit `.agent-os/upstream/**`; local enablement, invocation details, and unavailable behavior belong in this map or the adapter.

| Logical Tool ID | Command Or Callable | Use | Expected Evidence | Limitations | Disabled Or Unavailable Behavior | Validation Check |
| --- | --- | --- | --- | --- | --- | --- |
| `affected-surface` | `<command-or-callable>` | Identify source surfaces likely affected by a change. | Bounded affected-surface evidence. | `<known-limits>` | Report unavailable; use source reads and `rg`. | `<check-or-none>` |
| `test-relation` | `<command-or-callable>` | Relate changed source to likely tests or examples. | Bounded test-relation evidence. | `<known-limits>` | Report unavailable; select tests from source/config inspection. | `<check-or-none>` |
| `verification` | `<command-or-callable>` | Suggest or run supported verification for the current change. | Bounded verification evidence. | `<known-limits>` | Report unavailable; run repository-supported checks manually. | `<check-or-none>` |
| `repository-health` | `<command-or-callable>` | Inspect broad repo health when the task needs it. | Bounded repository-health evidence. | `<known-limits>` | Report unavailable; use targeted project checks. | `<check-or-none>` |
| `dependency-boundary` | `<command-or-callable>` | Inspect dependency direction, import boundaries, or equivalent architecture constraints when supported. | Bounded dependency-boundary evidence. | `<known-limits>` | Report unavailable; do not assume a dependency graph tool exists. | `<check-or-none>` |
| `context-bundle` | `<command-or-callable>` | Gather a bounded context bundle for a task. | Bounded context-bundle evidence. | `<known-limits>` | Report unavailable; use selected source reads and search. | `<check-or-none>` |

Add, remove, or rename logical IDs to match the adapter. Do not make a command universal merely because it exists in another repository.

If an upstream plugin or evidence-producer contract is missing from `.agent-os/upstream/`, report that capability as unavailable unless the adapter declares another local provider.
