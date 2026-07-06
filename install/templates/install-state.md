# Agent OS Install State

This is a target-owned maintenance record for a local Agent OS installation. It should usually live at `.agent-os/adapter/install-state.md`.

## Installed Layout

| Surface | Path | Owner | Status | Notes |
| --- | --- | --- | --- | --- |
| Upstream Agent OS snapshot | `.agent-os/upstream/` | Agent OS upstream | `<available | missing | partial | unavailable>` | Read-only from this target repository. |
| Target adapter | `.agent-os/adapter/` | Target repository | `<available | incomplete | unavailable>` | Target-owned routes, tools, validation, and capability notes. |
| Root entry contract | `AGENTS.md` | Target repository | `<available | missing>` | Routes agents to upstream bootloader and local adapter. |

## Upstream Pin

| Field | Value |
| --- | --- |
| Delivery mechanism | `<submodule | vendored snapshot | generated copy | archived snapshot | other>` |
| Pinned identifier | `<commit | tag | archive digest | other immutable id>` |
| Upstream source | `<repo-url-or-source-note>` |
| Last verified | `<date-or-none>` |
| Local update procedure | `<path-or-note>` |

## Adapter Status

| Field | Value |
| --- | --- |
| Adapter config | `.agent-os/adapter/adapter.md` |
| Project-control map | `.agent-os/adapter/project-setup-map.md` |
| Active tool map | `.agent-os/adapter/tool-map.md` |
| Validation profile | `<path-or-command-list>` |
| Known gaps | `<none-or-list>` |

## Missing Upstream Handling

If `.agent-os/upstream/` is missing, partial, or unreadable:

1. Check the upstream pin and delivery mechanism above.
2. Use the documented local update or restoration procedure when one exists and the current task permits it.
3. If the snapshot cannot be restored, report Agent OS upstream content as unavailable.
4. Do not replace the missing snapshot with remote `HEAD`, another target repository's copy, or local edits under `.agent-os/upstream/**`.

## Maintenance Notes

Record concise factual notes about pin updates, adapter migrations, disabled capabilities, unavailable plugins, or unresolved install gaps. Keep product decisions and architecture decisions in their project-owned authority surfaces instead.
