# Repository Ecosystem Map

## Overview

This document maps the relationships between the reference architecture repository and the actual test automation repositories that implement it.

## Repository Relationships

```mermaid
graph TB
    subgraph "Reference Architecture"
        REF[qe-platform-reference-architecture<br/>This Repository]
    end
    
    subgraph "Test Automation Repositories"
        UI[ui-test-automation<br/>Selenium + Cucumber + TestNG]
        API[api-test-automation<br/>RestAssured]
        PERF[performance-test-automation<br/>JMeter/Taurus]
    end
    
    subgraph "Application Repositories"
        APP1[application-repo-1]
        APP2[application-repo-2]
        APPN[application-repo-n]
    end
    
    subgraph "CI/CD System"
        CI[GitHub Actions<br/>Jenkins<br/>GitLab CI]
    end
    
    subgraph "Reporting & Observability"
        ALLURE[Allure TestOps/Reports]
        OBS[Observability Platform]
    end
    
    REF -.->|defines standards| UI
    REF -.->|defines standards| API
    REF -.->|defines standards| PERF
    
    UI -->|runs tests against| APP1
    UI -->|runs tests against| APP2
    API -->|runs tests against| APP1
    API -->|runs tests against| APP2
    PERF -->|runs tests against| APP1
    PERF -->|runs tests against| APP2
    
    UI -->|triggers| CI
    API -->|triggers| CI
    PERF -->|triggers| CI
    
    CI -->|generates| ALLURE
    CI -->|sends metrics| OBS
    
    ALLURE -->|displays| OBS
```

## Repository Responsibilities

### Reference Architecture Repository (This Repo)

**Purpose**: Define standards, workflows, and governance

**Contains**:

- Quality gate definitions
- Test strategy standards
- Governance policies
- Release workflows
- Onboarding guides

**Does NOT contain**:

- Actual test code
- Application-specific configurations
- Proprietary information

### UI Test Automation Repository

**Purpose**: End-to-end UI testing

**Implements**:

- Selenium WebDriver tests
- Cucumber BDD scenarios
- TestNG test execution
- Page Object Model pattern

**References**:

- This repository for standards
- Application repositories for test targets

**Generates**:

- Allure reports with screenshots
- Test execution artifacts

### API Test Automation Repository

**Purpose**: API contract and integration testing

**Implements**:

- RestAssured API tests
- Contract testing
- API performance tests
- Schema validation

**References**:

- This repository for standards
- API documentation (OpenAPI/Swagger)

**Generates**:

- Allure reports with request/response logs
- API test execution artifacts

### Performance Test Automation Repository

**Purpose**: Load, stress, and performance testing

**Implements**:

- JMeter test plans
- Taurus configurations
- Performance benchmarks
- Load scenarios

**References**:

- This repository for standards
- Performance requirements

**Generates**:

- Performance test reports
- Performance trend data

## Integration Patterns

### Pattern 1: PR Quality Gate

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant AppRepo as Application Repo
    participant TestRepo as Test Repo
    participant CI as CI/CD
    participant Gate as Quality Gate
    
    Dev->>AppRepo: Create PR
    AppRepo->>CI: PR created
    CI->>TestRepo: Trigger smoke tests
    TestRepo->>AppRepo: Run tests against PR branch
    TestRepo->>Gate: Report results
    Gate->>AppRepo: Pass/Fail status
    Gate->>Dev: Quality gate result
```

### Pattern 2: Release Quality Gate

```mermaid
sequenceDiagram
    participant Release as Release Manager
    participant AppRepo as Application Repo
    participant TestRepo as Test Repo
    participant CI as CI/CD
    participant Gate as Quality Gate
    participant Report as Allure Reports
    
    Release->>AppRepo: Create release branch
    AppRepo->>CI: Release branch created
    CI->>TestRepo: Trigger regression suite
    TestRepo->>AppRepo: Run full test suite
    TestRepo->>Report: Generate Allure report
    Report->>Gate: Quality metrics
    Gate->>Release: Go/No-Go decision
```

### Pattern 3: Cross-Repository Testing

```mermaid
graph LR
    subgraph "Application Changes"
        APP[Application Repo<br/>Feature Branch]
    end
    
    subgraph "Test Execution"
        UI[UI Tests]
        API[API Tests]
        PERF[Performance Tests]
    end
    
    subgraph "Quality Decision"
        GATE[Quality Gate]
    end
    
    APP -->|triggers| UI
    APP -->|triggers| API
    APP -->|triggers| PERF
    
    UI -->|results| GATE
    API -->|results| GATE
    PERF -->|results| GATE
    
    GATE -->|decision| APP
```

## Repository Naming Conventions

All repositories follow a consistent naming pattern:

- **Reference Architecture**: `qe-platform-reference-architecture`
- **UI Tests**: `{org}-ui-test-automation` or `ui-test-automation`
- **API Tests**: `{org}-api-test-automation` or `api-test-automation`
- **Performance Tests**: `{org}-performance-test-automation` or `performance-test-automation`

## Repository Structure Alignment

Each test automation repository should align with this reference architecture:

```text
test-automation-repo/
├── README.md                    # References this architecture
├── .github/
│   └── workflows/
│       └── quality-gates.yml    # Implements quality gates from this repo
├── src/
│   └── test/                    # Test code following standards
├── docs/
│   └── README.md                # Repository-specific docs
└── pom.xml / package.json       # Dependencies
```

## Dependency Management

### Test Repositories Depend On

- **Reference Architecture**: For standards and governance (documentation dependency)
- **Application Repositories**: For test targets (runtime dependency)
- **Test Frameworks**: Selenium, RestAssured, JMeter (library dependency)

### Reference Architecture Depends On

- **Nothing**: This is a standalone reference

## Versioning Strategy

- **Reference Architecture**: Semantic versioning (e.g., v1.0.0)
- **Test Repositories**: Follow application versioning or semantic versioning
- **Standards Compatibility**: Test repositories should reference specific versions of this architecture

## Communication Flow

```mermaid
graph TB
    subgraph "Standards Definition"
        REF[Reference Architecture]
    end
    
    subgraph "Implementation"
        UI[UI Test Repo]
        API[API Test Repo]
        PERF[Performance Test Repo]
    end
    
    subgraph "Feedback Loop"
        ISSUES[Issues & Improvements]
        PRS[Pull Requests]
    end
    
    REF -->|defines| UI
    REF -->|defines| API
    REF -->|defines| PERF
    
    UI -->|feedback| ISSUES
    API -->|feedback| ISSUES
    PERF -->|feedback| ISSUES
    
    ISSUES -->|improvements| PRS
    PRS -->|updates| REF
```

## Next Steps

- Review [Quality Gates](03-quality-gates.md) to understand integration points
- See [Test Strategy Standards](05-test-strategy-standards.md) for implementation details
- Check [Onboarding Playbook](09-onboarding-playbook.md) for repository setup
