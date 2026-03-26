# ARCHITECTURE.md Template

Use this template to create the high-level codemap for the repository.

## Bird's-Eye View

- Problem: [What problem the project solves and for whom]
- System shape: [Main runtime or workflow at a high level]
- Boundaries: [Important external systems, entrypoints, or interfaces]
- Evidence:
  - `path/to/file:line`
  - `path/to/another-file:line`

## Code Map

### `[module-or-directory]`

- Responsibility: [What this area owns]
- Collaborators: [What it depends on or feeds into]
- Key names: `[directory]`, `[module]`, `[type]`, `[entrypoint file]`
- Evidence:
  - `path/to/file:line`
  - `path/to/another-file:line`

### `[module-or-directory]`

- Responsibility: [What this area owns]
- Collaborators: [What it depends on or feeds into]
- Key names: `[directory]`, `[module]`, `[type]`, `[entrypoint file]`
- Evidence:
  - `path/to/file:line`
  - `path/to/another-file:line`

## Architectural Invariants

### `[Invariant name]`

- Statement: [Stable rule, boundary, or deliberate absence]
- Why it matters: [Why contributors should preserve it]
- Evidence:
  - `path/to/file:line`
  - `path/to/another-file:line`

Add this section only when the invariant is both important and supported by evidence.

## Cross-Cutting Concerns

- `[Concern]`: [Shared mechanism or constraint spanning multiple modules]
- Evidence:
  - `path/to/file:line`
  - `path/to/another-file:line`

Include this section only for concerns that materially affect changes across the repository.

## Placement

Store this file at `ARCHITECTURE.md` next to `AGENTS.md`.

## Reference Style

- Use repo-relative paths and symbol names so the document remains portable across clones and review tools
- Avoid workstation-specific absolute paths or absolute local markdown links

## Exclusions

Do not include:
- Exhaustive file-by-file walkthroughs
- Low-level implementation details that change often
- Direct code links as the primary navigation mechanism
- One-off facts that do not help a contributor answer "where should I change code?"
