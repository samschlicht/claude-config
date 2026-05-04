# Work Client Context

TypeScript/Angular frontend, Java Spring backend. Team project — do not modify
shared config files, CI definitions, or anything in the repo root without
being asked. Prefer following existing patterns over introducing new ones.

## Frontend

- Language: TypeScript — strict mode, no `any` or `unknown`
- Framework: Angular (check package.json for version)
- State: check the codebase — follow whatever pattern is already in use
- Styling: check the codebase — follow existing conventions
- Tests: check for existing test setup (Jest / Karma / Jasmine) and follow it
- Linting: run `ng lint` after changes; fix all warnings
- Build check: run `ng build` to verify no compilation errors

## Backend

- Language: Java — check Java version in pom.xml or build.gradle
- Framework: Spring Boot
- Build tool: check for pom.xml (Maven) or build.gradle (Gradle)
- Tests: JUnit — run `./mvnw test` or `./gradlew test` after changes
- Never use raw `Object`, unchecked casts, or suppress warnings without justification
- Follow existing package structure; don't introduce new architectural layers

## Both

- Check existing code for naming conventions before introducing new names
- If a pattern exists in the codebase for something, follow it — don't invent
- Do not add logging statements unless asked
- Do not modify dependency versions unless that's the task

## How to activate this context

Add to a project-level `.claude/CLAUDE.local.md` (gitignored):

```
@~/.claude/contexts/work-client.md
```

Or paste at the start of a session:

```
read ~/.claude/contexts/work-client.md before we start
```
