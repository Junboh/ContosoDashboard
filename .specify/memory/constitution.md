<!--
Sync Impact Report
Version change: n/a → 1.0.0
Modified principles: added 5 project-specific principles
Added sections: Project Constraints and Standards; Development Workflow and Quality Gates
Removed sections: none
Templates reviewed: 
- ✅ .specify/templates/constitution-template.md
- ✅ .specify/templates/plan-template.md
- ✅ .specify/templates/spec-template.md
- ✅ .specify/templates/tasks-template.md
- ✅ .github/copilot-instructions.md
- ✅ .specify/extensions.yml
Follow-up TODOs: none
-->

# ContosoDashboard Constitution

## Core Principles

### I. Training-Safe Data and Authentication
The ContosoDashboard codebase MUST preserve a training-safe environment by using mock or local credentials only, never storing production secrets, and never requiring real identity provider accounts for the default learning flow. All data access MUST be constrained to the local SQLite database and seeded example data, with no external database or cloud authentication required for normal training execution.

### II. Clear Separation of UI, Services, and Data
Application behavior MUST be organized so that UI pages handle rendering and interaction, services encapsulate business rules, and the data layer defines persistence. This separation MUST make services and data models independently testable and maintainable without coupling business logic into page markup.

### III. Secure-by-Default Authorization
All protected pages and actions MUST enforce authorization at both the route/page level and the service level. Users MUST only access projects, tasks, notifications, and announcements they are authorized to see, and every new feature MUST include an explicit access-control check before returning sensitive application data.

### IV. Locally Reproducible and Observable Development
The application MUST run end-to-end locally with `dotnet run` and SQLite, and development builds MUST be reproducible on a training workstation without cloud dependencies. Configuration, logging, and database initialization MUST support offline use and make it easy for learners to verify the application behavior on their local machine.

### V. Spec-Driven Development and Review Discipline
Feature work MUST follow the Spec Kit workflow configured in `.specify/` and `.github/`, including specification, planning, task generation, and review gates. Changes to behavior, architecture, or dependencies MUST be documented in a spec, reviewed before implementation, and aligned with the repository's Spec Kit workflow.

## Project Constraints and Standards
The project MUST target `.NET 10.0` and use `Microsoft.EntityFrameworkCore.Sqlite` for local persistence. The default training experience MUST remain Blazor Server and offline-first, with no production-only cloud dependency paths enabled by default. Code changes MUST preserve the local training architecture, keep `.specify` and `.github` artifacts current, and avoid introducing implementation details that require a production environment to build or run.

## Development Workflow and Quality Gates
Development MUST follow the GitHub Spec Kit workflow defined in `.specify/workflows/speckit/workflow.yml`. Every pull request affecting this repository MUST:
- pass `dotnet build`
- validate local SQLite startup
- reference the applicable spec and plan
- include a compliance note when security, data access, or training workflow is affected
The `agent-context` extension may refresh guidance after spec or plan changes, but constitution changes themselves MUST be committed with a clear governance rationale.

## Governance
This constitution is the source of truth for ContosoDashboard project practices and supersedes informal conventions. Amendments require a documented rationale, a corresponding update to `.specify` or `README.md` when relevant, and at least one code review approval from a team member familiar with the Spec Kit workflow.

- Security, persistence, and workflow changes MUST include an explicit note in the PR description.
- New feature branches MUST follow the `specify → plan → tasks → implement` path.
- Introduction of any new dependency MUST be justified in terms of local training reproducibility and learning value.

**Version**: 1.0.0 | **Ratified**: 2026-06-24 | **Last Amended**: 2026-06-24
