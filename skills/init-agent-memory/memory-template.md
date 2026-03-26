# AGENTS.md Template

Use this template to create the concise canonical memory document.

## Project Overview

- Purpose: [What the project does and why it exists]
- Scope: [Core responsibilities and boundaries]
- Primary anchors: `path/to/file`, `[symbol/type/module name]`

## Tech Stack

- Languages/runtime: [TypeScript, Node.js, etc.]
- Frameworks/libraries: [Commander.js, Vitest, etc.]
- Tooling: [build/lint/test tools]
- Primary anchors: `path/to/file`, `[config key/entrypoint/module]`

## Key Directories

- `src/...`: [responsibility]
- `...`: [responsibility]
- Anchor each directory with a repo-relative path and a stable symbol or responsibility name

## Essential Build/Test Commands

- `...`: [what it does and when to use it]
- `...`: [what it does and when to use it]
- Primary anchors: `path/to/file`, `[command/config section]`

## Documentation Conventions

- Use repo-relative paths, not workstation-specific absolute paths
- Prefer path plus stable names over raw `file:line` references
- Use `file:line` only when precision materially helps and the anchor is likely to stay stable
- In longer docs, collect source anchors in one place instead of repeating citations on every line

## Additional Documentation

- `ARCHITECTURE.md`: Bird's-eye overview, codemap, invariants, and boundaries
- Add only docs that provide specialized detail not suitable for AGENTS.md

## Constraints

- Keep full document under 150 lines
- Use repo-relative paths and stable symbols instead of code snippets or machine-specific paths
- Use `file:line` sparingly rather than as the default citation style
- Keep guidance universally applicable for contributors and agents
- Treat `AGENTS.md` as canonical, then create `CLAUDE.md` as a symlink to `AGENTS.md`
