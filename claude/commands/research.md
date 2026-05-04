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

Do not plan. Do not implement. Do not suggest changes yet.

## Prompt to use

Adapt and paste:

```
read [folder/file/area] deeply — understand how it works, what it depends on,
its conventions, edge cases, and intricacies. when done, write a detailed
research.md with everything you found. do not plan or implement yet.
```

## After research

Review research.md yourself. Correct any misunderstandings with inline notes
before moving to /plan. The quality of the plan depends entirely on the
quality of the research.
