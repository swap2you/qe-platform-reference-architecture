# Mermaid Diagram Snippets

This document contains reusable Mermaid diagram snippets for documentation. Copy and modify these snippets as needed.

## Platform Architecture

### Component Diagram

```mermaid
graph TB
    subgraph "Test Automation Repositories"
        UI[UI Test Repo]
        API[API Test Repo]
        PERF[Performance Test Repo]
    end
    
    subgraph "CI/CD Pipeline"
        PR[Pull Request]
        MERGE[Merge to Main]
        RELEASE[Release Branch]
    end
    
    subgraph "Quality Gates"
        SMOKE[Smoke Tests]
        REGRESSION[Regression Tests]
        PERF_GATE[Performance Benchmarks]
        SECURITY[Security-Lite Scan]
    end
    
    UI --> PR
    API --> PR
    PERF --> RELEASE
    
    PR --> SMOKE
    MERGE --> REGRESSION
    RELEASE --> PERF_GATE
    RELEASE --> SECURITY
```

## Quality Gates

### Quality Gate Workflow

```mermaid
graph TB
    PR[Pull Request] --> SMOKE[Smoke Tests]
    SMOKE -->|pass| MERGE[Allow Merge]
    SMOKE -->|fail| BLOCK[Block Merge]
    
    MERGE --> REGRESSION[Regression Tests]
    REGRESSION -->|pass| RELEASE[Release Branch]
    REGRESSION -->|fail| NOTIFY[Notify Team]
    
    RELEASE --> PERF[Performance Tests]
    RELEASE --> SEC[Security Scan]
    
    PERF -->|pass| APPROVE[Approve Release]
    SEC -->|pass| APPROVE
    
    PERF -->|fail| BLOCK_RELEASE[Block Release]
    SEC -->|fail| BLOCK_RELEASE
```

## Release Workflow

### Release Readiness Flow

```mermaid
graph TB
    START[Release Branch Created] --> REGRESSION[Run Regression Suite]
    REGRESSION --> REG_CHECK{All Tests Pass?}
    
    REG_CHECK -->|No| FIX_REGRESSION[Fix Regression Failures]
    FIX_REGRESSION --> REGRESSION
    
    REG_CHECK -->|Yes| PERF[Run Performance Tests]
    PERF --> PERF_CHECK{Meets SLA?}
    
    PERF_CHECK -->|No| FIX_PERF[Fix Performance Issues]
    FIX_PERF --> PERF
    
    PERF_CHECK -->|Yes| SECURITY[Run Security Scan]
    SECURITY --> SEC_CHECK{No Critical Issues?}
    
    SEC_CHECK -->|No| FIX_SEC[Fix Security Issues]
    FIX_SEC --> SECURITY
    
    SEC_CHECK -->|Yes| EVIDENCE[Generate Release Evidence]
    EVIDENCE --> REVIEW[Release Review Meeting]
    REVIEW --> DECISION{Go/No-Go Decision}
    
    DECISION -->|Go| APPROVE[Approve Release]
    DECISION -->|No-Go| BLOCK[Block Release]
```

## Test Execution

### Test Execution Flow

```mermaid
sequenceDiagram
    participant Dev as Developer
    participant PR as Pull Request
    participant Smoke as Smoke Tests
    participant Main as Main Branch
    participant Regression as Regression Tests
    participant Report as Allure Reports
    
    Dev->>PR: Create PR
    PR->>Smoke: Trigger smoke tests
    Smoke->>Report: Generate report
    Report->>PR: Pass/Fail status
    
    alt Smoke Tests Pass
        PR->>Main: Merge approved
        Main->>Regression: Trigger regression suite
        Regression->>Report: Generate report
        Report->>Main: Quality status
    end
```

## Repository Ecosystem

### Repository Relationships

```mermaid
graph TB
    subgraph "Reference Architecture"
        REF[qe-platform-reference-architecture]
    end
    
    subgraph "Test Automation Repositories"
        UI[ui-test-automation]
        API[api-test-automation]
        PERF[performance-test-automation]
    end
    
    subgraph "Application Repositories"
        APP1[application-repo-1]
        APP2[application-repo-2]
    end
    
    REF -.->|defines standards| UI
    REF -.->|defines standards| API
    REF -.->|defines standards| PERF
    
    UI -->|runs tests against| APP1
    API -->|runs tests against| APP1
    PERF -->|runs tests against| APP1
```

## Observability

### Observability Components

```mermaid
graph TB
    subgraph "Data Collection"
        TESTS[Test Execution]
        CI[CI/CD Pipeline]
        REPORTS[Test Reports]
    end
    
    subgraph "Metrics"
        QUALITY[Quality Metrics]
        PERFORMANCE[Performance Metrics]
        TRENDS[Trend Analysis]
    end
    
    subgraph "Visualization"
        DASHBOARD[Quality Dashboard]
        ALERTS[Alerts & Notifications]
    end
    
    TESTS --> QUALITY
    CI --> QUALITY
    REPORTS --> QUALITY
    
    QUALITY --> TRENDS
    PERFORMANCE --> TRENDS
    
    TRENDS --> DASHBOARD
    QUALITY --> DASHBOARD
    PERFORMANCE --> DASHBOARD
    
    DASHBOARD --> ALERTS
```

## Flaky Test Management

### Flaky Test Workflow

```mermaid
graph TB
    DETECT[Detect Flaky Test] --> CLASSIFY[Classify Priority]
    CLASSIFY --> CRITICAL{Critical?}
    
    CRITICAL -->|Yes| DISABLE[Disable Test]
    DISABLE --> INVESTIGATE[Investigate Root Cause]
    
    CRITICAL -->|No| INVESTIGATE
    
    INVESTIGATE --> FIX[Fix Test]
    FIX --> VALIDATE[Validate Fix]
    VALIDATE --> RE_ENABLE[Re-enable Test]
    RE_ENABLE --> MONITOR[Monitor Stability]
    
    MONITOR --> STABLE{Stable?}
    STABLE -->|Yes| CLOSE[Close Issue]
    STABLE -->|No| INVESTIGATE
```

## Test Pyramid

### Test Distribution

```mermaid
graph TB
    subgraph "Test Pyramid"
        E2E[E2E Tests<br/>10% - Critical Paths]
        INT[Integration Tests<br/>20% - API Contracts]
        UNIT[Unit Tests<br/>70% - Fast, Many]
    end
    
    E2E --> INT
    INT --> UNIT
```

## Usage Instructions

1. **Copy the snippet** you need
2. **Paste into your markdown file** within a mermaid code block
3. **Modify as needed** for your specific use case
4. **Test rendering** to ensure diagram displays correctly

## Customization Tips

- **Colors**: Add style definitions for visual emphasis
- **Labels**: Modify labels to match your terminology
- **Layout**: Change graph direction (TB, LR, etc.)
- **Grouping**: Use subgraphs to organize components
- **Styling**: Add CSS classes for custom styling

## Example with Styling

```mermaid
graph TB
    A[Start] --> B[Process]
    B --> C[End]
    
    style A fill:#90EE90
    style B fill:#87CEEB
    style C fill:#FFB6C1
```
