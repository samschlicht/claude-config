# Claude Code — Universal Configuration

## Workflow

For any non-trivial ticket, follow this pipeline in order. Do not skip phases.
Use the slash commands: /research → /plan → /implement

For small, self-contained changes (a single function, a typo, a rename),
skip straight to implementation — the pipeline adds overhead not worth paying.

If unsure whether something is trivial, treat it as non-trivial.

## Implementation standards

- Never start implementing until a plan.md has been reviewed and approved
- Never stop mid-implementation to ask questions — raise blockers before starting
- Do not add comments or JSDoc/Javadoc unless explicitly asked
- Do not introduce `any` or `unknown` types (TypeScript) or raw `Object` casts (Java)
- Do not suppress errors, lint warnings, or type errors — fix the root cause
- Run typecheck continuously during implementation, not just at the end
- Run the test suite after implementation; fix failures before stopping
- Write tests for new behaviour unless explicitly told not to

## Git discipline

- Always work on a branch, never directly on main/master
- Commit at the end of each completed phase (research, plan, implementation)
- Use short WIP commits as checkpoints during long implementation sessions
- Commit messages: imperative mood, present tense ("Add pagination" not "Added pagination")
- When something goes wrong, revert cleanly rather than patching over bad state

## Context management

- Use /clear between unrelated tasks — stale context degrades quality
- Use /compact with instructions about what to preserve before context fills
- When resuming work, start by reading plan.md rather than re-explaining context

## Response style

- Be concise — no preamble, no summaries of what you just did
- When correcting course, acknowledge briefly and proceed — don't over-explain
- Terse corrections during implementation are expected and preferred
- Ask at most one clarifying question at a time; prefer acting on reasonable assumptions

## What this file is not

Project-specific context (stack, tooling, conventions) lives in
~/.claude/contexts/ and is imported per session. Keep this file under 100 lines.
