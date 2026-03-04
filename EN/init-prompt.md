# SDD Project Initialization Prompt

> Copy everything below the `---` line and paste it into your first Claude Code session for a new project.
> Replace each `[PLACEHOLDER]` with your project information (6 fields total).

---

Please initialize a development framework for my new project. Here is the project information:

- **Project Name**: [project name]
- **One-line Description**: [what this project does]
- **Language/Tech Stack**: [Go 1.22+ / TypeScript + Node / Python 3.12 / ...]
- **Build Tool**: [Go Modules / npm / poetry / ...]
- **Test Framework**: [Go testing + testify / Jest / pytest / ...]
- **Database**: [SQLite / PostgreSQL / None / ...]

## Requirements

### 1. Create CLAUDE.md

Create `CLAUDE.md` in the project root with the following sections (adjust content based on the actual tech stack):

```
# CLAUDE.md — [Project Name] Conventions

## Project Overview
[One-line description]

## Tech Stack
[List language, framework, core dependencies]

## Directory Structure
[Design a reasonable directory tree for the project type, with comments describing each directory's responsibility]

## Coding Standards
### Naming Conventions
[Rules for file names, package/module names, interface/class names, constants, error variables]

### Error Handling
[Error handling patterns for this project, with correct and incorrect examples]

### Logging
[Logging library choice and usage patterns]

### Testing
[Test standards: naming, table-driven / parametrize patterns, coverage requirements]

## Core Interface Definitions
[Define 2-3 of the project's most critical interfaces/abstractions with complete type signatures]

## Forbidden Operations
[List things Claude Code is NOT allowed to do in this project, e.g.: modifying core interfaces, introducing specific dependencies, hardcoding secrets, etc.]

## Dependency Management
[Core dependency list, note that adding new dependencies requires justification]

## Commit Conventions
feat / fix / refactor / test / docs / chore, with examples

## Spec-Driven Development (SDD)
This project follows the Spec-Driven Development workflow.

- **SDD Process Docs**: docs/sdd/README.md
- **Module Status Overview**: docs/sdd/STATUS.md
- **Module Spec Template**: docs/sdd/templates/module-spec.tmpl.md
- **Module Specs Directory**: docs/sdd/specs/
- **Architecture Decision Records**: docs/sdd/adr/

Development workflow: Write spec → Implement → Test → Verify.

## Progress Tracking (Auto-maintained)

After completing any module or feature implementation, Claude Code **MUST** automatically update the following three files without user prompting:

1. **`TODO.md`** — Change the corresponding item from `[ ]` to `[x]`
2. **`docs/sdd/STATUS.md`** — Update the module status matrix (status, implementation path, test path); move new modules from "Pending Modules" into the matrix
3. **`.claude/projects/.../memory/MEMORY.md`** — Update "Recently Completed" and "Next Priorities"

This is a mandatory process and must not be skipped.
```

### 2. Create TODO.md

```markdown
# [Project Name] — Development Progress Tracker

## Completed

### Phase 0 — Project Initialization
- [x] Project skeleton + directory structure
- [x] CLAUDE.md project conventions
- [x] SDD framework (spec template, STATUS, ADR)
- [x] TODO / MEMORY progress tracking system

## Pending

### High Priority
[List 3-5 primary modules based on project requirements, each item formatted as:]
- [ ] **Module Name** (`implementation/path`)
  - Sub-task 1
  - Sub-task 2

### Medium Priority
[List 2-3 items]

### Low Priority
[List 2-3 items]
```

### 3. Create docs/sdd/STATUS.md

```markdown
# SDD Module Status Overview

> Last Updated: [today]

## Status Matrix

| Module | Spec | Status | Implementation | Tests | Notes |
|--------|------|--------|----------------|-------|-------|
| (Add rows as modules are completed) | | | | | |

## Spec Lifecycle

Draft → Review → Approved → Impl → Verified

## Pending Modules

| Module | Priority | Description |
|--------|----------|-------------|
[Extract from TODO.md pending items, listed by priority]
```

### 4. Create docs/sdd/README.md

SDD process documentation, including:
- Lifecycle state diagram (Draft → Verified)
- Meaning of each state
- Development workflow (Write spec → Review → Implement → Verify)
- Review checklist
- Implementation phase rules
- Verification checklist
- AI collaboration guidelines (how to use specs to constrain code generation)

### 5. Create docs/sdd/templates/module-spec.tmpl.md

A universal module spec template with the following sections:

```markdown
# [Module Name] Specification

| Field | Value |
|-------|-------|
| Module | `[package/path]` |
| Status | Draft |
| Version | 0.1.0 |
| Created | [today] |

## 1. Overview
## 2. Interface Contract
## 3. Data Contract
## 4. Behavioral Specification (Preconditions / Postconditions / Invariants)
## 5. Error Contract
## 6. Performance Constraints
## 7. Dependencies
## 8. Acceptance Criteria
## 9. Changelog
```

### 6. Create docs/sdd/adr/ Framework

- `docs/sdd/adr/README.md` — ADR index
- `docs/sdd/adr/template.md` — ADR template (title, status, context, decision, consequences)

### 7. Initialize MEMORY.md

Create in Claude Code's auto memory directory:

```markdown
# [Project Name] — Claude Code Cross-Session Memory

## Project Status
- Project just initialized, SDD framework is ready
- Status board: docs/sdd/STATUS.md
- Development backlog: TODO.md

## Recently Completed
- Project skeleton + SDD framework initialization

## Next Priorities
[Take top 3 items from TODO.md high priority]

## Key Conventions
[Extract 3-5 most critical rules from CLAUDE.md]
```

## Output Requirements

1. Based on the project information I provided, **generate actual content** — not placeholders
2. Core interface definitions in CLAUDE.md should be designed for the project domain — do not leave them empty
3. The pending list in TODO.md should plan reasonable module decomposition based on project requirements
4. Write all files directly to disk — do not just output content for me to create manually
5. Run a build/compile at the end to confirm the project skeleton works
