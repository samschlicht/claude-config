# Implement Phase

Execute the approved plan completely. The creative work is done — this phase
should be mechanical.

## Instructions

Implement everything in plan.md from top to bottom.

- Mark each task and phase as completed in plan.md as you go
- Do not stop to ask questions — all decisions were made in the plan
- Do not add unnecessary comments or documentation
- Do not use `any`/`unknown` types (TS) or raw Object casts (Java)
- Run typecheck continuously; do not let new errors accumulate
- Run the test suite when implementation is complete; fix all failures
- Write tests for new behaviour

When everything is done and green: commit with a descriptive message.

## Prompt to use

```
implement it all. mark tasks completed in plan.md as you go.
do not stop until all phases are complete.
do not add unnecessary comments or jsdoc/javadoc.
do not use any or unknown types.
run typecheck continuously.
run the test suite when done and fix any failures.
```

## During implementation

Corrections should be terse — Claude has full context of the plan and session:

- "you missed the deduplicateByTitle function"
- "that belongs in the service layer, not the controller"
- "wider" / "still misaligned" (for UI work, attach a screenshot)

If something goes badly wrong: revert, narrow the scope, re-approach.
Don't try to patch over a bad direction.

## When done

Commit. If opening a PR, ask Claude to write the PR description from plan.md.
