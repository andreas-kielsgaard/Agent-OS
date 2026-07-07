# Convivial Medicine Target Install Dry Run

Dry run date: 2026-07-07

Agent OS baseline reviewed: `5da7e90 Document pinned consumption contracts`

Target inspected read-only: `C:\Users\user\Documents\Code Projects\Convivial Medicine`

## Target Snapshot

Convivial Medicine is a Python 3.12 biomedical corpus constructor with a Typer CLI, a small FastAPI health surface, SQLAlchemy/Postgres persistence, Alembic migrations, optional MinIO/object-store configuration, deterministic fixture artifacts, and source-adapter boundaries for PubMed, PMC, and OpenAlex.

Important target surfaces observed:

| Surface | Evidence | Agent OS install relevance |
| --- | --- | --- |
| Project overview | `README.md` | Describes the product boundary, development commands, local services, API route, and fixture workflow. |
| Python package config | `pyproject.toml` | Declares `uv`, package metadata, console script `corpus`, Ruff, mypy, and pytest settings. |
| Active source | `src/convivial_medicine/` | Primary source root for CLI, API, adapters, domain, storage, and orchestration modules. |
| Tests | `tests/unit/`, `tests/integration/`, `tests/fixtures/` | Unit/integration coverage and committed source fixtures. |
| Migrations | `migrations/`, `alembic.ini` | Alembic schema authority for Postgres persistence. |
| Project docs | `docs/phase1-orientation.md`, `docs/source-boundaries.md`, `docs/phase1-fixture-workflow.md` | Human-readable source boundaries, acceptance workflow, and deferred work. |
| Local services | `docker-compose.yml`, `.env.example` | Postgres and MinIO development dependencies plus local environment defaults. |
| Generated/local artifacts | `.artifacts/`, `.coverage`, cache directories, `__pycache__/` | Generated evidence or local state; should not become source authority. |

The target already had an untracked `.artifacts/` directory before inspection. This dry run did not write to Convivial Medicine.

## Install-Mode Fit

Recommended mode: messy adoption leaning reference-quality.

Rationale:

- The repository has coherent source/docs/test structure and strong validation commands, so the adapter can be concrete rather than speculative.
- The repo also has generated artifact roots and runtime caches in the working tree, so the initial adapter should explicitly classify generated and ignored surfaces.
- Existing docs already own important phase boundaries. Agent OS should route to them rather than copying their decisions into reusable core.
- No existing `.agent-os/` install was observed during the dry run, so this would be a first local installation rather than an update.

## Adapter Sketch

Suggested target-owned adapter path: `.agent-os/adapter/`

Suggested upstream snapshot path: `.agent-os/upstream/`

Suggested root entry contract: `AGENTS.md`

```yaml
adapter:
  id: convivial-medicine-agent-os-adapter
  repository:
    name: Convivial Medicine
    root: .
    observedBranch: phase1-completion-audit

  installation:
    upstream:
      path: .agent-os/upstream/
      ownership: upstream-owned read-only snapshot
      pin: recorded in .agent-os/adapter/install-state.md
      unavailableBehavior: check install state; if not restorable, report Agent OS upstream guidance unavailable
    adapter:
      path: .agent-os/adapter/
      ownership: target-owned binding layer

  sourceGroups:
    - id: active-python-source
      paths:
        - src/convivial_medicine/
      role: maintained implementation source
    - id: tests
      paths:
        - tests/unit/
        - tests/integration/
        - tests/fixtures/
      role: verification and fixture evidence
    - id: migrations
      paths:
        - migrations/
        - alembic.ini
      role: database schema authority
    - id: project-docs
      paths:
        - README.md
        - docs/
      role: project-control and source-boundary documentation
    - id: local-service-config
      paths:
        - docker-compose.yml
        - .env.example
      role: local development service configuration

  sourcePolicy:
    activeSource:
      - src/convivial_medicine/
      - tests/
      - migrations/
      - manifests/
      - pyproject.toml
      - alembic.ini
      - docker-compose.yml
    generated:
      - .artifacts/
      - .coverage
      - .mypy_cache/
      - .pytest_cache/
      - .ruff_cache/
      - "**/__pycache__/"
    protected:
      - path: .agent-os/upstream/
        rule: read-only upstream Agent OS snapshot; update only through explicit pin maintenance
      - path: .agent-os/adapter/
        rule: edit only during explicit Agent OS install or adapter maintenance

  projectControl:
    map: .agent-os/adapter/project-setup-map.md
    routes:
      projectOverview: README.md
      phaseOrientation: docs/phase1-orientation.md
      sourceBoundaries: docs/source-boundaries.md
      fixtureWorkflow: docs/phase1-fixture-workflow.md
      schemaAuthority:
        - migrations/
        - src/convivial_medicine/storage/models.py
      packageAndTooling: pyproject.toml
      localServices:
        - docker-compose.yml
        - .env.example
      installState: .agent-os/adapter/install-state.md
      localToolMap: .agent-os/adapter/tool-map.md

  validation:
    profile: python-fastapi-data-pipeline
    commands:
      - uv run ruff check .
      - uv run ruff format --check .
      - uv run mypy src
      - uv run pytest
      - uv run corpus doctor
      - uv run corpus build seed
      - uv run corpus validate build
      - uv run corpus audit phase-one
```

