# Root Coordination Re-Ingestion

## Purpose

Use this file to refresh the root coordination thread after compaction, a long worker cycle, or any point where the setup risks drifting.

This is a plain coordination setup. Do not mix it with existing orchestration records or startup machinery in Agent-OS or Field Platform.

## Root Objective

Coordinate the Agent-OS pinned consumption stabilization effort across:

```text
C:\Users\user\Documents\Code Projects\Agent-OS
C:\Users\user\Documents\App
```

The root should create focused worker threads, review their completion reports, re-prompt when needed, and proceed through the proposal slices in order.

## Proposal Files

```text
docs/proposals/agent-os-pinned-consumption-stabilization/overview.md
docs/proposals/agent-os-pinned-consumption-stabilization/01-agent-os-baseline-publication-review.md
docs/proposals/agent-os-pinned-consumption-stabilization/02-field-platform-pin-consistency-audit.md
docs/proposals/agent-os-pinned-consumption-stabilization/03-field-platform-pin-update-if-needed.md
docs/proposals/agent-os-pinned-consumption-stabilization/04-legacy-reference-sweep.md
docs/proposals/agent-os-pinned-consumption-stabilization/05-pinned-consumption-acceptance-report.md
```

## Serial Protocol

1. Read the proposal overview and current slice file.
2. Create a focused worker thread for the current slice.
3. Include the root thread id in the worker prompt so the worker can report back.
4. Require the worker to report summary, files changed, tests or validation, branch, commit if any, blockers, and review notes.
5. Review the worker result before proceeding.
6. If unacceptable, re-prompt that worker or create a correction worker with the same report-back instruction.
7. If acceptable, continue to the next slice.

Do not launch later slices before their prerequisite conclusions are accepted. In particular, do not run the Field Platform pin update unless Slice 2 concludes that an update is needed.

## Parallelism Reflection

The default execution model remains serial unless the user explicitly authorizes parallel workers. This task has a dependency chain around the pin decision:

- Slice 1 determines whether Agent-OS `main` is the intended baseline.
- Slice 2 uses that accepted baseline to audit Field Platform's installed pin.
- Slice 3 is conditional on Slice 2.
- Slice 5 should remain last because it is the stabilization marker.

Potential future parallelism is mostly useful for read-only inspection and preparation, not for accepting or changing shared truth.

Potentially safe future parallel tasks:

- read-only Field Platform reconnaissance while Slice 1 is underway, clearly marked preliminary
- preparing Slice 2 or Slice 4 worker prompts while the current worker runs
- running an independent review helper after a worker reports completion
- preparing the acceptance-report outline without filling final conclusions

Tasks that should stay serial:

- deciding the recommended Agent-OS pin source
- deciding whether the Field Platform pin is consistent
- updating the submodule pin
- changing `.gitmodules` policy or install-state wording
- accepting slice completion
- writing the final acceptance report

Use this rule if parallelism is later enabled: parallelize evidence gathering and prompt preparation; serialize decisions and edits that establish repository truth.

## Reasoning Level Guidance

Use the smallest reasoning level that is reliable for the task. The current root coordination thread should use high reasoning, per user instruction.

Recommended levels for this stabilization effort:

- Root coordination and sequencing: high.
- Root acceptance review: high.
- Slice 1 Agent-OS baseline publication review: high when deciding the recommended pin source; medium is acceptable for purely mechanical doc cleanup after the decision is clear.
- Slice 2 Field Platform pin consistency audit: high, because submodule state, install-state records, and docs must agree exactly.
- Slice 3 Field Platform pin update: high when deciding or changing the installed pin; medium only for a narrowly specified mechanical follow-up after the audit has already accepted the target commit.
- Slice 4 Legacy reference sweep: medium for search and classification; high if many hits are ambiguous between active guidance and historical evidence.
- Slice 5 Acceptance report: medium for drafting from accepted facts; high for final root acceptance.
- Independent review helpers: high for pin/submodule decisions; medium for doc-only or search-only checks.
- Validation-only command runs: low or medium, depending on whether interpretation of failures is needed.
- Documentation-only corrections: low or medium unless they affect install policy or agent routing.

Avoid xhigh by default. Reserve it for a serious contradiction or high-value ambiguity, such as a pinned commit not being reachable from the expected Agent-OS baseline, `.gitmodules` and install-state implying different ownership models, or validation failures whose cause spans both repositories.

## Slice Order

1. Agent-OS Baseline Publication Review.
2. Field Platform Pin Consistency Audit.
3. Field Platform Pin Update If Needed.
4. Legacy Reference Sweep.
5. Pinned Consumption Acceptance Report.

## Review Rules

Review with a code-review posture:

- findings first
- severity ordered
- specific file and line references where applicable
- brief summary only after findings

Check that the worker did not:

- redesign the Agent-OS contract
- broaden scope into unrelated Field Platform product work
- churn archive or migration evidence unnecessarily
- treat moving branch state as the installed pin
- imply `.agent-os/upstream` is locally editable Field Platform guidance
- skip validation without explaining why

## Recovery After Compaction

After compaction:

1. Read this file.
2. Read `overview.md`.
3. Read the current active slice file.
4. Inspect recent worker reports and git status in the relevant repo.
5. Continue from the latest reviewed and accepted slice.
