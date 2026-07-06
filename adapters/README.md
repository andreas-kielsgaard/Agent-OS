# Adapters

Adapters bind reusable Agent OS core guidance to a specific repository. They are the project-local layer that tells an installed Agent OS where the repository keeps source, generated output, archive material, protected surfaces, project-control routing, active tools, validation commands, and optional evidence producers.

An adapter is repository-specific configuration, not reusable core meaning. It lets an implementation agent install Agent OS into a project without hard-coding that project's paths, decisions, commands, tools, or plugin choices into core.

## Core Boundary

Core does not know:

- target repository paths;
- project decisions or architecture authority;
- actual command names or package scripts;
- which evidence producers are installed, enabled, or compatible.

Adapters bind those project-local facts into an installation. If an adapter does not declare a route, tool, validation command, or plugin, core should treat that capability as absent rather than inventing one.

## Adapter Responsibilities

An adapter declares:

- repository identity;
- source groups and their intended use;
- source policy, including active source, generated surfaces, archive surfaces, and protected surfaces;
- project-control routing into local decisions and authority files;
- adapter-declared active tools;
- validation profile for the target repository;
- enabled, disabled, unavailable, or failed plugins and evidence producers;
- capability notes and unavailable capability notes.

See [adapter-contract.md](adapter-contract.md) for the first reusable contract foundation.

## Installation Role

The adapter is installed into a target repository alongside local entry files such as `AGENTS.md`, a project-control route map, an active tool map, and install state. In the default pinned layout, reusable Agent OS content is consumed from `.agent-os/upstream/` as read-only upstream-owned content, while target-specific adapter files live under `.agent-os/adapter/`.

Those installed files route agents to project-local authority and evidence without moving project-specific meaning into reusable core or editing consumed upstream files.

Field Platform is useful reference material, but its app roots, package layout, generated paths, command names, dependency-boundary tooling, validation scripts, and project decisions must stay Field Platform-specific unless a later extraction task explicitly generalizes them.
