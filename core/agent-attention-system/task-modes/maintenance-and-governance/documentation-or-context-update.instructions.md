# Mode: Documentation Or Context Update

## Orientation Cues

- local agent entry files
- `core/agent-attention-system/agent-attention-system-usage.md` when documentation changes source-of-truth structure, instruction ownership, or durable authority
- adapter-declared project-control routing for relevant human-owned project decisions when documentation changes mature human-owned context
- The relevant core, adapter, or project instruction file being changed.
- Final response notes for scoped compromises or unresolved authority.

## Evidence Cues


- Consider searching for duplicate or conflicting instructions.
- Consider searching references to renamed docs or modes.

## Implementation Cues

- Consider updating the smallest document that owns the relevant memory.
- Prefer one routed source for a rule instead of duplicating it across many files.
- Keep agent-critical behavior in agent-facing instruction surfaces; keep README-style explanation human-facing.
- Move detailed procedures out of local agent entry files into mode files.
- Keep local agent entry files as routing and behavioral contract.
- If a correction has happened more than once, encode it as a mode instruction, checklist item, script/check, lint rule, or concise guidance.
- Mark provisional migration docs honestly when they are not yet active.

## Cross-Application Impact Cues

- Does this change routing for future agents?
- Does it conflict with other instruction files?
- Does it create or retire a control surface?
- Do tool adapters need to point somewhere new?

## Documentation Cues

- Consider using structural maintenance if doc structure, instruction ownership, or durable authority changes.
- Consider updating relevant adapter-surfaced project decisions if documentation changes mature platform/component layout or boundary expectations.
- Consider updating local agent entry files if routing or instruction hierarchy changes.
- Consider updating mode files if task behavior changes.
- Consider updating relevant durable memory if documentation policy changes.

## Regression Cues

- Conflicting instructions.
- Rules duplicated across many files.
- Prose-only instructions where a check/script should exist.
- Active instructions pointing to empty or retired files.
- Missing migration status.

## Structural Maintenance Clues

- Consider entering structural maintenance when documentation changes source-of-truth ownership, audience, authority, tool contracts, generated/manual boundaries, or maintenance paths.

## Report Cues

```text
Primary mode: documentation or context update
Docs changed:
Reason:
Instruction moved/added/removed:
Affected modes:
Generated maps refreshed:
Potential conflicts removed:
Checks run:
```
