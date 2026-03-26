---
name: init-agent-memory
description: Creates, refreshes, or consolidates project memory docs such as `AGENTS.md` and supporting docs. Use when onboarding a repository, updating stale memory, merging overlapping memory files, or restructuring the memory layout when explicitly requested.
metadata:
  namespace: thought-cabinet
  version: "0.0.1"
---

# Initializing And Consolidating Agent Memory

Create or maintain high-signal project memory with progressive disclosure. The default shape is a concise canonical memory doc, a higher-level architecture doc, optional focused supporting docs under `docs/`, and compatibility symlinks such as `CLAUDE.md` when needed.

## Workflow Overview

1. **Gather context and choose mode** - Read instructions, existing memory docs, and explicit path inputs
2. **Research evidence** - Identify tech stack, project layout, commands, coarse-grained modules, boundaries, and stable invariants
3. **Decide whether structure approval is needed** - Only propose layout changes when the layout is new or explicitly changing
4. **Write or consolidate docs** - Refresh content in place or create the agreed structure
5. **Quality review** - Validate constraints, references, and symlink behavior

## Step 1: Gather Context And Choose Mode

### Read Inputs First

If present, read these in order:
1. User-provided memory instructions or explicit path list
2. Existing memory docs and compatibility docs such as `AGENTS.md`, `CLAUDE.md`, `ARCHITECTURE.md`, and any user-specified supporting docs
3. `README.md` and package/build metadata

Read full files before drafting. Do not assume conventions.

### Choose A Mode

Determine the mode before writing.

- **`init`**: No usable memory docs exist, or the user asks to bootstrap memory for the first time
- **`consolidate`**: Memory docs already exist and the user wants them updated, refreshed, merged, or de-duplicated
- **`restructure`**: The user explicitly wants a different memory layout, different canonical paths, or new supporting-doc splits

Default rules:

- Requests like "update agent memory", "refresh memory", or "consolidate memory" default to **`consolidate`**
- If the repo already has the target shape such as `AGENTS.md` plus `ARCHITECTURE.md`, treat that as an existing approved layout and use **`consolidate`**
- If there are multiple overlapping memory files with unclear ownership, still start in **`consolidate`** and only escalate to **`restructure`** if a real layout conflict remains

### Ask Only Missing Questions

Ask only when required information cannot be inferred from repository files.

- Good reason to ask: two competing canonical memory files and no user preference
- Bad reason to ask: the repo already uses the standard `AGENTS.md` plus `ARCHITECTURE.md` layout and the user asked to update memory

Example:

```text
I found both `AGENTS.md` and `docs/agent-memory.md`, and each looks canonical. Which file should remain the primary memory entrypoint?
```

## Step 2: Research Evidence

Collect concrete references for each required section.

### Required Evidence Buckets

- **Project overview (WHY):** repository purpose and problem domain
- **Tech stack (WHAT):** languages, frameworks, runtime, major tooling
- **Key directories (WHAT):** top-level modules and responsibilities
- **Essential commands (HOW):** build, test, lint, run workflows used daily
- **Architecture:** coarse-grained modules, boundaries, and stable invariants that explain where things live and how major parts relate

### Evidence Rules

- Prefer durable references over brittle ones: cite file paths plus stable names such as directories, packages, modules, entrypoints, functions, types, commands, or config keys
- Default to repo-relative paths rooted at the repository, not absolute filesystem paths tied to one machine
- Use exact `file:line` references only when they materially help and are likely to stay stable enough to verify soon, such as `Makefile`, `go.mod`, top-level config, or a narrowly scoped claim in a small file
- For architecture docs, name important files, modules, and types in prose; treat any `:line` references as supporting evidence snapshots rather than the primary navigation method
- For longer docs, prefer section-level source anchors or component indexes over repeating a file citation in every bullet
- Prefer primary sources such as `src/`, command definitions, config files, and entrypoints
- For architecture, prefer stable structural facts over volatile implementation details
- Include invariants and boundaries only when the codebase provides concrete evidence for them
- If evidence conflicts across docs and code, prefer the code and mention the mismatch briefly

### Reference Durability Heuristics

- Best: directory names, module names, package names, type names, function names, command names, config section names
- Good: file paths with a named symbol or responsibility, for example ``main/shark/shark.go` (`main`, `initializeWorkflowAndETCD`)``
- Use sparingly: raw `file:line` references in large, frequently edited source files
- Avoid depending on direct code links as the main way a contributor finds things; the document should still work with text search or symbol search alone

## Step 3: Decide Whether Structure Approval Is Needed

Use the mode to decide whether to stop for approval.

- **`init`**: propose the planned memory layout and get confirmation unless the user already requested that exact structure
- **`consolidate`**: keep the current layout, skip the layout-approval prompt, and proceed directly to content consolidation
- **`restructure`**: propose the new layout and get confirmation before writing

For `consolidate`, send a short status update instead of a blocking prompt.

Example:

```text
The repo already uses `AGENTS.md` and `ARCHITECTURE.md`, so I’m consolidating content in place and will only call out structural changes if I find a real gap.
```

When a layout proposal is needed, use this format:

```text
Here is the proposed memory layout.

AGENTS.md (under 150 lines):
1. Project Overview
2. Tech Stack
3. Key Directories
4. Essential Build/Test Commands
5. Additional Documentation

Supporting docs:
- ARCHITECTURE.md
- docs/... (only if needed for specialized details)

