# Plan Phase

Turn research into an annotated implementation plan before any code is written.

## Instructions

Based on research.md (read it first), write a detailed implementation plan
in `plan.md`. The plan must include:

- The approach and why it fits the existing system
- Every file that will change, and how
- Code snippets showing the key changes (not pseudocode — actual code)
- Anything that could go wrong and how to handle it
- A granular todo list at the end, broken into phases and individual tasks

Do not implement. The plan is the deliverable for this phase.

## The annotation cycle

After Claude writes plan.md, the human will open it in their editor and add
inline notes — corrections, constraints, rejected approaches, domain knowledge.

When sent back with notes, Claude must:
- Address every note
- Update plan.md in place
- Not implement anything

This cycle repeats until the human is satisfied. The explicit signal to proceed
is "implement it all" or equivalent — not Claude deciding the plan looks good enough.

## Prompt to use

```
based on research.md, write a detailed plan.md for [feature/change].
include code snippets, all files affected, and a granular todo list.
do not implement yet.
```

## After each annotation round

```
I've added notes to plan.md — address all of them and update the document.
do not implement yet.
```

## Ready to implement?

When the plan is approved, use /implement.
