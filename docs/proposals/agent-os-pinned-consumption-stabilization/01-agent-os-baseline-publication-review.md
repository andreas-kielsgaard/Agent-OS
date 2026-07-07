# Slice 1: Agent-OS Baseline Publication Review

## Project

Agent-OS reusable repository:

```text
C:\Users\user\Documents\Code Projects\Agent-OS
```

## Goal

Review whether Agent-OS `main` is now the intended stable baseline for pinned target consumption, and patch only stale or misleading documentation discovered by that review.

This is a small review and cleanup slice. It should not redesign contracts.

## Branch

Suggested branch:

```text
agent-os-baseline-publication-review
```

Use the repo's current branching conventions if they differ.

## Inspect

```text
install/pinned-consumption.md
install/templates/install-state.md
install/README.md
adapters/adapter-contract.md
plugins/plugin-contract.md
plugins/evidence-producer-contract.md
docs/target-install-dry-runs/convivial-medicine.md
docs/field-platform-reference.md
```

## Review Questions

1. Is Agent-OS `main` ready to be treated as the upstream source for pinned target installs?
2. Which Agent-OS commit should target repos pin next?
3. Are pinned-consumption, adapter, install, and plugin docs internally consistent?
4. Does the Convivial Medicine dry-run support the baseline?
5. Are any docs stale, especially references implying Field Platform is still the only reference or that publication is pending?
6. What remains intentionally out of scope?

## Expected Output

Create:

```text
docs/baseline-publication-review.md
```

Patch docs only if the review finds concrete stale wording. Do not redesign contracts.

## Validation

Run:

```text
git status
git diff --check origin/main...HEAD
git diff --name-status origin/main...HEAD
```

If Markdown tooling exists, run it. Otherwise state that no automated Markdown validation exists.

## Completion Report

Report back to the root coordination thread with:

- branch
- commit SHA, if committed
- changed files
- validation results
- conclusion on whether Agent-OS `main` is the recommended pin source
- blockers or follow-up questions

After this slice is accepted, the next slice is Field Platform Pin Consistency Audit.
