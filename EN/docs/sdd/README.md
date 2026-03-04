# Spec-Driven Development (SDD) Process

## Overview

SDD (Spec-Driven Development) is a development methodology centered on specification documents. Before writing any code, define the module's interface contracts, data contracts, and behavioral specifications, then use the spec to constrain the implementation.

## Lifecycle

```
┌─────────┐    ┌─────────┐    ┌──────────┐    ┌─────────┐    ┌──────────┐
│  Draft  │───▶│ Review  │───▶│ Approved │───▶│  Impl   │───▶│ Verified │
└─────────┘    └─────────┘    └──────────┘    └─────────┘    └──────────┘
```

### State Definitions

| State | Meaning |
|-------|---------|
| **Draft** | Initial spec draft, may be incomplete, open to major changes |
| **Review** | Spec is mostly complete, entering review phase, only corrective changes accepted |
| **Approved** | Spec passed review, interfaces are frozen, implementation can begin |
| **Impl** | Implementation in progress, no breaking changes to the spec allowed |
| **Verified** | Implementation complete, all acceptance criteria passed, module delivered |

## Development Workflow

### Phase 1: Write Spec (Draft)

1. Copy the template from `templates/module-spec.tmpl.md` to the `specs/` directory
2. Fill in all sections, focusing on:
   - **Interface Contract**: All public function/method signatures, parameter types, return values
   - **Data Contract**: Struct/type definitions, database schemas
   - **Behavioral Specification**: Preconditions, postconditions, invariants
   - **Error Contract**: All possible error types and their trigger conditions
3. Note dependencies: which other module specs does this module depend on

### Phase 2: Review Spec (Review)

#### Review Checklist

- [ ] Interface signatures are complete and unambiguous
- [ ] All parameters and return values have type annotations
- [ ] All error scenarios are enumerated with handling strategies
- [ ] Preconditions and postconditions are testable
- [ ] Performance constraints are reasonable and measurable
- [ ] Interfaces are consistent with dependent modules
- [ ] Acceptance criteria are specific and executable

#### Review Pass Criteria

- All checklist items pass
- No remaining TODOs or TBDs
- Dependent module specs are at Approved status or higher

### Phase 3: Implement (Impl)

#### Implementation Phase Rules

1. **Implement strictly per spec** — Public interfaces must exactly match the spec
2. **No deviations allowed** — If a spec issue is found, update the spec first, then the code
3. **Write tests first** — Write test cases based on the spec's acceptance criteria
4. **Internal freedom** — Private functions and internal structures are not constrained by the spec
5. **Update progress** — After implementation, update STATUS.md and TODO.md

### Phase 4: Verify (Verified)

#### Verification Checklist

- [ ] Test cases exist and pass for all acceptance criteria
- [ ] Public interfaces exactly match the spec
- [ ] Error handling covers all scenarios listed in the spec
- [ ] Performance meets the constraints defined in the spec
- [ ] Code passes lint and static analysis
- [ ] No remaining TODO / FIXME / HACK comments

## AI Collaboration

### Using Specs to Constrain Code Generation

When asking Claude Code to implement a module:

1. **Point to the spec**: "Please implement this module according to `docs/sdd/specs/xxx.md`"
2. **Verify consistency**: After implementation, check all public interfaces against the spec
3. **Test coverage**: Ensure every acceptance criteria item has a corresponding test

### Specs as Context

Spec documents are the core context for Claude Code. Good specs = good code generation quality.

Key principles:
- The more specific the spec, the higher the code generation quality
- Interface signatures must be complete (parameter types, return values, errors)
- Usage examples are highly effective for AI understanding intent
- Edge cases and error scenarios must be explicitly listed, or AI will overlook them

## File Organization

```
docs/sdd/
├── README.md                    # This file - SDD process documentation
├── STATUS.md                    # Module status matrix
├── templates/
│   └── module-spec.tmpl.md      # Module spec template
├── specs/                       # Individual module specs
│   ├── module-a.md
│   └── module-b.md
└── adr/                         # Architecture Decision Records
    ├── README.md
    ├── template.md
    └── 001-xxx.md
```
