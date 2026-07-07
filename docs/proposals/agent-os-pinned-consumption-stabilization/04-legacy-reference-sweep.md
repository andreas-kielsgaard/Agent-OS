# Slice 4: Legacy Reference Sweep

## Project

Field Platform reference installation:

```text
C:\Users\user\Documents\App
```

## Goal

Find stale active references to the retired `Agent OS/` path or old migration-era assumptions.

Patch only active stale references. Do not churn archive, fixture, or migration evidence unless it can mislead active agents.

## Branch

Suggested branch:

```text
agent-os-field-platform-legacy-reference-sweep
```

Use the repo's current branching conventions if they differ.

## Search Terms

```text
Agent OS/
Agent OS\
agent-os-installation-state
agent-os-reusable-extraction-handoff
project-control-files
tool-map.md
.agent-os/upstream
.agent-os/adapter
```

## Classification

Classify hits as:

- active stale reference - must fix
- historical archive reference - leave alone
- test fixture or reference evidence - leave if intentional
- migration evidence - leave if explicitly marked non-active

## Validation

Run as much of the following as is available:

```text
corepack pnpm check
corepack pnpm boundary:validate
corepack pnpm agent-os context manifest --json
git diff --check origin/main...HEAD
```

If any command is unavailable or fails due to environment setup, report it clearly.

## Completion Report

Report back to the root coordination thread with:

- branch
- commit SHA, if committed
- changed files
- validation results
- search terms used
- stale active references fixed
- references intentionally left alone and why
- blockers or follow-up questions
