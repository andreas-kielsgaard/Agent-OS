# Agent-OS Pinned Consumption Stabilization

## Purpose

This proposal sets up a plain recursive coordination flow for stabilizing Field Platform's pinned consumption of reusable Agent OS from the Agent-OS repository.

This is intentionally not an Agent-OS contract redesign and not a new orchestration framework inside either repository. It is a coordination packet for a root Codex thread to run focused workers in sequence, review each result, and continue only after acceptance.

## Goal

Bring Field Platform into a stable state where it consumes reusable Agent OS from the Agent-OS repository as a pinned upstream snapshot, while keeping Field Platform's adapter, project-control routing, active tools, validation profile, and project decisions local.

The current task is stabilization, verification, cleanup, and deciding the final pin-update path. The pinned model does not need to be redesigned from scratch.

## Repositories

Agent-OS reusable repository:

```text
C:\Users\user\Documents\Code Projects\Agent-OS
```

Field Platform reference installation:

```text
C:\Users\user\Documents\App
```

## Current State Summary

Agent-OS now has pinned-consumption documentation on `main`. The install docs define a default layout where upstream-owned content lives under `.agent-os/upstream/` and target-owned adapter material lives under `.agent-os/adapter/`.

Field Platform already has a pinned `.agent-os` install on `main`. Its root `AGENTS.md` routes agents to `.agent-os/upstream/core/agent-os-bootloader.md`, then to `.agent-os/adapter/adapter.md`, and marks `.agent-os/upstream/**` as read-only upstream guidance.

The highest-priority concern is that Field Platform's submodule config may still point at a temporary branch named `codex/agent-os-pinned-consumption-contract`, while the install-state records a specific pinned commit and says not to track remote `HEAD` implicitly.

## Non-Goals

Do not include:

- extracting `tools/agent-tools` into Agent-OS
- turning Agent-OS into an npm/package runtime
- creating executable adapter schemas
- making dependency-cruiser mandatory
- installing Agent OS into Convivial Medicine
- adopting Agent OS into Job App
- changing Field Platform product architecture or MVP scope
- broad cleanup of `Archive/**`
- redesigning the Agent-OS pinned-consumption contract

## Sequenced Slices

1. [Agent-OS Baseline Publication Review](./01-agent-os-baseline-publication-review.md)
2. [Field Platform Pin Consistency Audit](./02-field-platform-pin-consistency-audit.md)
3. [Field Platform Pin Update If Needed](./03-field-platform-pin-update-if-needed.md)
4. [Legacy Reference Sweep](./04-legacy-reference-sweep.md)
5. [Pinned Consumption Acceptance Report](./05-pinned-consumption-acceptance-report.md)

The default coordination model is serial. Start Slice 1 first, review completion, re-prompt if needed, then continue to Slice 2.

## Coordination Rule

The root coordination thread should not implement the slices directly. It should create focused worker threads, require each worker to report back, review the work, then either re-prompt or continue to the next slice.

Do not mix this plain setup with existing orchestration records or machinery in either repository. Treat these files as the proposal and coordination source for this stabilization run.

## Completion Definition

The effort is complete when Field Platform has an acceptance report confirming:

- the Agent-OS upstream commit is pinned intentionally
- local adapter files are present
- root `AGENTS.md` routing is verified
- project-control map is verified
- active tool map is verified
- old `Agent OS/` route is retired
- `.agent-os/upstream` is protected from local edits
- context tooling excludes upstream from active source
- Field Platform validation commands passed or clearly documented as unavailable
- known remaining gaps are recorded
