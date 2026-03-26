# Managed Global Claude Rules

This file is the managed global standards file for Claude Code agents operating in this project.

Project-specific rules belong in the root `CLAUDE.md`.
Do not duplicate project context or repository-specific details here unless they are intended to apply across many repositories.

---

## 1. Purpose

This file defines working rules, constraints, and conventions for Claude Code agents operating in this repository.

It exists to:
- Reduce repeated mistakes
- Standardise engineering decisions
- Improve output quality over time
- Enable safe autonomous execution

Treat this file as persistent memory for the agent system, not documentation for humans.

---

## 2. Core Principles

### 2.1 Plan Before Code
- ALWAYS begin in planning mode
- Do not implement until the plan is coherent and complete
- Every plan must identify:
  - scope
  - files likely to change
  - dependencies
  - risks and assumptions
  - verification steps
  - rollback impact if relevant

### 2.2 Correctness Over Speed
- Prefer accurate, reviewable output over rapid but fragile output
- Avoid speculative edits
- Avoid “fix-forward” workflows caused by careless initial changes

### 2.3 Small, Isolated Changes
- Prefer narrowly scoped tasks
- Avoid mixing refactors with feature work unless required
- Keep diffs easy to review

### 2.4 Verify Everything
Claude must verify work using the relevant checks for the stack in use:
- restore
- build
- test
- lint / formatting validation
- runtime smoke checks where appropriate

If something cannot be verified:
- state that clearly
- explain why
- propose the exact next validation step

### 2.5 Never Assume Success
- Never claim code works without evidence
- Never state tests passed unless they were actually run
- Surface uncertainty explicitly

---

## 3. Safety Rules

### 3.1 Production and Secret Safety
- NEVER access, print, move, or modify secrets unless explicitly instructed
- NEVER commit secrets, tokens, connection strings, certificates, or `.env` contents
- NEVER deploy, rotate secrets, change infrastructure, or alter production settings unless explicitly instructed

### 3.2 File Safety
- Do not delete files unless explicitly instructed
- Prefer minimal diffs over large rewrites
- Preserve existing project structure unless restructuring is required

### 3.3 Command Safety
Only run commands that are relevant, bounded, and safe.

Avoid destructive commands unless explicitly approved, including:
- `rm -rf`
- force resets
- schema-destructive database commands
- broad file rewrites without backup or clear justification

---

## 4. General Coding Standards

### 4.1 Follow the Repository
- Follow existing project conventions first
- Match naming, structure, test style, and dependency choices already in the repo
- Do not introduce new frameworks or libraries unless justified

### 4.2 Readability
Prefer:
- small composable functions
- explicit inputs and outputs
- low surprise code
- maintainable abstractions

Avoid:
- hidden side effects
- unnecessary indirection
- speculative abstraction
- “clever” code that reduces clarity

### 4.3 Naming
- Use descriptive names
- Avoid vague names like `helper`, `data`, `temp`, `misc`
- Keep naming consistent with .NET and repository conventions

### 4.4 Comments
- Explain why, not what
- Add comments only where intent is not obvious from the code
- Keep comments current with the implementation

---

## 5. .NET-Specific Rules

### 5.1 .NET General
- Prefer the existing target framework and SDK conventions already used by the repository
- Do not upgrade target frameworks, package versions, or SDK assumptions unless explicitly asked
- Use the existing solution and project layout unless there is a strong reason not to

### 5.2 C# Style
- Follow standard C# conventions:
  - PascalCase for public members and types
  - camelCase for locals and parameters
  - `_camelCase` for private readonly fields when that is the project convention
- Prefer clear types over overly terse code
- Use `var` only where the type is obvious from the right-hand side or required by local style
- Avoid deeply nested logic; extract private methods where it improves readability

### 5.3 Nullability and Defensive Coding
- Respect nullable reference types if enabled
- Do not suppress nullability warnings without a good reason
- Validate external inputs at boundaries
- Prefer explicit handling over null-forgiving operators

### 5.4 Async / Await
- Use async all the way where appropriate
- Do not block on async with `.Result` or `.Wait()`
- Accept `CancellationToken` in I/O, HTTP, background, and long-running flows where appropriate
- Propagate cancellation instead of ignoring it

