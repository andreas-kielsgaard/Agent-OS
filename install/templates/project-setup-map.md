# Project Setup Map

This is a target-owned project-control router for an installed Agent OS. It should usually live at `.agent-os/adapter/project-setup-map.md`. It routes agents to target-repository authority surfaces; it does not own product decisions, architecture decisions, source truth, or local policy.

| Route | Local Surface | Owner | Use | Notes |
| --- | --- | --- | --- | --- |
| Upstream Agent OS snapshot | `.agent-os/upstream/` | Agent OS upstream | Pinned reusable core, install, adapter, plugin, and evidence-producer contracts. | Read-only from this target repository; update by explicit pin maintenance. |
| Project decisions | `<path-or-none>` | `<human/project owner>` | Mature human-owned decisions and explicit tradeoffs. | Route only; decisions live in the linked surface. |
| Architecture docs | `<path-or-none>` | `<human/project owner>` | Architecture context, diagrams, ADRs, or boundary notes. | Note stale or advisory status when known. |
| Local policies | `<path-or-none>` | `<human/project owner>` | Repository-specific workflow, review, security, release, or contribution rules. | Do not promote policy into core. |
| Adapter config | `.agent-os/adapter/adapter.md` | Target Agent OS adapter | Source policy, project-control routes, active tools, validation profile, plugins, and capability notes. | Adapter binds pinned upstream core to this repo. |
| Active tool map | `.agent-os/adapter/tool-map.md` | Target Agent OS adapter | Logical tool IDs, commands or callables, evidence outputs, and limitations. | Tools produce bounded evidence only. |
| Validation profile | `<path-or-command-list>` | Repository/tooling owner | Checks that are supported by this repo. | Include unavailable checks explicitly. |
| Source/config authority | `<paths>` | Repository source owners | Source, schema, config, contracts, migrations, generated-source inputs, or equivalent authority. | Source/config truth outranks generated evidence. |
| Install state | `.agent-os/adapter/install-state.md` | Target Agent OS adapter | Installed upstream pin, adapter status, known gaps, and maintenance notes. | Keep concise and factual. |

When a route is unknown, write `unresolved` or `none` instead of inventing an authority surface.
