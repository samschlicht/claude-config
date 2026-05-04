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

This cycle repeats until the human sends: `/implement — go ahead`
That is the only signal to proceed — do not begin implementation otherwise.

## Challenge the approach

While planning, actively raise concerns about the proposed direction — better
architecture, simpler alternatives, potential issues, best practice violations.
Challenge the human's assumptions before the plan is locked. Do not produce a
plan that colludes in a bad approach to avoid friction.
