## Start of turn

1. Re-evaluate primary and secondary task modes internally; state them only when useful for broad, ambiguous, or high-impact work.

2. Re-evaluate relevant behaviors internally; state them only when useful for broad, ambiguous, or high-impact work.

3. Re-evaluate relevant lenses internally; state them only when useful for broad, ambiguous, or high-impact work.

## Throughout task execution

- Leverage provided tools when they can achieve an action.

- Leverage provided skills when they correspond to an action.

- Use human-maintained maps, selected source reads, `rg`, adapter-declared active tools, plugin/evidence-producer outputs, and standard project checks to orient in the workspace.

- Keep examples and assumptions stack-aware. TypeScript, Python, greenfield projects, and messy adoption projects may expose different source groups, validation profiles, generated surfaces, and authority surfaces.

- Treat deterministic evidence as bounded. A successful tool result can support reasoning, but it does not decide ownership, meaning, architecture quality, or correctness.

## Reporting And Logging

- Keep mode, behavior, and lens selection as working context during normal tasks.
- Do not create per-task attention logs by default.
- Do not create handoff or report files by default.
- Use a compact final summary in chat for normal task completion: changed surfaces, checks run, skipped checks or failures, and important unresolved risk.
- Create a persistent report, handoff, or log only when the user explicitly asks for one or the task genuinely requires a durable artifact.
- Treat task-mode report cues as optional prompts for the final summary, not as a requirement to fill every field or write a file.

# Re-evaluation cues

Especially consider revisiting mode, behavior, and lens selection when:

- the implementation reveals a different root cause
- a local change starts touching shared components, public interfaces, schemas, accessors, permissions, state, mocks, fixtures, naming, packaging, or deployment surfaces
- a task grows from a narrow edit into cross-surface work
- review-before-commit reveals missing affected surfaces
- evidence producers are absent, disabled, unavailable, failed, or contradict source/config inspection
- the work reveals a decision about placement, ownership, boundary, lifecycle, naming, reuse, duplication, contract, audience, maintenance path, or authority of a durable maintained element