I will keep AGENTS.md as an operational index and use ARCHITECTURE.md for the high-level codemap, invariants, and boundaries.
I will then create CLAUDE.md as a symlink to AGENTS.md for backward compatibility.
Should I proceed with this structure?
```

## Step 4: Write Or Consolidate Docs

### 4a. Consolidation Rules

When working in `consolidate` mode:

- Preserve the current canonical paths unless the user requested a move
- Merge useful non-redundant content from overlapping memory docs into the canonical set
- Remove duplication across `AGENTS.md`, `ARCHITECTURE.md`, and supporting docs by keeping the higher-level summary in the more central file and moving dense detail outward
- Keep stable headings when practical so repeated updates produce smaller diffs
- Repair missing compatibility symlinks in place; that is maintenance, not a restructure

### 4b. Create Or Refresh The Canonical Memory Doc

Use [memory-template.md](memory-template.md).

Required constraints:

- Keep total length under 150 lines
- Include WHAT, WHY, HOW coverage
- Use concrete evidence references instead of code snippets; prefer `file:line` only for stable operational facts and smaller files
- Do not include formatting or style rules that linters already enforce
- Add an "Additional Documentation" section that points to `ARCHITECTURE.md` and any relevant `docs/*` files

### 4c. Create Or Refresh `ARCHITECTURE.md`

Use [architecture-template.md](architecture-template.md).

Required constraints:

- Keep it short and stable enough for recurring contributors to reread
- Start with a bird's-eye view of the system and problem being solved
- Provide a codemap of coarse-grained modules and their relationships
- Call out important architectural invariants, especially absences and layer boundaries
- End with cross-cutting concerns if they materially affect work across modules
- Name important directories, modules, files, and types without depending on fragile direct links; prefer symbol names and searchable identifiers over raw line-number navigation
- Avoid low-level implementation walkthroughs and volatile details that should live inline or in narrower docs
- Support non-trivial claims with concrete evidence, but keep line-number citations secondary and sparse in `ARCHITECTURE.md`

Create additional `docs/*.md` files only when specialized detail would make `ARCHITECTURE.md` or the canonical memory doc too dense.

### 4d. Create Compatibility Symlinks

After writing the canonical memory doc, ensure each requested compatibility file points at it.

If `CLAUDE.md` or another compatibility file already exists as a regular file instead of a symlink:
1. Read the existing content
2. Identify any useful, non-redundant information not already covered
3. Incorporate that content into the canonical memory doc or a supporting doc
4. Replace the old file with a symlink to the canonical memory doc

If the canonical file is `AGENTS.md`, create the standard compatibility symlink with:

```bash
ln -sf AGENTS.md CLAUDE.md
```

Required constraints:

- The canonical memory file remains the source of truth
- Compatibility files are symlinks, not duplicated copies, unless the user explicitly forbids symlinks
- Pre-existing useful content must be preserved before replacement

### 4e. Progressive Disclosure Rules

- Keep the canonical memory doc concise and universally applicable
- Use `ARCHITECTURE.md` for project structure and stable design knowledge
- Put specialized details in `docs/*.md`
- References from the canonical memory doc should be direct and descriptive
- Avoid deep reference chains
- Keep references collaborator-friendly: no workstation-specific absolute paths, no broken cross-doc links

### 4f. Reference Style By Document

- Canonical memory doc: use repo-relative paths plus stable symbols as the default; acceptable to use `file:line` for commands, entrypoints, and compact operational facts, but avoid peppering every sentence with line numbers
- `ARCHITECTURE.md`: prefer codemap prose built around module, file, and type names; add a short evidence note only where a non-obvious claim needs support
- Supporting docs under `docs/`: prefer repo-relative file references, short anchor lists, and searchable symbol names over absolute links or dense line-by-line citation blocks
- When a file is large or changes frequently, cite the symbol name and path rather than betting on a line number staying valid
- If the user explicitly requests strict `file:line` citations everywhere, comply, but mention that they are maintenance-heavy and best treated as snapshots

## Step 5: Quality Review

Run this checklist before presenting output:

- [ ] Canonical memory doc is under 150 lines
- [ ] Compatibility symlinks point to the canonical memory doc as intended
- [ ] Sections cover project overview, tech stack, key directories, essential commands, and additional docs
- [ ] References are concrete and durable; any `file:line` citations used are accurate at the time of writing
- [ ] References use repo-relative paths unless an absolute path is explicitly required by the user
- [ ] No workstation-specific absolute paths or broken cross-document references remain
- [ ] No code snippets in the canonical memory doc
- [ ] No generic formatting or style guidance duplicated from linters
- [ ] `ARCHITECTURE.md` includes a bird's-eye view, codemap, and any proven invariants or boundaries
- [ ] `ARCHITECTURE.md` stays focused on stable structure rather than change-prone detail
- [ ] Mode choice was appropriate: no unnecessary layout prompt in `consolidate`, no silent restructure in `restructure`
- [ ] Terminology is consistent across canonical doc, architecture doc, compatibility files, and `docs/`

Present the result with file paths and invite targeted revision requests.

## Guidelines

**Scope discipline:**

- Optimize for first-session usefulness, not exhaustive documentation
- Prefer omission over speculative or weakly supported claims

**Progressive disclosure:**

- The canonical memory doc is the entrypoint index for daily operation
- `ARCHITECTURE.md` is the high-level codemap for understanding where to change code
- Keep narrower advanced details in dedicated `docs/` files

**Reliability:**

- Cite primary sources for non-trivial claims, but prefer references that will survive ordinary refactors
- Re-check any exact line-number citations after edits
- When updating existing memory, improve the content before inventing new structure
