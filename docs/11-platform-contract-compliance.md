# Platform Contract Compliance Checklist

Use this checklist to verify that your repository complies with the QE Platform Contract defined in [`CONTRACT.md`](../CONTRACT.md).

## Repository Structure

- [ ] Repository folder structure matches the required pattern
- [ ] `README.md` exists and references this contract
- [ ] `.github/` folder exists with required workflows
- [ ] `docs/` folder exists with required documentation
- [ ] Test source code follows required structure

## CI/CD Quality Gates

### PR Gate: Smoke Tests

- [ ] `.github/workflows/smoke-tests.yml` exists
- [ ] Workflow triggers on `pull_request` events
- [ ] Tests are tagged with `@smoke` or equivalent
- [ ] Execution time is < 10 minutes
- [ ] PR merge is blocked on smoke test failure
- [ ] Allure results are uploaded as artifacts
- [ ] Workflow runs successfully on test PR

### Nightly Gate: Regression Tests

- [ ] `.github/workflows/regression-tests.yml` exists
- [ ] Workflow is scheduled (cron-based)
- [ ] Tests are tagged with `@regression` or equivalent
- [ ] Execution time is < 60 minutes
- [ ] Allure results are uploaded as artifacts
- [ ] Artifacts are retained for 30 days minimum

### Artifact Retention

- [ ] Allure test results are uploaded
- [ ] Test execution logs are uploaded
- [ ] Screenshots are uploaded (UI tests, on failure)
- [ ] Artifact retention periods are configured correctly
- [ ] Artifacts are accessible after execution

## Tagging Taxonomy

### Test Type Tags

- [ ] All tests have test type tags (`@smoke`, `@regression`, etc.)
- [ ] Tags are used correctly in CI workflows
- [ ] Tag usage is documented

### Feature Tags

- [ ] Tests are tagged by feature/component
- [ ] Feature tags are consistent across the repository
- [ ] Feature tags are documented

### Priority Tags

- [ ] Critical tests are tagged with `@critical`
- [ ] Priority tags are used appropriately
- [ ] Priority tags are documented

## Reporting Standard: Allure Evidence Bundle

- [ ] Allure reports are generated for every test execution
- [ ] Reports include test execution results
- [ ] Reports include test history and trends
- [ ] Screenshots are included (UI tests, on failure)
- [ ] Request/response logs are included (API tests)
- [ ] Performance metrics are included (performance tests)
- [ ] Test execution summary (JSON/XML) is generated
- [ ] Metadata (timestamp, environment, versions) is included
- [ ] Reports are accessible and linkable

## Documentation Set

### README.md

- [ ] Repository purpose is documented
- [ ] Contract compliance is referenced (link to CONTRACT.md)
- [ ] Quick start guide exists
- [ ] CI/CD status badges are present
- [ ] Test structure is documented
- [ ] Reporting access is documented
- [ ] Contributing guidelines exist

### /docs Folder

- [ ] `docs/README.md` exists (documentation index)
- [ ] `docs/test-strategy.md` exists (test strategy)
- [ ] `docs/reporting-guide.md` exists (reporting standards)
- [ ] Documentation is up-to-date and accurate

## Governance

### Branch Strategy

- [ ] Branch strategy is documented
- [ ] `main` branch is protected
- [ ] PRs are required for all changes
- [ ] PRs must pass smoke tests before merge
- [ ] At least one approval is required

### PR Template

- [ ] `.github/PULL_REQUEST_TEMPLATE.md` exists
- [ ] Template includes description field
- [ ] Template includes test execution results field
- [ ] Template includes Allure report link field
- [ ] Template includes public-safe check
- [ ] Template includes documentation update check
- [ ] PRs use the template

### CODEOWNERS

- [ ] `.github/CODEOWNERS` file exists
- [ ] Default owner is defined
- [ ] Critical paths have specific owners (if applicable)
- [ ] Review requirements are enforced

## Definition of Done for Compliance

A repository is considered **compliant** when:

1. ✅ All checklist items above are checked
2. ✅ Smoke tests pass on every PR
3. ✅ Nightly regression tests run successfully
4. ✅ Allure reports are generated and accessible
5. ✅ Required documentation exists and is accurate
6. ✅ Governance standards are enforced
7. ✅ Audit has been completed and documented (see [`docs/12-repo-audit-guide.md`](12-repo-audit-guide.md))

## Non-Compliance Actions

If a repository is non-compliant:

1. **Identify gaps**: Use this checklist to identify missing items
2. **Create issue**: Use the `contract-change.yml` template to track compliance work
3. **Prioritize fixes**: Address blocking items first (PR gates, artifact retention)
4. **Verify compliance**: Re-run checklist after fixes
5. **Document**: Update compliance status in repository README

## Compliance Verification Frequency

- **Before Release**: Compliance MUST be verified
- **Quarterly**: Full compliance audit
- **After Major Changes**: Verify compliance is maintained

## Questions

For questions about compliance, create an issue using the `contract-change.yml` template.

