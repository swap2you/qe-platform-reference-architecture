# Documentation Index

Welcome to the QE Platform Reference Architecture documentation. This index provides a structured guide to all documentation.

## Getting Started

1. **[Platform Overview](01-platform-overview.md)** - Start here for the big picture
2. **[Repository Ecosystem Map](02-repo-ecosystem-map.md)** - Understand how repositories integrate
3. **[Onboarding Playbook](09-onboarding-playbook.md)** - Quick start for new teams

## Core Architecture

### Platform Components

- **[Platform Overview](01-platform-overview.md)** - Architecture overview, components, and principles
- **[Repository Ecosystem Map](02-repo-ecosystem-map.md)** - Repository relationships and integration patterns

### Quality Gates & Workflows

- **[Quality Gates](03-quality-gates.md)** - CI/CD quality gate definitions and implementation
- **[Release Workflows](04-release-workflows.md)** - Release readiness workflows and decision flows

### Standards & Governance

- **[Test Strategy Standards](05-test-strategy-standards.md)** - Test strategy, naming conventions, and best practices
- **[Flaky Tests Policy](06-flaky-tests-policy.md)** - Flaky test detection, management, and resolution

### Reporting & Observability

- **[Reporting and Evidence](07-reporting-and-evidence.md)** - Allure reports, artifact retention, traceability
- **[Observability](08-observability.md)** - Quality metrics, dashboards, and trend analysis

## Advanced Topics

- **[AI-Assisted QE](10-ai-assisted-qe.md)** - Practical AI use cases for quality engineering

## Compliance & Audit

- **[Platform Contract Compliance](11-platform-contract-compliance.md)** - Compliance checklist for implementing repositories
- **[Repository Audit Guide](12-repo-audit-guide.md)** - Step-by-step audit procedure

## Architecture Decision Records

- **[ADRs](adr/README.md)** - Architecture Decision Records documenting key decisions
  - [ADR-0001: Documentation-First Reference Architecture](adr/0001-doc-first-reference-architecture.md)
  - [ADR-0002: Quality Gates Separation](adr/0002-quality-gates-separation.md)
  - [ADR-0003: Reporting and Evidence Standard](adr/0003-reporting-and-evidence-standard.md)

## Reference

- **[Mermaid Diagrams](diagrams/mermaid-snippets.md)** - Reusable diagram snippets
- **[Issues Backlog](issues-backlog.md)** - Platform improvement backlog

## Documentation Structure

```text
docs/
├── index.md                          # This file
├── 01-platform-overview.md           # Platform architecture
├── 02-repo-ecosystem-map.md         # Repository relationships
├── 03-quality-gates.md              # Quality gate definitions
├── 04-release-workflows.md          # Release processes
├── 05-test-strategy-standards.md    # Test standards
├── 06-flaky-tests-policy.md         # Flaky test management
├── 07-reporting-and-evidence.md     # Reporting standards
├── 08-observability.md              # Quality observability
├── 09-onboarding-playbook.md        # Team onboarding
├── 10-ai-assisted-qe.md             # AI use cases
├── 11-platform-contract-compliance.md # Compliance checklist
├── 12-repo-audit-guide.md           # Audit procedure
├── adr/                              # Architecture Decision Records
│   ├── README.md
│   ├── 0001-doc-first-reference-architecture.md
│   ├── 0002-quality-gates-separation.md
│   └── 0003-reporting-and-evidence-standard.md
├── diagrams/
│   └── mermaid-snippets.md          # Diagram library
└── issues-backlog.md                # Improvement backlog
```

## How to Navigate

- **New to the platform?** → Start with [Platform Overview](01-platform-overview.md) and [Onboarding Playbook](09-onboarding-playbook.md)
- **Implementing quality gates?** → Read [Quality Gates](03-quality-gates.md) and [Release Workflows](04-release-workflows.md)
- **Setting up repositories?** → Review [Repository Ecosystem Map](02-repo-ecosystem-map.md) and [Test Strategy Standards](05-test-strategy-standards.md)
- **Managing quality metrics?** → See [Reporting and Evidence](07-reporting-and-evidence.md) and [Observability](08-observability.md)

## Contributing

See [CONTRIBUTING.md](../CONTRIBUTING.md) for guidelines on contributing to this documentation.
