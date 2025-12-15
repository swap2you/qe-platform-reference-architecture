# QE Platform Contract

**Version**: 1.0.0  
**Effective Date**: 2025-12-14  
**Status**: REQUIRED for all implementing repositories

## Purpose

This contract defines **mandatory standards** that any repository implementing the QE Platform Reference Architecture must follow. Non-compliance blocks production releases.

## Scope

This contract applies to:
- UI test automation repositories
- API test automation repositories
- Performance test automation repositories
- Any repository claiming compliance with this platform

## Required Standards

### 1. Repository Folder Structure

Every implementing repository MUST follow this structure:

```
repository-name/
├── README.md                    # Required: references this contract
├── .github/
│   ├── workflows/
│   │   ├── smoke-tests.yml     # Required: PR gate
│   │   └── regression-tests.yml # Required: nightly gate
│   ├── CODEOWNERS              # Required: defines ownership
│   └── PULL_REQUEST_TEMPLATE.md # Required: PR quality checks
├── src/
│   └── test/
│       ├── java/               # Or appropriate language structure
│       │   └── com/
│       │       └── [org]/
│       │           └── tests/
│       │               ├── smoke/      # Smoke tests
│       │               ├── regression/  # Regression tests
│       │               └── [feature]/  # Feature-specific tests
│       └── resources/
│           ├── features/       # Cucumber feature files (if applicable)
│           ├── test-data/      # Test data files
│           └── config/        # Configuration files
├── docs/
│   ├── README.md              # Required: repository-specific docs
│   ├── test-strategy.md       # Required: test strategy documentation
│   └── reporting-guide.md     # Required: reporting standards
├── pom.xml / package.json     # Build configuration
└── .gitignore
```

**Compliance Check**: Repository structure matches this pattern.

### 2. Required CI/CD Quality Gates

#### 2.1 PR Gate: Smoke Test Suite

**REQUIRED**: Every Pull Request MUST trigger a smoke test suite.

**Requirements**:
- Workflow file: `.github/workflows/smoke-tests.yml`
- Trigger: `pull_request` events
- Test tags: `@smoke` or equivalent
- Execution time: < 10 minutes
- **Blocking**: PR merge MUST be blocked if smoke tests fail
- Artifacts: Allure results MUST be uploaded

**Example workflow structure**:
```yaml
name: Smoke Tests
on:
  pull_request:
jobs:
  smoke-tests:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - name: Run smoke tests
        run: mvn test -Dgroups=smoke
      - name: Generate Allure report
        run: mvn allure:report
      - name: Upload Allure results
        uses: actions/upload-artifact@v3
        with:
          name: allure-results
          path: target/allure-results
```

**Compliance Check**: PR workflow exists, blocks on failure, generates Allure artifacts.

#### 2.2 Nightly Gate: Regression Test Suite

**REQUIRED**: Scheduled regression test execution.

**Requirements**:
- Workflow file: `.github/workflows/regression-tests.yml`
- Trigger: Scheduled (cron: `0 2 * * *` or similar)
- Test tags: `@regression` or equivalent
- Execution time: < 60 minutes
- Artifacts: Allure results + logs + screenshots MUST be retained for 30 days

**Compliance Check**: Nightly workflow exists, scheduled, retains artifacts.

#### 2.3 Artifact Retention Policy

**REQUIRED**: All test executions MUST produce and retain artifacts.

**Required Artifacts**:
- Allure test results (JSON/XML)
- Test execution logs
- Screenshots (for UI tests, on failure)
- Performance metrics (for performance tests)
- Test metadata (execution time, environment, version)

**Retention Periods**:
- PR artifacts: 7 days
- Nightly artifacts: 30 days
- Release artifacts: 90 days

**Compliance Check**: Artifacts are uploaded, retention periods are configured.

### 3. Required Tagging Taxonomy

#### 3.1 Test Type Tags

**REQUIRED**: All tests MUST be tagged with test type.

**Cucumber Tags**:
- `@smoke` - Smoke tests (critical path)
- `@regression` - Regression tests (full suite)
- `@performance` - Performance tests
- `@security` - Security tests

**TestNG Groups**:
- `smoke` - Smoke tests
- `regression` - Regression tests
- `performance` - Performance tests
- `security` - Security tests

**Compliance Check**: All tests have appropriate tags, tags are used in CI workflows.

