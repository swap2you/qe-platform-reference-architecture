# Architecture Decision Records (ADRs)

This directory contains Architecture Decision Records (ADRs) for the QE Platform Reference Architecture.

## What are ADRs?

ADRs document important architectural decisions, including:
- **Context**: Why the decision was needed
- **Decision**: What was decided
- **Options Considered**: Alternatives that were evaluated
- **Consequences**: Impact and trade-offs

## ADR Format

Each ADR follows this structure:

```markdown
# ADR-XXXX: [Title]

## Status
[Proposed | Accepted | Deprecated | Superseded]

## Context
[Why this decision is needed]

## Decision
[What was decided]

## Options Considered
- Option 1: [description]
- Option 2: [description]
- Option 3: [description]

## Consequences
- Positive: [benefits]
- Negative: [drawbacks]
- Risks: [potential issues]
```

## Current ADRs

- [ADR-0001: Documentation-First Reference Architecture](0001-doc-first-reference-architecture.md)
- [ADR-0002: Quality Gates Separation](0002-quality-gates-separation.md)
- [ADR-0003: Reporting and Evidence Standard](0003-reporting-and-evidence-standard.md)

## How to Add a New ADR

1. **Create new file**: `docs/adr/XXXX-[short-title].md`
2. **Number sequentially**: Use next available number (0004, 0005, etc.)
3. **Follow format**: Use the ADR format above
4. **Update this README**: Add entry to "Current ADRs" list
5. **Link from relevant docs**: Reference the ADR where appropriate

## ADR Status

- **Proposed**: Decision is under consideration
- **Accepted**: Decision is final and implemented
- **Deprecated**: Decision is no longer valid
- **Superseded**: Decision replaced by another ADR

## References

- [ADR GitHub Template](https://github.com/joelparkerhenderson/architecture-decision-record)
- [Documenting Architecture Decisions](https://cognitect.com/blog/2011/11/15/documenting-architecture-decisions)

