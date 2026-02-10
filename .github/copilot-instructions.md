# Copilot instructions for e2e-demo

## Project purpose
- Repo goal: demonstrate all aspects of DevOps in GitHub (see README).

## Key files
- Start with [README.md](../README.md) for the only documented project context.

## What is *not* discoverable yet
- No source code, build scripts, tests, or workflows are present in the repo.
- No established architecture, module boundaries, or conventions can be inferred.

## Working guidance
- Ask for missing context (language, build/test commands, CI expectations) before making assumptions.
- When adding new files, document them in README so future agents can infer structure.

## C# and Blazor guidance (when introduced)
- Prefer .NET SDK-style projects; keep solutions organized by feature (e.g., `src/App`, `src/App.Client`, `src/App.Server`).
- Use `nullable` and treat warnings as errors in CI; avoid `dynamic` unless interop requires it.
- Favor dependency injection with explicit lifetimes; keep service registration in a single composition root.
- Keep configuration in `appsettings.json` and environment overrides; avoid hardcoding secrets.
- Use async/await end-to-end; avoid blocking calls like `.Result` or `.Wait()`.
- For Blazor components, keep `.razor` markup focused and move logic into `@code` or code-behind when complex.
- Use `@key` for stable list rendering, and dispose `IDisposable` resources in components.
- Keep client/server boundaries clear; validate inputs on the server even if client-side validation exists.
- Use logging and structured exceptions for observability; avoid silent failures or swallowing exceptions.
- Follow .NET naming conventions (PascalCase for types/members, camelCase for parameters/locals) and keep code style consistent.
- Use XML documentation comments for public APIs and complex logic; keep comments up-to-date with code changes.
- For Blazor UI, prefer component-level tests with Playwright for end-to-end scenarios that span multiple layers.
- Use a consistent UI design system (e.g., Bootstrap, Material) and keep styles organized; avoid inline styles.
- For Blazor Server, be mindful of state management and consider using a state container or scoped services to manage UI state across components.

## Testing guidance (when introduced)
- Separate unit, integration, and UI tests into dedicated projects or folders for clear ownership.
- Use fixtures or test-specific DI containers to isolate external dependencies; prefer fakes over live services.
- For Blazor UI tests, prefer component-level tests over end-to-end unless a behavior spans multiple layers.
- Keep test data near the tests (inline builders or small JSON files) to avoid hidden dependencies.
- Use descriptive test names that convey the scenario and expected outcome; avoid generic names like `Test1`.
- Utilize NUnit's features like `[SetUp]`, `[TearDown]`, and `[TestCase]` to keep tests DRY and maintainable.
- Ensure tests are deterministic and can run in parallel; avoid shared state or reliance on external services.
- Aim for high coverage of critical paths, but prioritize meaningful tests over coverage percentage.

## CI/CD guidance (when introduced)
- Use GitHub Actions for CI/CD; start with a simple workflow that builds and tests on push and pull request.
- Keep workflows in `.github/workflows` and name them descriptively (e.g., `build-and-test.yml`).
- Use matrix builds to test against multiple .NET versions or configurations if relevant.
- Store secrets in GitHub Actions secrets and reference them in workflows; avoid hardcoding sensitive information.
- Use caching for dependencies (e.g., NuGet packages) to speed up builds.
- Include steps for code analysis (e.g., SonarCloud) and test reporting to maintain code quality.
- Consider adding a deployment step to GitHub Pages or Azure Static Web Apps for the Blazor app once it's ready.
- Keep workflows focused and modular; avoid monolithic workflows that do too much in one file.
- Publish build artifacts (e.g., test results, coverage reports) for visibility and debugging.
- Use workflow dispatch or workflow templates to allow manual triggering of important workflows (e.g., deployments).
- Document the purpose and expected behavior of each workflow in the README for future agents to understand the CI/CD setup.
- Continuously iterate on the CI/CD setup as the project evolves; start simple and add complexity as needed.
- Publish a badge for build status in the README to provide quick visibility into the health of the main branch.
- Publish a badge for test coverage in the README to encourage maintaining good test coverage as the project grows.
- Publish a badge for code quality (e.g., SonarCloud) in the README to encourage maintaining high code quality as the project grows.
- Publish a badge for deployment status in the README to provide quick visibility into the health of the deployed application once deployment is set up.
- Publish a badge for security vulnerabilities in the README to encourage maintaining a secure codebase as the project grows.
- Publish the build artifacts to GitHub Releases to provide versioned access to build outputs and test results for future agents to reference.