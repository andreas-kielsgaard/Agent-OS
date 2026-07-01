# Core

Agent OS core is the reusable agent operating guidance that can be installed into a repository before any project-specific adapter is written.

Core includes:

- the bootloader and context-loading hierarchy;
- task modes for classifying and running work;
- structural behaviors for durable maintenance choices;
- reasoning lenses for lightweight analysis;
- skills and execution guidance for repeatable agent workflows;
- evidence-vs-authority rules that keep generated output and tool output in their proper place.

For now, task modes, behaviors, and lenses are treated as core Agent OS material, not pluggable extension points. A future contract may separate them differently, but this foundation should preserve them as shared operating-system guidance until that decision is made explicitly.

Core should remain adapter-neutral. It may define how agents ask for context and how they treat evidence, but it should not embed a specific repository's source roots, domain terms, package manager, validation scripts, architecture decisions, or product intent.

## Initial Subareas

- `agent-attention-system/`: placeholder home for the reusable attention-system maps, task-mode guidance, behaviors, lenses, and skills once they are extracted intentionally.
