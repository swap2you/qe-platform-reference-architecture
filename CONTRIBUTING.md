# Contributing to QE Platform Reference Architecture

Thank you for your interest in contributing to this reference architecture! This document provides guidelines for contributing.

## Documentation-First Approach

This repository is **documentation-first**. Contributions should:
- Focus on improving documentation clarity and completeness
- Maintain public-safe, generic content (no proprietary information)
- Include Mermaid diagrams for workflows and processes
- Follow the existing documentation structure

## How to Contribute

### Reporting Issues

1. Use the [issue templates](.github/ISSUE_TEMPLATE/) when creating issues
2. For bugs in documentation, use the bug report template
3. For new documentation or improvements, use the feature request template

### Making Changes

1. **Fork the repository**
2. **Create a branch** from `main`:
   ```bash
   git checkout -b docs/your-feature-name
   ```
3. **Make your changes**:
   - Follow existing markdown formatting
   - Include Mermaid diagrams where appropriate
   - Ensure all links are valid
   - Keep content generic and public-safe
4. **Test locally**:
   - Run markdown linting (if available)
   - Verify Mermaid diagrams render correctly
   - Check all links
5. **Commit your changes**:
   ```bash
   git commit -m "docs: description of your changes"
   ```
6. **Push to your fork**:
   ```bash
   git push origin docs/your-feature-name
   ```
7. **Create a Pull Request** using the PR template

## Documentation Standards

### Markdown Formatting

- Use proper heading hierarchy (H1 for page title, H2 for major sections, etc.)
- Include table of contents for documents longer than 500 lines
- Use code blocks with language identifiers
- Include links to related documentation

### Mermaid Diagrams

- Place Mermaid code blocks in markdown files
- Use descriptive titles for diagrams
- Keep diagrams focused and readable
- Reference diagram files in [`docs/diagrams/mermaid-snippets.md`](docs/diagrams/mermaid-snippets.md) if reusable

### Content Guidelines

- **Public-Safe**: No internal URLs, proprietary names, or confidential information
- **Generic**: Use placeholder names (e.g., "your-org", "your-service")
- **Concise**: Be thorough but avoid unnecessary verbosity
- **Actionable**: Provide clear, implementable guidance

## Pull Request Process

1. Ensure your PR description follows the template
2. Link to related issues
3. Ensure all GitHub Actions checks pass (markdown lint, link validation)
4. Request review from CODEOWNERS
5. Address review feedback promptly

## Review Criteria

PRs will be reviewed for:
- **Accuracy**: Information is correct and up-to-date
- **Clarity**: Documentation is easy to understand
- **Completeness**: All necessary information is included
- **Consistency**: Follows existing patterns and structure
- **Public-Safety**: No proprietary or confidential information

## Questions?

If you have questions about contributing, please open an issue with the `question` label.

Thank you for contributing to the QE Platform Reference Architecture!

