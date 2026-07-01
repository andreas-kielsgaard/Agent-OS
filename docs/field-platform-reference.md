# Field Platform Reference Installation

Field Platform is the current reference installation for Agent OS. It demonstrates a working local setup, not a universal template.

## What Field Platform Demonstrates

- bootloader-driven task and context orientation;
- an attention system with task modes, behaviors, lenses, skills, and tool routing;
- project-control routing that keeps Agent OS guidance separate from human-owned project decisions;
- adapter-neutral command wording, JSON envelopes, and schema-registry surfaces for context tooling;
- a repository adapter that declares source groups, source policy, generated/archive handling, capabilities, and enabled evidence producers;
- `dependency-cruiser` as a toggleable evidence-producer candidate;
- deterministic evidence tools that support agent judgment without replacing it.

## What Must Stay Field Platform-Specific

- app source roots such as `apps/web/app`, `apps/web/src`, and `tools/agent-tools/src`;
- Field Platform domain vocabulary, product intent, and architecture decisions;
- human-owned project decisions under repository-root `project-decisions/`;
- pnpm, React, TypeScript, Drizzle, Biome, monorepo, and web-app assumptions;
- package scripts, command composition, dependency versions, and validation profile;
- `dependency-cruiser.config.cjs`, dependency boundary rules, and active-source roots;
- generated output, report, coverage, build, and archive policies tied to Field Platform;
- local command names unless a later reusable contract adopts them explicitly.

## Target Implications

- **Convivial Medicine**: Python, FastAPI, and data-pipeline portability test for adapter and plugin assumptions.
- **Personal Finance Orchestrator**: greenfield install test for implementation-agent instructions.
- **Job App**: messy/adoption-mode test after the first two targets; lower priority because adoption complexity is secondary for the initial reusable foundation.

The reusable repository should learn from Field Platform while resisting the urge to turn Field Platform into the template. Core should stay reusable, adapters should carry project bindings, plugins should remain evidence-only, and installation should be explicit about unsupported or unavailable capabilities.
