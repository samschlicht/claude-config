# Talent Catalog Context

Talent Catalog is a Spring Boot + Angular application for managing candidate
skills, opportunities, and partner organizations.

Read and follow AGENTS.md in the project root. The instructions below extend
or clarify it — where there is any conflict, prefer these instructions.

## Structure

- Backend: `server/` — Spring Boot, Maven (build via Gradle — see build.gradle)
- Frontend: `ui/` — Angular 17

## Frontend tests

- Framework: Jasmine
- Run with: `ng test` from the `ui/` directory
- Use `jasmine.createSpyObj` for mocking services
- Use `xit()` / `xdescribe()` to skip tests, never delete them
- Common TestBed issues and fixes are documented in the project wiki —
  check there before assuming a test setup is wrong

## Backend tests

Unit tests:
- Located in `server/`
- Run with Gradle

Integration tests:
- Located in `src/test/java/org/tctalent/server/integration/`
- Require Docker running and `dump.sql` in `src/test/resources/`
- Extend `BaseJpaIntegrationTest` for repository tests
- Extend `BaseDBIntegrationTest` for service/API tests
- Use `TestDataFactory` to create test data — do not create entities manually
- Do not run integration tests unless explicitly asked — they require Docker setup

## Database

- Flyway manages migrations — follow AGENTS.md rules strictly:
  never modify existing migrations, always add new ones for schema changes
- Be aware of N+1 query problems — prefer DTO projections or native queries

## Conventions that extend AGENTS.md

- Constructor injection only — no field injection
- Controllers must be thin — business logic belongs in services
- Do not introduce new architectural layers without discussion
- Do not modify dependency versions unless that is the task
- Do not add logging statements unless asked

## Git

- Base branch is `staging` — not `main`. PRs are raised against `staging`.
- When asked to write a PR description, follow the AGENTS.md format:
  description of change, list of modified components, tests added or updated