## Active-Tool Support Table

| Logical tool ID | Suggested route | Expected evidence | State | Notes |
| --- | --- | --- | --- | --- |
| `verification` | `uv run ruff check .`, `uv run ruff format --check .`, `uv run mypy src`, `uv run pytest` | Lint, format, type, and test results | Supported | Declared directly in `README.md` and `pyproject.toml`. |
| `repository-health` | `uv run corpus doctor`; optionally `uv run corpus doctor --check-db` | Local configuration and optional DB connectivity | Supported, DB check optional | DB-dependent checks require local Postgres. |
| `fixture-workflow` | `uv run corpus build seed`, `uv run corpus validate build`, `uv run corpus export slice --output ...`, `uv run corpus audit phase-one` | Deterministic fixture build, validation, export, and audit evidence | Supported, writes generated artifacts | Should be routed as generated evidence because it writes `.artifacts/`. |
| `api-smoke` | `uv run uvicorn convivial_medicine.api.main:app --reload` plus `GET /health` | FastAPI app health evidence | Partially supported | Requires a running server; not a default install validation. |
| `database-migration` | `docker compose up -d postgres`, `uv run alembic upgrade head` | Schema migration evidence | Supported with services | Requires Docker and local Postgres. |
| `dependency-boundary` | None observed | Import or architecture-boundary evidence | Unavailable | Do not make dependency-cruiser or another graph tool mandatory. |
| `context-bundle` | Selected `rg`, source reads, and project docs | Bounded local context evidence | Manual fallback | Could become a project-local script later, but no route exists now. |
| `affected-surface` | Selected `rg`, `git diff --name-only`, test naming conventions | Likely affected source/tests | Manual fallback | No dedicated impact analyzer observed. |
| `test-relation` | Test paths and `pytest` selection by inspected modules | Related tests | Manual fallback | No dedicated test-selection tool observed. |

## Plugin And Evidence Candidates

Good candidate evidence producers:

- Python verification evidence: Ruff, mypy, pytest.
- CLI workflow evidence: `corpus build seed`, `corpus validate build`, `corpus audit phase-one`.
- Database evidence: Alembic migration status and optional Postgres-backed integration checks.
- Artifact evidence: build report and source snapshot manifests under `.artifacts/`.
- API smoke evidence: FastAPI `/health` when a server is intentionally started.

Suggested initial plugin states:

| Capability | State | Reason |
| --- | --- | --- |
| Python lint/type/test evidence | Enabled through adapter routes | Commands are first-class project checks. |
| Fixture workflow evidence | Enabled, generated-output aware | Supported by project docs but writes generated artifacts. |
| Database migration evidence | Disabled by default or enabled with service preconditions | Requires Docker/Postgres and may mutate local DB state. |
| Dependency-boundary graph | Unavailable | No compatible tool observed and the Agent OS contract says no graph tool is universal. |
| Live biomedical source fetching | Disabled by default | Requires explicit credentials and network opt-in. |
| Notebook/product UI tools | Unavailable | Explicitly outside current project boundary. |

## Template Fit

The Agent OS templates fit this target with no required baseline patch.

`install/templates/AGENTS.md` fits because it keeps the root entry small, routes first to `.agent-os/upstream/core/agent-os-bootloader.md`, then to `.agent-os/adapter/adapter.md`, and gives a clear missing-upstream fallback.

`install/templates/install-state.md` fits because Convivial Medicine needs to record:

- upstream delivery mechanism and immutable pin;
- snapshot availability;
- adapter path;
- known gaps such as unavailable dependency-boundary tooling;
- local update procedure;
- generated-evidence warnings for `.artifacts/`.

