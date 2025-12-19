# Repository Audit Guide

This guide provides a step-by-step procedure for auditing a repository implementing the QE Platform Contract.

## Audit Scope

An audit verifies that a repository:

- Implements required standards from [`CONTRACT.md`](../CONTRACT.md)
- Follows governance policies
- Generates required artifacts
- Maintains required documentation

## Pre-Audit Preparation

1. **Identify Repository**: Note the repository name and URL
2. **Review Contract**: Familiarize yourself with [`CONTRACT.md`](../CONTRACT.md)
3. **Access Repository**: Ensure you have read access
4. **Prepare Checklist**: Use [`docs/11-platform-contract-compliance.md`](11-platform-contract-compliance.md)

## Audit Procedure

### Phase 1: Repository Structure Audit

**Objective**: Verify repository structure matches required pattern.

**Steps**:

1. **Check Root Structure**:
   - [ ] `README.md` exists
   - [ ] `.github/` folder exists
   - [ ] `src/test/` or equivalent exists
   - [ ] `docs/` folder exists

2. **Check .github Structure**:
   - [ ] `.github/workflows/` exists
   - [ ] `.github/CODEOWNERS` exists
   - [ ] `.github/PULL_REQUEST_TEMPLATE.md` exists

3. **Check Test Structure**:
   - [ ] Test source code follows required structure
   - [ ] Smoke tests are separated (folder or tag)
   - [ ] Regression tests are separated (folder or tag)
   - [ ] Test resources are organized

4. **Check Documentation Structure**:
   - [ ] `docs/README.md` exists
   - [ ] `docs/test-strategy.md` exists
   - [ ] `docs/reporting-guide.md` exists

**Document Findings**: Note any structural deviations.

### Phase 2: CI/CD Workflows Audit

**Objective**: Verify required workflows exist and function correctly.

**Steps**:

1. **PR Gate: Smoke Tests**:
   - [ ] Open `.github/workflows/smoke-tests.yml`
   - [ ] Verify trigger: `pull_request`
   - [ ] Verify test execution command uses smoke tags
   - [ ] Verify Allure report generation
   - [ ] Verify artifact upload
   - [ ] Check recent PRs: Do smoke tests run?
   - [ ] Check recent PRs: Are PRs blocked on failure?

2. **Nightly Gate: Regression Tests**:
   - [ ] Open `.github/workflows/regression-tests.yml`
   - [ ] Verify trigger: `schedule` (cron)
   - [ ] Verify test execution command uses regression tags
   - [ ] Verify Allure report generation
   - [ ] Verify artifact upload
   - [ ] Verify artifact retention (30 days)
   - [ ] Check Actions tab: Do nightly runs exist?
   - [ ] Check Actions tab: Are artifacts retained?

3. **Workflow Execution History**:
   - [ ] Review last 10 workflow runs
   - [ ] Verify success rate > 95%
   - [ ] Verify execution times are within limits
   - [ ] Verify artifacts are generated

**Document Findings**: Note workflow issues, execution problems, or missing configurations.

### Phase 3: Tagging Taxonomy Audit

**Objective**: Verify tests are properly tagged.

**Steps**:

1. **Test Type Tags**:
   - [ ] Search for `@smoke` or equivalent in test files
   - [ ] Search for `@regression` or equivalent in test files
   - [ ] Verify tags are used in CI workflows
   - [ ] Count: How many smoke tests? (should be < 20)
   - [ ] Count: How many regression tests? (should cover features)

2. **Feature Tags**:
   - [ ] Review test files for feature tags
   - [ ] Verify feature tags are consistent
   - [ ] Verify feature tags are documented

3. **Priority Tags**:
   - [ ] Search for `@critical` or equivalent
   - [ ] Verify critical tests are identified
   - [ ] Verify priority tags are documented

**Document Findings**: Note tagging inconsistencies or missing tags.

### Phase 4: Reporting Artifacts Audit

**Objective**: Verify Allure evidence bundles are generated correctly.

**Steps**:

1. **Allure Report Generation**:
   - [ ] Check recent workflow runs for Allure artifacts
   - [ ] Download and open an Allure report
   - [ ] Verify report includes test results
   - [ ] Verify report includes test history
   - [ ] Verify report includes screenshots (UI tests)
   - [ ] Verify report includes logs (API tests)

