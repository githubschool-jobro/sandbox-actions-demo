# High Performance DevOps Cultures

This guide outlines best practices for establishing a high-performance DevOps culture using GitHub.

## Planning with GitHub Projects

- Use GitHub Projects to organize work into actionable items aligned with team goals
- Link issues and pull requests to project boards for end-to-end visibility
- Use automation to transition issues through workflow states (Backlog → In Progress → In Review → Done)
- Create views by priority, assignee, or milestone to support sprint planning and capacity management
- Leverage project insights to track velocity and identify bottlenecks

## Branching Practices

- Adopt a consistent branching strategy (e.g., trunk-based development or Git Flow)
- Enforce branch naming conventions (e.g., `feature/`, `fix/`, `docs/`) to clarify intent at a glance
- Require branches to be up-to-date with main before merging to reduce conflicts
- Delete merged branches promptly to keep the repository clean
- Protect main branch: require at least one code review and passing CI before merge
- Use short-lived branches (1–3 days) to reduce merge complexity and improve collaboration

## Small Batch Deployments

- Deploy frequently in small, incremental changes to reduce risk and complexity
- Keep changes focused to a single feature or fix; avoid combining unrelated work
- Use trunk-based development to encourage frequent merges to main (at least daily)
- Limit pull requests to a size reviewable in 30 minutes to maintain code quality and velocity
- Ship features in small batches to gather feedback early and pivot quickly

## Copilot Instructions for Team Standards

- Create `.github/copilot-instructions.md` to document project-specific patterns, conventions, and workflows
- Document architecture decisions, file organization, and naming conventions so AI agents apply consistent style
- Include language-specific guidance (e.g., C#/Blazor patterns, async expectations, logging practices)
- Link to key files and examples that exemplify team standards
- Update instructions as conventions evolve; review during retrospectives
- Reference instructions in PR comments when guiding reviewers on expected patterns
- Share `.github/copilot-instructions.md` in team documentation to align human reviewers with AI agent expectations

## Automated Testing & Quality Practices

- Layer testing: unit, integration, contract, and end-to-end tests in CI pipeline
- Run all tests automatically on every commit to catch regressions early
- Maintain test data and environments that closely mirror production
- Aim for high confidence in automated tests to avoid manual testing bottlenecks
- Cover critical business paths and error scenarios; prioritize meaningful tests over coverage percentage
- Use feature flags to test new functionality in production safely without releasing to users

## Quality Gates in Pull Requests

- Require status checks to pass before merging: automated tests, linting, security scans, and type checking
- Configure branch protection rules to enforce PR review policies (minimum reviewers, dismiss stale reviews)
- Use code owners files (`.github/CODEOWNERS`) to automatically assign reviewers based on changed files
- Set up GitHub Actions to run build, test, and coverage jobs on every PR
- Display code coverage, test results, and performance metrics in PR comments for quick feedback
- Fail builds on warnings in CI (e.g., treat compiler warnings as errors) to maintain code quality
- Require passing checks before acknowledging PR approval to prevent accidental merges of failing code

## Approval Gates and CI/CD Triggering

- Use workflow dispatch to allow manual triggering of deployments after approval
- Require explicit approval before deploying to production; store approval records in Git
- Leverage GitHub environments with deployment protection rules to gate production deployments
- Use pull request reviews as the primary approval mechanism; require authorized reviewers
- Implement conditional workflows: trigger staging deployments on PR approval, production on main after merge
- Post deployment status and logs back to PRs for full visibility into deployment lifecycle
- Consider using action approvals (e.g., with `environment` in workflows) to enforce approval workflows at deploy time
- Document approval authority and escalation paths in team runbooks

## Feature Flags & Safe Deployments

- Use feature flags to decouple deployment from feature release (enables frequent deployments with reduced risk)
- Enable/disable features in production without redeployment to quickly respond to issues
- Gradually roll out features via canary or blue-green deployments to catch issues early
- Roll back features independently of code rollbacks to minimize blast radius
- Clean up feature flags once a feature is stable and broadly rolled out

## Infrastructure as Code (IaC)

- Manage all infrastructure (networking, compute, databases, monitoring) as code in Git
- Test infrastructure changes in lower environments before production
- Enable rapid, reproducible deployments and emergency recovery (MTTR)
- Version and review infrastructure changes like application code through pull requests
- Use IaC to enforce consistent naming, tagging, and configuration standards across environments

## Monitoring, Observability & Incident Response

- Implement comprehensive logging, metrics, and tracing to detect failures quickly (enables rapid MTTR)
- Set up alerting on critical business metrics and system health, not just infrastructure
- Create runbooks and incident response playbooks for common failures
- Practice blameless postmortems to learn from incidents; document findings into preventive actions
- Automate incident triage and routing to reduce response time
- Build feedback loops: use production metrics to inform development priorities and risk assessments

## Documentation & Knowledge Sharing

- Maintain runbooks, architecture decision records (ADRs), and troubleshooting guides
- Document on-call procedures, escalation paths, and common failure scenarios
- Keep documentation close to code (in `.github/`, `/docs/`, or adjacent READMEs) to stay current
- Share learnings from incidents and retrospectives across the team
- Update documentation as workflows and standards evolve; treat docs as a team responsibility

## Summary

A high-performance DevOps culture relies on continuous flow: clear planning (GitHub Projects) → small, frequent changes (branching, batch deployments) → rigorous quality (automated testing, gates) → safe deployment (feature flags, approvals, IaC) → rapid feedback (monitoring, incident response). Invest in documentation—especially `.github/copilot-instructions.md`—and automate enforcement via GitHub Actions and branch policies to scale consistency. Measure success using DORA metrics: track Deployment Frequency, Lead Time, MTTR, and Change Failure Rate to identify areas for improvement.
