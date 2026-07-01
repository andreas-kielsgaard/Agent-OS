# Installation Modes

Installation mode helps an implementation agent choose how conservative the first adapter should be. A repository can have traits from more than one mode; pick the mode that best describes the risk.

## Greenfield

Use this when Agent OS is installed before much project structure exists.

Priorities:

- keep the adapter small;
- identify current source roots without inventing future architecture;
- mark unknown project-control routes explicitly;
- define a minimal validation profile from commands that already work;
- leave unsupported tools and plugins disabled or unavailable.

Good output is an honest thin adapter that can grow as the project creates real source, policies, and checks.

## Reference Installation

Use this when an existing working Agent OS installation is source context for a new repository.

Priorities:

- extract reusable contract shape, not reference project decisions;
- rename or replace all reference-specific paths, commands, validation steps, and product terms;
- choose only plugins and active tools the target repo can support;
- create new local project-control routes instead of copying reference project-control files;
- validate the adapter against the target repo, not the reference repo.

Good output is a target-local installation that learned from the reference without becoming a clone of it.

## Messy Adoption

Use this when the target repo has mixed history, unclear ownership, generated clutter, partial conventions, or competing docs.

Priorities:

- identify active source, generated surfaces, archive surfaces, and protected surfaces first;
- route to existing authority surfaces conservatively;
- record unresolved authority conflicts instead of deciding them inside Agent OS;
- start with basic validation and repository-health evidence before optional plugins;
- report unsupported capabilities and missing decisions plainly.

Good output is a conservative adapter that reduces confusion without pretending the repository is cleaner than it is.
