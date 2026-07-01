# Project Setup Map

This is a local project-control router for an installed Agent OS. It routes agents to target-repository authority surfaces; it does not own product decisions, architecture decisions, source truth, or local policy.

| Route | Local Surface | Owner | Use | Notes |
| --- | --- | --- | --- | --- |
| Project decisions | `<path-or-none>` | `<human/project owner>` | Mature human-owned decisions and explicit tradeoffs. | Route only; decisions live in the linked surface. |
| Architecture docs | `<path-or-none>` | `<human/project owner>` | Architecture context, diagrams, ADRs, or boundary notes. | Note stale or advisory status when known. |
| Local policies | `<path-or-none>` | `<human/project owner>` | Repository-specific workflow, review, security, release, or contribution rules. | Do not promote policy into core. |
| Adapter config | `<path-to-adapter>` | Agent OS installation | Source policy, project-control routes, active tools, validation profile, plugins, and capability notes. | Adapter binds core to this repo. |
| Active tool map | `<path-to-tool-map>` | Agent OS installation | Logical tool IDs, commands or callables, evidence outputs, and limitations. | Tools produce bounded evidence only. |
| Validation profile | `<path-or-command-list>` | Repository/tooling owner | Checks that are supported by this repo. | Include unavailable checks explicitly. |
| Source/config authority | `<paths>` | Repository source owners | Source, schema, config, contracts, migrations, generated-source inputs, or equivalent authority. | Source/config truth outranks generated evidence. |
| Install state | `<path-or-none>` | Agent OS installation | Installed Agent OS version, adapter status, known gaps, and maintenance notes. | Keep concise and factual. |

When a route is unknown, write `unresolved` or `none` instead of inventing an authority surface.
