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

## More to come

This file will be updated as we review each config file.
