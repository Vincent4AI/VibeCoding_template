# VibeCoding Template

**SDD (Spec-Driven Development) + Claude Code Project Initialization Template**

A project template designed for the Claude Code vibecoding workflow. When starting a new project, use the initialization prompt to generate a complete development framework in one shot: spec-driven development system, progress tracking, and cross-session memory.

**[English](./EN/) | [中文](./CN/)**

---

## Why This Template?

Vibecoding is great — until your project gets big enough to lose control:

- Claude Code is "amnesic" across sessions — context is lost every time
- Without spec constraints, generated code is inconsistent in style
- No way to track what's been changed — progress tracking is all in your head
- Module interfaces aren't aligned — integration is full of surprises

**This template solves these problems with SDD workflow + automated progress tracking.**

## Core Idea

```
Write spec first → Then write code → Auto-track progress
```

| Mechanism | What It Solves |
|-----------|---------------|
| `CLAUDE.md` | Unified coding conventions, interface definitions, forbidden operations |
| `TODO.md` | Feature roadmap, auto-checked on completion |
| `docs/sdd/STATUS.md` | Module status matrix, everything at a glance |
| `docs/sdd/specs/` | Module specs that constrain code generation |
| `MEMORY.md` | Cross-session memory, no more re-explaining context |

## Quick Start

### 1. Create a new project directory

```bash
mkdir my-project && cd my-project
```

### 2. Open Claude Code

```bash
claude
```

### 3. Paste the initialization prompt

Copy the contents of the init prompt file — pick your language:

- **English**: [`EN/init-prompt.md`](./EN/init-prompt.md)
- **中文**: [`CN/init-prompt.md`](./CN/init-prompt.md)

Fill in the 6 project info fields:

```
- Project Name: my-awesome-app
- One-line Description: A tool that does XX
- Language/Tech Stack: TypeScript + Node.js
- Build Tool: npm
- Test Framework: Jest
- Database: PostgreSQL
```

Paste into Claude Code and send — **all files are generated automatically in one shot**.

### 4. Start developing

Generated file structure:

```
my-project/
├── CLAUDE.md                          # Project conventions (auto-read by Claude Code)
├── TODO.md                            # Development roadmap
├── docs/
│   └── sdd/
│       ├── README.md                  # SDD process docs
│       ├── STATUS.md                  # Module status matrix
│       ├── templates/
│       │   └── module-spec.tmpl.md    # Module spec template
│       ├── specs/                     # Individual module specs
│       └── adr/                       # Architecture Decision Records
│           ├── README.md
│           └── template.md
└── .claude/projects/.../memory/
    └── MEMORY.md                      # Cross-session memory
```

## SDD Workflow

```
┌─────────┐    ┌─────────┐    ┌──────────┐    ┌─────────┐    ┌──────────┐
│  Draft  │───▶│ Review  │───▶│ Approved │───▶│  Impl   │───▶│ Verified │
└─────────┘    └─────────┘    └──────────┘    └─────────┘    └──────────┘
 Write spec    Review spec    Spec approved   Write code     Tests pass
```

**After completing each module, Claude Code automatically updates:**
1. `TODO.md` — Checks off `[x]`
2. `docs/sdd/STATUS.md` — Updates the status matrix
3. `MEMORY.md` — Updates cross-session memory

## Auto Progress Tracking

This is the template's core feature. A mandatory instruction is built into `CLAUDE.md`:

> After completing any module or feature implementation, Claude Code **MUST** automatically update TODO.md, STATUS.md, and MEMORY.md — no user prompting required.

You don't need to maintain progress manually — just focus on writing requirements.

## Template Structure

```
VibeCoding_template/
├── README.md                              # This file
├── EN/                                    # English version
│   ├── init-prompt.md                     # Initialization prompt
│   └── docs/sdd/                          # SDD framework files
│       ├── README.md
│       ├── STATUS.md
│       ├── templates/module-spec.tmpl.md
│       ├── specs/
│       └── adr/
└── CN/                                    # 中文版本
    ├── init-prompt.md                     # 初始化 prompt
    └── docs/sdd/                          # SDD 框架文件
        ├── README.md
        ├── STATUS.md
        ├── templates/module-spec.tmpl.md
        ├── specs/
        └── adr/
```

## Use Cases

- Personal vibecoding projects
- Projects requiring long-term Claude Code maintenance
- Multi-module projects needing interface alignment
- Any scenario where you want more control over AI coding

## License

MIT
