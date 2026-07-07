# Slice 2: Field Platform Pin Consistency Audit

## Project

Field Platform reference installation:

```text
C:\Users\user\Documents\App
```

## Goal

Verify that Field Platform's pinned submodule state, install-state file, `.gitmodules`, and root docs agree.

This is the highest-priority Field Platform stabilization question.

## Branch

Suggested branch:

```text
agent-os-field-platform-pin-consistency-audit
```

Use the repo's current branching conventions if they differ.

## Inspect

```text
.gitmodules
AGENTS.md
README.md
.agent-os/adapter/install-state.md
.agent-os/adapter/adapter.md
.agent-os/adapter/project-setup-map.md
.agent-os/adapter/tool-map.md
tools/agent-tools/src/context/adapters/field-platform-adapter-config.mjs
```

Also inspect:

```text
git submodule status
```

## Review Questions

1. Does `.gitmodules` point to an acceptable branch, or should it use `main` or no branch?
2. Does install-state pin the intended Agent-OS commit?
3. Does the pinned commit exist on Agent-OS `main`?
4. Does install-state still say main publication is pending when that is no longer true?
5. Does `AGENTS.md` point only to the pinned upstream bootloader and local adapter?
6. Does `README.md` match the actual installed layout?
7. Does context tooling exclude `.agent-os/upstream` from active Field source?
8. Are local tools still routed through `.agent-os/adapter/tool-map.md`?

## Expected Output

Create:

```text
.agent-os/adapter/project-control/pin-consistency-audit.md
```

If obvious stale text exists, patch it. For example, if install-state still says normal Agent OS `origin/main` publication remains pending after Agent-OS `main` is the intended baseline, update it.

## Validation

Run as much of the following as is available:

```text
git submodule status
corepack pnpm check
corepack pnpm boundary:validate
corepack pnpm depcruise:active-source
corepack pnpm agent-os context manifest --json
corepack pnpm agent-os context evidence --json
git diff --check origin/main...HEAD
```

If any command is unavailable or fails due to environment setup, report it clearly.

## Completion Report

Report back to the root coordination thread with:

- branch
- commit SHA, if committed
- changed files
- validation results
- pin consistency conclusion
- whether Slice 3 is needed
- blockers or follow-up questions
