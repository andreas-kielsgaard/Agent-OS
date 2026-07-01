# Adapters

Adapters bind reusable Agent OS guidance to a specific repository. They describe where the project keeps source, generated output, archive material, project-control files, local commands, and optional evidence integrations.

An adapter is repository-specific configuration, not core Agent OS meaning. It should let an implementation agent install Agent OS into a project without hard-coding that project's assumptions into core.

Adapters should cover:

- source groups and their intended use;
- source policy, including active source, generated surfaces, archive surfaces, and protected surfaces;
- repository capabilities and local command availability;
- enabled plugins and evidence producers;
- project-control routing into local decisions and authority files;
- validation profile for the target repository.

## Shape Sketch

This is a sketch, not a final schema:

```text
adapter:
  id: project-id
  repo:
    name: Project Name
    root: .
  sourceGroups:
    - id: app-source
      paths:
        - src/
      role: active-source
  sourcePolicy:
    generated:
      - build/
      - coverage/
    archive:
      - Archive/
    protected:
      - Agent OS/
  capabilities:
    packageManager: detected-or-none
    languages:
      - detected-language
  evidenceProducers:
    dependencyCruiser:
      enabled: false
      reason: optional-plugin-not-configured
  projectControl:
    map: Agent OS/project-control-files/project-setup-map.md
  validation:
    commands:
      - command-name-or-shell-command
```

The final adapter contract should be defined before multiple project adapters are added. Field Platform's adapter is useful reference material, but its app roots, package layout, generated paths, and validation scripts should not become defaults.
