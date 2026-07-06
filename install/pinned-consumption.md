# Pinned Consumption Contract

Pinned consumption lets a target repository use a fixed Agent OS snapshot while keeping target-specific adaptation outside upstream-owned content.

The default installed layout is:

| Surface | Default Path | Ownership | Edit Rule |
| --- | --- | --- | --- |
| Upstream Agent OS snapshot | `.agent-os/upstream/` | Agent OS upstream | Read-only from the target repository. |
| Target adapter | `.agent-os/adapter/` | Target repository | Editable during Agent OS install or explicit adapter maintenance. |
| Root entry contract | `AGENTS.md` | Target repository | Routes agents to the pinned upstream bootloader and local adapter. |

An installation may use a git submodule, vendored snapshot, generated copy, archived snapshot, or another repository-approved delivery mechanism. The delivery mechanism does not change the ownership rule: consumed upstream content remains upstream-owned, and target-specific binding belongs in the adapter.

## Upstream Snapshot

The pinned upstream snapshot should contain the reusable Agent OS core, install docs, adapter contract docs, plugin contract docs, and any reusable evidence-producer examples selected by the installed pin.

Target repositories should not edit `.agent-os/upstream/**` to make Agent OS fit local paths, commands, project decisions, validation profiles, plugins, or evidence producers. If reusable Agent OS content is wrong, update Agent OS upstream in its source repository or through an explicit upstream maintenance flow, then repin the target repository to the new snapshot.

During ordinary target-repository work, agents may read `.agent-os/upstream/**` for guidance, but should treat it as protected, upstream-owned input.

## Target Adapter

The target adapter should live under `.agent-os/adapter/` unless the install state records a different target-owned path.

The adapter owns target-specific binding:

- repository identity and source groups;
- source, generated, archive, and protected surface policy;
- project-control routing;
- active-tool routing;
- validation profile;
- enabled, disabled, unavailable, or failed plugins and evidence producers;
- local capability notes and unresolved gaps.

The adapter may point at upstream contracts under `.agent-os/upstream/`, but it must not require agents to modify those upstream files for local operation.

## Install State

Each pinned installation should keep a concise target-owned install-state file, usually `.agent-os/adapter/install-state.md`.

The install state should record:

- upstream delivery mechanism;
- pinned upstream ref, commit, release tag, archive digest, or equivalent immutable identifier;
- upstream snapshot path;
- adapter path;
- whether upstream content is available, missing, partial, or intentionally unavailable;
- known adapter gaps and disabled capabilities;
- the local update procedure or the absence of one.

Install state is factual maintenance context. It should not store product decisions, architecture decisions, or reusable core guidance.

## Missing Or Unavailable Upstream Content

If `.agent-os/upstream/` or an expected upstream submodule/snapshot is missing, partial, or unreadable:

1. Read `.agent-os/adapter/install-state.md` if present.
2. Check the recorded delivery mechanism and pinned identifier.
3. Use only repository-supported restoration steps that are documented in the install state or normal repository docs.
4. If no restoration step is available or the task does not permit restoring the snapshot, report the upstream content as unavailable.
5. Continue with ordinary source reads and project checks only when the requested task can proceed without Agent OS guidance.

Agents should not silently substitute remote `HEAD`, copy content from another target repository, or edit `.agent-os/upstream/**` to repair a missing snapshot. A missing upstream snapshot is an installation state problem, not a reason to invent local core guidance.

## Updating A Pin

A pin update is explicit Agent OS maintenance. A target repository should:

1. Select the intended upstream Agent OS snapshot.
2. Update the delivery mechanism to that immutable snapshot.
3. Review upstream contract changes for adapter impact.
4. Update only target-owned adapter files when local routes, tools, validation, plugins, or unavailable-capability notes need to change.
5. Record the new pin and known gaps in install state.
6. Validate the installed bootloader route, adapter route, and any adapter-declared checks that the repository supports.

Do not treat a moving remote branch as the installed contract. The installed contract is the pinned snapshot recorded in the target repository.
