# Claude Code Playbook

My personal workflow for using Claude Code effectively. A reference for when
I've forgotten my own process.

---

## Starting a new ticket

1. Open GitHub, create a branch from the ticket, check it out locally
2. Open Claude Code in the repo root
3. For non-trivial work: type `/research` and follow the prompt
4. For trivial changes (single function, rename, typo): just describe the task directly

---

## Session hygiene

- **Between unrelated tasks:** type `/clear` to start fresh — stale context from a previous task degrades quality on the next one
- **Before context fills:** type `/compact` and tell Claude what to preserve, e.g. "focus on the plan and key decisions, discard file read contents"
- **Don't let Claude run too long without a checkpoint** — long sessions with full context windows produce worse output

---

## Resuming work mid-ticket

1. Open Claude Code on the correct branch
2. Say: "read plan.md and tell me where we are"
3. Continue from there — no need to re-explain context

---

## Research phase

1. Type `/research` in Claude Code
2. Paste this prompt, adapted to your ticket:
   "read [folder/file/area] deeply — understand how it works, what it depends on,
   its conventions, edge cases, and intricacies. when done, write a detailed
   research.md with everything you found. do not plan or implement yet."
3. While Claude works, don't interrupt — let it read widely
4. When research.md is ready, read it yourself carefully
5. Add inline corrections for anything Claude got wrong — be specific
6. Check the code quality observations section — triage each one: fix in this
   ticket, create a separate ticket, or consciously accept the debt
7. Only move to /plan when you're satisfied the understanding is accurate

---

## Plan phase

1. Type `/plan` in Claude Code
2. Paste this prompt, adapted to your ticket:
   "based on research.md, write a detailed plan.md for [feature/change].
   include code snippets, all files affected, and a granular todo list.
   do not implement yet."
3. When plan.md is ready, open it in IntelliJ and read it carefully
4. Add inline notes directly in the file — corrections, constraints, rejected
   approaches, domain knowledge Claude wouldn't have
5. Pay attention to any concerns Claude raised — it's required to challenge
   bad approaches, so if it flags something, take it seriously
6. Return to Claude and say:
   "I've added notes to plan.md — address all of them and update the document.
   do not implement yet."
7. Repeat steps 3-6 until satisfied
8. The signal to proceed is explicit — say "implement it all" or equivalent.
   Never let Claude decide the plan is good enough on its own.

---

## Implement phase

1. When the plan is approved, say "implement it all" — this is the explicit trigger
2. Watch progress — Claude will mark tasks complete in plan.md as it goes
3. Corrections during implementation should be terse — Claude has full context:
    - "you missed the deduplicateByTitle function"
    - "that belongs in the service layer, not the controller"
    - For UI work: "wider" / "still misaligned" + attach a screenshot
4. If Claude flags a genuine blocker, stop — don't push through it
    - Assess whether to return to plan phase or revert and re-approach
    - Do not let Claude patch over a bad direction
5. If something goes badly wrong: revert cleanly, narrow the scope, re-approach
6. When done and green, Claude will commit — review the commit message
7. To open a PR, say "write a PR description from plan.md"

---

## More to come

This file will be updated as we review each config file.