`install/templates/project-setup-map.md` fits because the target already has clear authority surfaces: `README.md`, `docs/phase1-orientation.md`, `docs/source-boundaries.md`, `docs/phase1-fixture-workflow.md`, `pyproject.toml`, migrations, and source/config files.

`install/templates/tool-map.md` fits because it supports partial tool availability and manual fallbacks. This is important for Convivial Medicine, where verification is strong but dependency-boundary and context-bundle tools are not dedicated commands.

## Contract Feedback

Reviewed Agent OS baseline files:

- `install/pinned-consumption.md`
- `install/README.md`
- `install/installation-modes.md`
- `install/templates/AGENTS.md`
- `install/templates/install-state.md`
- `install/templates/project-setup-map.md`
- `install/templates/tool-map.md`
- `adapters/adapter-contract.md`
- `plugins/plugin-contract.md`
- `plugins/evidence-producer-contract.md`

Consistency result: the pinned-consumption contract is internally consistent across install, adapter, and plugin surfaces.

Specific checks:

| Contract concern | Dry-run result |
| --- | --- |
| `.agent-os/upstream/` ownership | Consistently defined as upstream-owned and read-only from the target repository. |
| `.agent-os/adapter/` ownership | Consistently defined as target-owned binding for local paths, validation, tools, plugins, gaps, and install state. |
| Install state | Consistently framed as concise factual maintenance context, not product or architecture authority. |
| Missing upstream behavior | Consistently routes to install state and forbids silent substitution from remote `HEAD`, another target repository, or local upstream edits. |
| Protected upstream ownership | Reinforced in install docs, adapter contract, plugin contract, evidence contract, and root `AGENTS.md` template. |
| Active tools | Correctly described as bounded evidence rather than semantic authority. |
| Plugin/evidence enablement | Correctly owned by the target adapter, not upstream plugin files. |

No contract patch is required before using this baseline for a Convivial Medicine install.

Narrow future improvements to consider, not blockers:

- Add one install-guide example for generated artifact roots such as `.artifacts/` so adapters consistently classify deterministic local outputs as evidence, not source authority.
- Add one install-guide sentence that install validation should avoid running commands that mutate target generated surfaces unless the user explicitly requests a real install or evidence run. This matters for fixture workflows that write `.artifacts/`.
- Consider a short Python/FastAPI/data-pipeline adapter example later, but keep it illustrative rather than mandatory.

## Unsupported Capabilities

The adapter should explicitly mark these unsupported or disabled unless a future project decision changes them:

- Dependency graph or import-boundary evidence from dependency-cruiser or similar tooling.
- Live PubMed, PMC, or OpenAlex source calls without explicit credentials and network opt-in.
- Database-backed checks when Postgres is not running.
- MinIO/object-store evidence unless the service is intentionally started and configured.
- Product UI, notebook, embedding, vector database, and graph database workflows, which project docs currently defer or exclude.
- Any target-specific plugin enablement that would require editing `.agent-os/upstream/**`.

## Readiness Recommendation

Recommendation: ready for a read-only review sign-off of the Agent OS contract baseline, and ready for a future explicit Convivial Medicine install if that repo owner wants one.

The Convivial Medicine dry run supports the current pinned-consumption contract. The baseline cleanly handles a non-Field Python/FastAPI/data-pipeline target with generated artifacts, optional services, fixture workflows, and partial tool availability. The adapter should be conservative, generated-output aware, and explicit about unavailable dependency-boundary tooling.

Do not proceed from this report into a Convivial Medicine write/install unless a separate slice explicitly authorizes edits to that repository.

## Validation Notes

Agent OS preflight:

- `git status --short --branch`: `## main...origin/main [ahead 1]`
- `git log --oneline -5`: confirmed `5da7e90 Document pinned consumption contracts` at HEAD.

Convivial Medicine pre-inspection:

- `git status --short --branch`: `## phase1-completion-audit...origin/phase1-completion-audit` plus pre-existing `?? .artifacts/`.

Final validation:

- Agent OS `git status --short --branch`: `## main...origin/main [ahead 1]` plus `?? docs/target-install-dry-runs/`.
- Agent OS `git diff --check`: passed with no output.
- Convivial Medicine `git status --short --branch`: unchanged from pre-inspection, `## phase1-completion-audit...origin/phase1-completion-audit` plus pre-existing `?? .artifacts/`.

Read-only verification: Convivial Medicine had no writes from this dry run. The only observed target working-tree item, `?? .artifacts/`, was present before inspection and remained the only item after inspection.
