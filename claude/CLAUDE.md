# Claude Code — Universal Configuration

## Workflow

For any non-trivial ticket, follow this pipeline in order. Do not skip phases.
Use the slash commands: /research → /plan → /implement

For small, self-contained changes (a single function, a typo, a rename),
skip straight to implementation — the pipeline adds overhead not worth paying.

If unsure whether something is trivial, treat it as non-trivial.

## Implementation standards

- Never start implementing until a plan.md has been reviewed and approved
- Raise all blockers before starting — do not begin implementation with unresolved unknowns
- EXCEPTION: if something genuinely unexpected arises mid-implementation that invalidates
  the plan, stop and flag it immediately — do not guess or work around it. Return to plan phase if needed.
- Add JSDoc/Javadoc to all new methods and classes
- Do not add inline comments unless the code is genuinely non-obvious
- Do not introduce `any` or `unknown` types (TypeScript) or raw `Object` casts (Java)
- Do not suppress errors, lint warnings, or type errors — fix the root cause
- Run typecheck continuously during implementation, not just at the end
- Run the test suite after implementation; fix failures before stopping
- Write tests for new behaviour

## Git discipline

- Never commit directly to main, master, or staging — if somehow on one of these branches, stop and 
  flag it immediately
- Commit at the end of each completed phase (research, plan, implementation)
- Use short WIP commits as checkpoints during long implementation sessions
- Commit messages: imperative mood, present tense ("Add pagination" not "Added pagination")
- When something goes wrong, revert cleanly rather than patching over bad state

## Context management

- When resuming work, start by reading plan.md rather than asking for context

## Response style

- Actively challenge decisions, approaches, or assumptions that conflict with best
  practice, established conventions, or the existing codebase patterns — at any
  phase, but especially during research and planning. Do not collude in a bad
  approach to avoid friction. Being wrong early is cheap; being wrong during
  implementation is expensive.
- Be concise — no preamble, no summaries of what you just did
- When correcting course, acknowledge briefly and proceed — don't over-explain
- Terse corrections during implementation are expected and preferred
- Ask at most one clarifying question at a time; prefer acting on reasonable assumptions

## Code quality

- Prefer existing conventions for consistency and team readability, but do not
  follow them blindly — if a convention is itself the problem, say so
- Do not treat existing code as correct simply because it exists — if something
  is poorly designed, brittle, or violates best practice, flag it
- Raise code quality issues as observations, not blockers — note them in research.md
  or plan.md and let the human decide whether to address them as part of the ticket
  or separately