2. **Artifact Contents**:
   - [ ] Check artifact structure
   - [ ] Verify test execution summary exists
   - [ ] Verify metadata is included (timestamp, environment, versions)
   - [ ] Verify screenshots are present (on failures, UI tests)
   - [ ] Verify logs are present

3. **Artifact Retention**:
   - [ ] Check artifact retention settings
   - [ ] Verify PR artifacts are retained (7 days)
   - [ ] Verify nightly artifacts are retained (30 days)
   - [ ] Verify release artifacts are retained (90 days)

**Document Findings**: Note missing artifacts, incomplete reports, or retention issues.

### Phase 5: Documentation Audit

**Objective**: Verify required documentation exists and is accurate.

**Steps**:

1. **README.md**:
   - [ ] Read README.md
   - [ ] Verify repository purpose is documented
   - [ ] Verify contract compliance is referenced
   - [ ] Verify quick start guide exists
   - [ ] Verify CI/CD badges are present
   - [ ] Verify test structure is documented
   - [ ] Verify reporting access is documented
   - [ ] Verify contributing guidelines exist

2. **docs/ Folder**:
   - [ ] Read `docs/README.md`
   - [ ] Read `docs/test-strategy.md`
   - [ ] Read `docs/reporting-guide.md`
   - [ ] Verify documentation is accurate
   - [ ] Verify documentation is up-to-date
   - [ ] Verify links work

**Document Findings**: Note missing documentation, outdated content, or broken links.

### Phase 6: Governance Audit

**Objective**: Verify governance standards are enforced.

**Steps**:

1. **Branch Strategy**:
   - [ ] Check repository settings: Is `main` protected?
   - [ ] Check branch protection rules
   - [ ] Review recent PRs: Are PRs required?
   - [ ] Review recent PRs: Do PRs require approvals?

2. **PR Template**:
   - [ ] Open `.github/PULL_REQUEST_TEMPLATE.md`
   - [ ] Verify template includes required fields
   - [ ] Review recent PRs: Do PRs use template?
   - [ ] Review recent PRs: Are required fields filled?

3. **CODEOWNERS**:
   - [ ] Open `.github/CODEOWNERS`
   - [ ] Verify default owner is defined
   - [ ] Verify critical paths have owners (if applicable)
   - [ ] Check: Are CODEOWNERS reviews enforced?

**Document Findings**: Note governance gaps or enforcement issues.

### Phase 7: Flaky Test Quarantine Policy Audit

**Objective**: Verify flaky test management policy is implemented.

**Steps**:

1. **Flaky Test Detection**:
   - [ ] Review test execution history for flaky patterns
   - [ ] Check: Are flaky tests identified?
   - [ ] Check: Is flaky test rate < 5%?

2. **Flaky Test Management**:
   - [ ] Check: Is there a process for handling flaky tests?
   - [ ] Check: Are flaky tests quarantined?
   - [ ] Check: Are flaky tests tracked in issues?
   - [ ] Check: Are flaky tests fixed or removed?

3. **Documentation**:
   - [ ] Verify flaky test policy is documented
   - [ ] Verify flaky test process is followed

**Document Findings**: Note flaky test issues or policy gaps.

## Audit Report

After completing all phases, create an audit report:

1. **Summary**: Overall compliance status
2. **Findings**: List of issues found
3. **Recommendations**: Actions to achieve compliance
4. **Timeline**: When compliance should be achieved

## Audit Frequency

- **Before Release**: Full audit required
- **Quarterly**: Regular compliance audit
- **After Major Changes**: Verify compliance maintained

## Audit Checklist Template

Use this template for each audit:

```text
Repository: [name]
Audit Date: [date]
Auditor: [name]

Phase 1: Repository Structure - [ ] Pass / [ ] Fail
Phase 2: CI/CD Workflows - [ ] Pass / [ ] Fail
Phase 3: Tagging Taxonomy - [ ] Pass / [ ] Fail
Phase 4: Reporting Artifacts - [ ] Pass / [ ] Fail
Phase 5: Documentation - [ ] Pass / [ ] Fail
Phase 6: Governance - [ ] Pass / [ ] Fail
Phase 7: Flaky Test Policy - [ ] Pass / [ ] Fail

Overall Status: [ ] Compliant / [ ] Non-Compliant

Issues Found: [list]
Recommendations: [list]
```

## Questions

For audit questions, create an issue using the `contract-change.yml` template.