#### 3.2 Feature Tags

**REQUIRED**: Tests MUST be tagged with feature/component.

**Examples**:
- `@login` - Login functionality
- `@checkout` - Checkout process
- `@payment` - Payment processing
- `@api-users` - User API endpoints

**Compliance Check**: Tests are tagged by feature, tags are documented.

#### 3.3 Priority Tags

**REQUIRED**: Critical tests MUST be tagged with priority.

**Tags**:
- `@critical` - Critical tests (must pass)
- `@high` - High priority tests
- `@medium` - Medium priority tests
- `@low` - Low priority tests

**Compliance Check**: Critical tests are identified and tagged.

### 4. Required Reporting Standard: Allure Evidence Bundle

**REQUIRED**: Every test execution MUST generate an Allure evidence bundle.

**Bundle Contents**:
1. **Allure Report** (HTML)
   - Test execution results
   - Test history and trends
   - Screenshots (UI tests)
   - Request/response logs (API tests)
   - Performance metrics (performance tests)

2. **Test Execution Summary** (JSON/XML)
   - Total tests executed
   - Pass/fail/skip counts
   - Execution time
   - Test coverage metrics

3. **Artifacts**
   - Screenshots (on failure for UI tests)
   - Logs (browser console, API logs)
   - Videos (optional, for flaky tests)

4. **Metadata**
   - Execution timestamp
   - Environment information
   - Application version
   - Test framework version

**Compliance Check**: Allure reports are generated, artifacts are included, metadata is present.

### 5. Required Documentation Set

**REQUIRED**: Every implementing repository MUST include:

#### 5.1 README.md Sections

- **Repository Purpose**: What this repository tests
- **Contract Compliance**: Link to this CONTRACT.md
- **Quick Start**: How to run tests locally
- **CI/CD Status**: Links to workflow badges
- **Test Structure**: How tests are organized
- **Reporting**: How to access Allure reports
- **Contributing**: How to add new tests

#### 5.2 /docs Folder Contents

- `docs/README.md` - Documentation index
- `docs/test-strategy.md` - Test strategy and approach
- `docs/reporting-guide.md` - Reporting standards and access
- `docs/onboarding.md` - Team onboarding guide (optional but recommended)

**Compliance Check**: Required documentation exists and is up-to-date.

### 6. Required Governance

#### 6.1 Branch Strategy

**REQUIRED**: Git branching MUST follow this pattern.

**Branches**:
- `main` - Production-ready code (protected)
- `develop` - Integration branch (optional)
- `feature/*` - Feature branches
- `bugfix/*` - Bug fix branches
- `hotfix/*` - Emergency fixes

**Rules**:
- All changes MUST go through Pull Requests
- `main` branch MUST be protected
- PRs MUST pass smoke tests before merge
- At least one approval required (via CODEOWNERS)

**Compliance Check**: Branch strategy is documented, main is protected, PRs are required.

#### 6.2 PR Template Requirements

**REQUIRED**: Every PR MUST use a template that includes:

- Description of changes
- Test execution results (smoke tests)
- Link to Allure report
- Public-safe check (no proprietary information)
- Documentation updates (if applicable)

**Compliance Check**: PR template exists, PRs use template, required fields are filled.

#### 6.3 CODEOWNERS Usage

**REQUIRED**: `.github/CODEOWNERS` MUST define ownership.

**Minimum Requirements**:
- Default owner for all files
- Specific owners for critical paths (if applicable)
- Review requirements documented

**Example**:
```
* @team-lead
/.github/workflows/ @devops-team
/docs/ @qe-team
```

**Compliance Check**: CODEOWNERS file exists, ownership is defined, reviews are enforced.

## Compliance Verification

To verify compliance, use:
- [`docs/11-platform-contract-compliance.md`](docs/11-platform-contract-compliance.md) - Compliance checklist
- [`docs/12-repo-audit-guide.md`](docs/12-repo-audit-guide.md) - Step-by-step audit procedure

## Enforcement

- **Pre-Release**: Compliance MUST be verified before production release
- **Audit**: Repositories are audited quarterly
- **Non-Compliance**: Blocks production releases until resolved

## Version History

- **1.0.0** (2025-12-14): Initial contract definition

## Questions or Changes

For contract changes, use the `contract-change.yml` issue template in this repository.

