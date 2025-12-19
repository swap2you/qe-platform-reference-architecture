# QE Platform Onboarding Playbook

## Overview

This playbook guides new team members through the QE Platform Reference Architecture, ensuring they understand both the technical implementation and the quality philosophy that drives it.

## Learning Objectives

By completing this playbook, you will:

- Understand the platform's quality-first approach
- Know how to implement quality gates in your projects
- Be able to generate and interpret quality reports
- Follow the platform's standards and best practices
- Contribute effectively to platform improvements

## Prerequisites

Before starting, ensure you have:

- Access to the platform repository
- Development environment set up (Node.js, npm/yarn)
- Basic understanding of testing frameworks
- GitHub account with appropriate permissions

## Week 1: Foundation & Philosophy

### Day 1-2: Platform Overview

**Reading (2 hours)**

- Read the [README](../README.md)
- Review the [Architecture Decision Records](adr/README.md)
- Understand the [Platform Contract](06-platform-contract.md)

**Exercise (1 hour)**

- Clone the repository
- Run `npm install`
- Execute `npm test` and observe the output
- Review the generated reports in `allure-report/`

**Checkpoint Questions**

- What are the three main quality gates?
- Why does the platform emphasize "doc-first" approach?
- What happens when a quality gate fails?

### Day 3-4: Local Development Setup

**Hands-on (4 hours)**

- Create a test branch

```bash
git checkout -b onboarding/your-name
```

- Add a simple test file in `tests/examples/`
- Run quality gates locally
- Generate Allure report
- Review all generated artifacts

**Exercise Tasks**

1. Create a new test file: `tests/examples/onboarding-test.spec.js`

```javascript
import { test, expect } from '@playwright/test';

test.describe('Onboarding Exercise', () => {
  test('should demonstrate basic assertions', async () => {
    expect(1 + 1).toBe(2);
  });

  test('should show test metadata', async () => {
    await test.step('Setup', async () => {
      // Setup code
    });
    
    await test.step('Execution', async () => {
      expect(true).toBeTruthy();
    });
    
    await test.step('Verification', async () => {
      expect(false).toBeFalsy();
    });
  });
});
```

2. Run the test and verify it passes
3. Generate Allure report
4. Find your test in the report
5. Take a screenshot and share with your mentor

**Checkpoint**

- Can you run tests locally?
- Do you understand the test structure?
- Can you navigate the Allure report?

### Day 5: Documentation Standards

**Reading (2 hours)**

- Study the [Documentation Guide](03-documentation-guide.md)
- Review existing ADRs for structure examples
- Read about Mermaid diagrams

**Exercise (2 hours)**

Create a personal learning log document:

```markdown
# My QE Platform Learning Journey

## Week 1: Foundation

### What I Learned
- Key concept 1
- Key concept 2

### Questions & Clarifications
- Question 1
- Question 2

### Action Items
- [ ] Item 1
- [ ] Item 2
```

**Checkpoint**

- Do you understand the documentation structure?
- Can you create Mermaid diagrams?
- Have you reviewed markdown best practices?

## Week 2: Practical Implementation

### Day 6-7: Test Development

**Learning (2 hours)**

- Review [Test Development Guide](04-test-development.md)
- Study existing test examples
- Understand test organization patterns

**Exercise (4 hours)**

Create a complete test suite:

1. Choose a simple API or web page
2. Write at least 3 test cases covering:
   - Happy path
   - Error handling
   - Edge cases
3. Add proper test metadata (tags, descriptions)
4. Include step-by-step reporting

**Quality Criteria**

- Tests must pass quality gates
- Code must be documented
- Allure report must show clear test steps
- Tests must be tagged appropriately

### Day 8-9: Quality Gates Deep Dive

**Hands-on (4 hours)**

1. Intentionally fail each quality gate:
   - Test Execution Gate (write a failing test)
   - Evidence Collection Gate (break report generation)
   - Platform Compliance Gate (violate standards)

2. Observe the failures
3. Fix each issue
4. Document what you learned

**Exercise: Create Quality Gate Report**

Document your findings:

```markdown
# Quality Gate Investigation

## Test Execution Gate
- How I broke it: ...
- What happened: ...
- How I fixed it: ...
- Key learning: ...

## Evidence Collection Gate
- How I broke it: ...
- What happened: ...
- How I fixed it: ...
- Key learning: ...

## Platform Compliance Gate
- How I broke it: ...
- What happened: ...
- How I fixed it: ...
- Key learning: ...
```

### Day 10: CI/CD Integration

**Learning (3 hours)**

- Review `.github/workflows/` configurations
- Understand the CI/CD pipeline
- Study how quality gates run in CI

**Exercise (2 hours)**

1. Create a pull request with your onboarding work
2. Watch the CI/CD pipeline execute
3. Review the automated checks
4. Address any failures
5. Get your PR reviewed

**Checkpoint**

- Do you understand the CI/CD flow?
- Can you interpret pipeline results?
- Have you successfully created a PR?

## Week 3: Advanced Topics & Real Work

### Day 11-12: Reporting & Evidence

**Deep Dive (4 hours)**

- Study the [Reporting Guide](05-evidence-and-reporting.md)
- Explore Allure features:
  - Test steps
  - Attachments
  - Categories
  - History
  - Trends

**Exercise: Enhanced Test Suite**

Enhance your previous test suite with:

1. Screenshot attachments
2. Custom step reporting
3. Test categorization
4. Environment information
5. Test data attachments

**Example Enhancement**

