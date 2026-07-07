# Slice 3: Field Platform Pin Update If Needed

## Project

Field Platform reference installation:

```text
C:\Users\user\Documents\App
```

## Goal

Update the pinned Agent-OS submodule to the accepted upstream commit if Slice 2 shows the current pin is not the intended stable baseline.

Only do this if the pin consistency audit shows an update is needed.

## Branch

Suggested branch:

```text
agent-os-field-platform-pin-update
```

Use the repo's current branching conventions if they differ.

## Expected Changes

Possible files:

```text
.gitmodules
.agent-os/upstream gitlink
.agent-os/adapter/install-state.md
README.md
AGENTS.md
```

Patch README or AGENTS only if wording must change to stay accurate.

## Policy

- Pin to an immutable Agent-OS commit.
- Record the exact commit in install-state.
- Avoid implying the installed contract is a moving branch.
- If `.gitmodules` keeps a branch field, document that it is only a fetch convenience, not the installed contract.

## Validation

Run as much of the following as is available:

```text
git submodule status
git -C .agent-os/upstream rev-parse HEAD
git -C .agent-os/upstream status --short --branch
corepack pnpm check
corepack pnpm boundary:validate
corepack pnpm depcruise:active-source
corepack pnpm agent-os context manifest --json
corepack pnpm agent-os context evidence --json
```

If any command is unavailable or fails due to environment setup, report it clearly.

## Completion Report

Report back to the root coordination thread with:

- branch
- commit SHA, if committed
- changed files
- validation results
- exact Agent-OS commit now pinned
- whether `.gitmodules` has a branch field and what it means
- blockers or follow-up questions
