# ARCHITECTURE.md Template

Use this template to create the high-level codemap for the repository.

## Bird's-Eye View

- Problem: [What problem the project solves and for whom]
- System shape: [Main runtime or workflow at a high level]
- Boundaries: [Important external systems, entrypoints, or interfaces]
- Primary anchors:
  - `path/to/file`
  - `[entrypoint/type/module name]`

## Code Map

### `[module-or-directory]`

- Responsibility: [What this area owns]
- Collaborators: [What it depends on or feeds into]
- Key names: `[directory]`, `[module]`, `[type]`, `[entrypoint file]`
- Primary anchors:
  - `path/to/file`
  - `[type/function/package name]`

### `[module-or-directory]`

- Responsibility: [What this area owns]
- Collaborators: [What it depends on or feeds into]
- Key names: `[directory]`, `[module]`, `[type]`, `[entrypoint file]`
- Primary anchors:
  - `path/to/file`
  - `[type/function/package name]`

## Architectural Invariants

### `[Invariant name]`

- Statement: [Stable rule, boundary, or deliberate absence]
- Why it matters: [Why contributors should preserve it]
- Primary anchors:
  - `path/to/file`
  - `[symbol or config key]`

Add this section only when the invariant is both important and supported by evidence.

## Cross-Cutting Concerns

- `[Concern]`: [Shared mechanism or constraint spanning multiple modules]
- Primary anchors:
  - `path/to/file`
  - `[symbol or config section]`

Include this section only for concerns that materially affect changes across the repository.

## Placement

Store this file at `ARCHITECTURE.md` next to `AGENTS.md`.

## Exclusions

Do not include:
- Exhaustive file-by-file walkthroughs
- Low-level implementation details that change often
- Direct code links as the primary navigation mechanism
- Workstation-specific absolute filesystem paths
- One-off facts that do not help a contributor answer "where should I change code?"