```javascript
import { test } from '@playwright/test';
import { allure } from 'allure-playwright';

test('enhanced test with reporting', async ({ page }) => {
  await allure.epic('Onboarding');
  await allure.feature('Advanced Reporting');
  await allure.story('Enhanced Evidence Collection');
  
  await test.step('Navigate and capture', async () => {
    await page.goto('https://example.com');
    const screenshot = await page.screenshot();
    await allure.attachment('page-screenshot', screenshot, 'image/png');
  });
  
  await test.step('Collect environment data', async () => {
    const envData = {
      url: page.url(),
      timestamp: new Date().toISOString(),
      viewport: page.viewportSize()
    };
    await allure.attachment('environment', JSON.stringify(envData, null, 2), 'application/json');
  });
});
```

### Day 13-14: Platform Compliance & Best Practices

**Study (3 hours)**

- Review [Platform Contract Compliance](11-platform-contract-compliance.md)
- Study [Repository Audit Guide](12-repo-audit-guide.md)
- Understand compliance requirements

**Exercise: Compliance Audit**

1. Create feature branch

```bash
git checkout -b feature/compliance-exercise
```

2. Audit your onboarding work against platform contract
3. Create a compliance checklist
4. Fix any non-compliance issues
5. Document your compliance status

**Compliance Checklist Template**

```markdown
# Platform Compliance Checklist

## Quality Gates
- [ ] All tests pass
- [ ] Reports generated successfully
- [ ] Platform standards followed

## Documentation
- [ ] Code is documented
- [ ] Tests have descriptions
- [ ] ADRs reviewed (if applicable)

## Evidence Collection
- [ ] Allure reports generated
- [ ] Test artifacts preserved
- [ ] Screenshots/attachments included

## Best Practices
- [ ] Code follows conventions
- [ ] Tests are maintainable
- [ ] No hardcoded values
```

### Day 15: Real Project Assignment

**Project Work (Full Day)**

You'll be assigned a real task from the backlog:

1. Review Allure report

```bash
git checkout -b feature/your-first-task
```

2. Understand requirements
3. Plan your approach
4. Implement with quality gates
5. Create PR with proper documentation
6. Get team review

**Success Criteria**

- All quality gates pass
- Code review approved
- Documentation complete
- Tests provide clear evidence
- PR merged successfully

## Week 4: Contribution & Mastery

### Day 16-17: Platform Improvement

**Learning (2 hours)**

- Review [Platform Development](08-platform-development.md)
- Understand contribution guidelines
- Study improvement proposals

**Exercise: Propose an Improvement**

1. Identify something that could be better
2. Create an ADR draft
3. Discuss with team
4. Implement if approved

**ADR Template for Your Proposal**

```markdown
# ADR XXX: [Your Improvement Title]

## Status
Proposed

## Context
What problem are you solving?

## Decision
What do you propose?

## Consequences
What are the impacts?
```

### Day 18-19: Knowledge Sharing

**Preparation (4 hours)**

Prepare a presentation covering:

1. Your onboarding journey
2. Key learnings
3. Challenges faced
4. Suggestions for improvement
5. Demo of your work

**Presentation Structure**

- Introduction (5 min)
- Technical deep dive (15 min)
- Demo (10 min)
- Q&A (10 min)

### Day 20: Assessment & Reflection

**Assessment (2 hours)**

Complete the onboarding assessment:

1. Access Allure report

```bash
npm run test:assessment
```

2. Build and review the report
3. Submit your work

**Reflection (2 hours)**

Create a retrospective document:

```markdown
# Onboarding Retrospective

## What Worked Well

- Item 1
- Item 2

## What Could Be Better
- Item 1
- Item 2

## Action Items for the Team
- [ ] Improvement 1
- [ ] Improvement 2

## Personal Growth Areas
- Area 1
- Area 2
```

## Ongoing Learning

### Monthly Activities

- Review new ADRs
- Participate in platform discussions
- Share knowledge with new team members
- Contribute to platform improvements

### Quarterly Goals

- Master advanced testing techniques
- Contribute significant platform enhancement
- Mentor new team members
- Present at team meetings

## Resources

### Internal Documentation

- [Platform Contract](06-platform-contract.md)
- [Test Development Guide](04-test-development.md)
- [Reporting Guide](05-evidence-and-reporting.md)
- [All ADRs](adr/)

### External Resources

- [Playwright Documentation](https://playwright.dev)
- [Allure Framework](https://docs.qameta.io/allure/)
- [GitHub Actions](https://docs.github.com/en/actions)
- [Mermaid Diagrams](https://mermaid-js.github.io/)

## Getting Help

### Support Channels

- Team Slack: `#qe-platform`
- Office Hours: Daily 10-11 AM
- Mentor: Assigned on Day 1
- Documentation: This repository

### Escalation Path

1. Check documentation
2. Ask your mentor
3. Team Slack channel
4. Team lead
5. Platform maintainers

## Success Indicators

You've successfully completed onboarding when you can:

- [ ] Run quality gates independently
- [ ] Create compliant test suites
- [ ] Generate and interpret reports
- [ ] Contribute to platform improvements
- [ ] Help onboard others
- [ ] Make decisions aligned with platform philosophy

## Certification

Upon completion, you'll receive:

- Onboarding completion badge
- Access to advanced platform features
- Invitation to platform working group
- Mentorship opportunities

## Feedback

We continuously improve this playbook. Please submit feedback via:

- PR to update this document
- Issues in the repository
- Direct feedback to platform team

---

**Welcome to the QE Platform team! We're excited to have you on this quality journey.**