### 5.5 Dependency Injection
- Use the repository’s existing DI pattern
- Prefer constructor injection
- Avoid service locators
- Register services with sensible lifetimes:
  - Singleton only for stateless/shared-safe services
  - Scoped for request-bound dependencies
  - Transient when appropriate and lightweight

### 5.6 ASP.NET Core
For web apps and APIs:
- Keep controllers/endpoints thin
- Put business logic into services, handlers, or domain components
- Validate request models
- Return appropriate status codes
- Do not leak internal exception details to clients
- Respect authentication and authorization patterns already present

### 5.7 Entity Framework / Data Access
If EF Core is used:
- Prefer explicit queries over accidental over-fetching
- Avoid N+1 patterns
- Use projections for read models where appropriate
- Do not introduce lazy-loading surprises unless already established
- Keep migrations focused and reviewable
- Never modify historical migrations unless explicitly instructed

### 5.8 Logging
- Use structured logging
- Do not log secrets, full PANs, credentials, tokens, or sensitive personal data
- Keep log messages useful for operations and debugging
- Prefer contextual properties over string-only logs

### 5.9 Configuration
- Use options/config binding patterns already present in the solution
- Do not hardcode environment-specific values
- Do not add secrets to appsettings files
- Keep configuration keys consistent and grouped logically

### 5.10 Testing in .NET Repos
- Add or update tests for behavioural changes
- Prefer the project’s established test framework and assertion style
- Keep unit tests deterministic and fast
- Use integration tests only where they provide real value
- Do not silently change snapshots/golden files without checking whether the behavioural change is intentional

### 5.11 Formatting and Analysis
Before finalising, run the applicable checks where available:
- `dotnet restore`
- `dotnet build`
- `dotnet test`
- `dotnet format --verify-no-changes`
- analyzers defined by the solution or CI

If a monorepo or large solution makes full validation too expensive, run the narrowest meaningful scope and say exactly what was and was not checked.

### 5.12 Security-Sensitive Repositories
If the repository handles compliance, payments, identity, audit, or security workflows:
- prefer explicit validation and auditability
- preserve traceability
- do not weaken access control
- do not bypass approval or evidence flows
- treat sensitive data minimisation as a design requirement

---

## 6. Workflow Conventions

### 6.1 Standard Flow
1. Inspect relevant files
2. Produce a plan
3. Implement narrowly
4. Run verification
5. Refine if needed
6. Summarise changes and residual risks

### 6.2 PR / Change Summary Behaviour
When preparing a summary, include:
- what changed
- why it changed
- files touched
- validation performed
- outstanding risks or follow-ups

### 6.3 Commit Guidance
Use concise, scoped commits when asked to prepare commit messages.

Suggested format:
`type(scope): concise description`

Examples:
- `feat(api): add validation for evidence upload`
- `fix(auth): prevent null role mapping in claims transform`
- `refactor(core): simplify scope evaluation service`

---

## 7. Subagent / Command Use

Use reusable commands where possible for repeatable workflows.

Preferred command groups:
- `/plan`
- `/implement`
- `/test`
- `/review`
- `/commit`

Commands should:
- reduce prompt repetition
- enforce repository standards
- produce predictable outputs

---

## 8. Common Failure Modes

Watch for:
- editing unrelated files
- changing public behaviour without tests
- skipping validation
- introducing framework drift
- adding unnecessary packages
- mixing formatting noise with logic changes
- making .NET changes that ignore DI, nullability, logging, or cancellation patterns

Mitigations:
- inspect diff before finalising
- run the smallest meaningful verification suite
- state assumptions clearly
- keep changes scoped

---

## 9. Continuous Improvement Rule

Whenever Claude makes a mistake, needs correction, or produces suboptimal output:
- add a short, durable rule to this file if the lesson is likely to recur

This file should evolve with the repository.

---

## 10. Default Commands

Use these defaults unless the repository specifies otherwise:

```yaml
language: "C# / .NET"
restore_command: "dotnet restore"
build_command: "dotnet build"
test_command: "dotnet test"
format_check_command: "dotnet format --verify-no-changes"