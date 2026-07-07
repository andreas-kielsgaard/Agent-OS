# Agent OS Baseline Publication Review

Review date: 2026-07-07

Branch: `codex/agent-os-baseline-publication-review`

Reviewed baseline: `9e7223f8cf91cf1e145fb8120af788f28647ebc0` (`origin/main`, `Document Convivial Medicine dry-run evidence`)

## Conclusion

Agent OS `main` is ready to be treated as the upstream source for pinned target installs.

Recommended next target pin:

```text
9e7223f8cf91cf1e145fb8120af788f28647ebc0
```

This commit includes the pinned-consumption contracts plus the Convivial Medicine dry-run evidence that checks the baseline against a non-Field Python/FastAPI/data-pipeline target.

## Review Scope

Reviewed files:

- `install/pinned-consumption.md`
- `install/templates/install-state.md`
- `install/README.md`
- `adapters/adapter-contract.md`
- `plugins/plugin-contract.md`
- `plugins/evidence-producer-contract.md`
- `docs/target-install-dry-runs/convivial-medicine.md`
- `docs/field-platform-reference.md`

This review stayed limited to baseline publication readiness. It did not redesign the pinned-consumption contract, extract Field Platform tooling, install Agent OS into target repositories, or change Field Platform state.

## Findings

The pinned-consumption, install, adapter, plugin, and evidence-producer docs are internally consistent.

Consistent points across the reviewed docs:

- `.agent-os/upstream/` is upstream-owned pinned Agent OS content and read-only from the target repository.
- `.agent-os/adapter/` is target-owned and carries repository paths, project-control routing, active tools, validation, plugin enablement, capability notes, and install state.
- Install state records the immutable upstream pin and factual maintenance context, not product decisions or reusable core guidance.
- Missing upstream content should be handled through install state and repository-supported restoration steps; agents should not substitute remote `HEAD`, another target repository copy, or local upstream edits.
- Plugin and evidence-producer enablement is adapter-owned; reusable upstream plugin files do not make a capability enabled for every target.
- Active tools and evidence producers provide bounded evidence, not semantic authority.

The Convivial Medicine dry-run supports the baseline. It verifies that the same pinned model can describe a non-Field target with Python/FastAPI/data-pipeline tooling, generated artifacts, optional services, and unavailable dependency-boundary tooling without making Field Platform assumptions universal.

`docs/field-platform-reference.md` remains accurate. It identifies Field Platform as the current reference installation while explicitly saying it is not a universal template and listing what must stay Field Platform-specific. The Convivial Medicine evidence is a dry run, not a second completed reference installation, so no wording change is required there.

No reviewed documentation says Agent OS publication is still pending. No contract patch was required.

## Out Of Scope

Intentionally out of scope for this review:

- redesigning the pinned-consumption contract;
- proceeding to Field Platform pin consistency or install-state work;
- updating any target repository pin;
- installing Agent OS into Convivial Medicine or another target repository;
- extracting `tools/agent-tools`, dependency-cruiser configuration, package scripts, or other Field Platform tooling into Agent OS;
- turning Agent OS into an npm package or package runtime;
- changing archives, fixtures, or historical migration evidence.

## Validation Notes

Validation should be run after this review file is committed or prepared for review:

- `git status`
- `git diff --check origin/main...HEAD`
- `git diff --name-status origin/main...HEAD`

No automated Markdown tooling was found in this repository during this review.
