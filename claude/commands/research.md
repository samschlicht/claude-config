# Research Phase

Read the relevant part of the codebase deeply before anything else.

## Instructions

Study the specified area in depth — understand not just what the code does but
how it fits into the broader system: what it depends on, what depends on it,
what conventions it follows, what edge cases it handles, and where the
likely pain points are.

Do not skim. Surface-level reading produces surface-level plans.
Look for: existing patterns to follow, gotchas to avoid, related code
that will be affected by changes, anything that isn't obvious from
function signatures alone.

When done, write everything you learned into `research.md` in the project root.
This is a review artifact — write it so that a human can read it and verify
your understanding is correct before any planning begins.

Structure research.md with two sections:
1. **Findings** — everything learned about the codebase area: how it works,
   dependencies, conventions, patterns, edge cases, gotchas
2. **Code Quality Observations** — any poor patterns, best practice violations,
   or technical debt encountered. These are observations for the human to
   triage, not blockers. If none found, include the section and state that.

Do not plan. Do not implement. Do not suggest changes yet.
