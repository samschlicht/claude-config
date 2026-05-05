# Claude Code Playbook

My personal workflow for using Claude Code effectively. A reference for when
I've forgotten my own process.

---

## Before you start a ticket

Ask yourself:
- Is this trivial (single function, rename, typo, one-liner)? If yes, skip the
  pipeline — just describe the task directly in Claude Code.
- Do I understand the ticket well enough to direct research? If not, read the
  ticket and any linked context first — Claude can't compensate for your own
  unclear understanding of what's needed.
- Are there unknowns that will block implementation? Surface them now, not
  mid-implementation.
- Delete any existing research.md and plan.md from previous tickets — stale
  artifacts confuse Claude at the start of a new session.

---

## Starting a new ticket

1. Open GitHub, create a branch from the ticket, check it out locally
2. Activate the project context — check that CLAUDE.local.md exists in the repo
   root pointing to the right context file. See `~/.claude/contexts/` for available options.
   If missing, create it: `echo "@~/.claude/contexts/[project].md" > CLAUDE.local.md`
3. Open Claude Code in the repo root
4. For non-trivial work: proceed to Research phase
5. For trivial changes: describe the task directly and skip to implementation

---

## Research phase

1. Type `/research` followed immediately by your context in the same message —
   do not hit enter after `/research` alone or Claude will start exploring blindly.
   Use this template:
   ```
   /research

   I'm working on ticket #[number] — [brief description].
   read [folder/file/area] deeply — understand how it works, what it depends
   on, its conventions, edge cases, and intricacies. when done, write a
   detailed research.md with everything you found. do not plan or implement.
   ```
2. While Claude works, don't interrupt — let it read widely
3. When research.md is ready, read it yourself carefully:
    - Is Claude's understanding of the system accurate?
    - Has it identified the right files and dependencies?
    - Has it spotted the right patterns to follow?
4. Add inline corrections using the `# SAM:` prefix for anything wrong — be specific, not general
5. Check the code quality observations section — triage each one:
    - Fix as part of this ticket
    - Create a separate ticket
    - Consciously accept the debt
6. Only move to `/plan` when you're confident the understanding is accurate —
   a bad research phase produces a bad plan, which produces bad code

---

## Plan phase

1. Type `/plan` in Claude Code
2. Paste this prompt, adapted to your ticket:
   `based on research.md, write a detailed plan.md for [feature/change].
   include actual code snippets (not pseudocode), all files affected, what
   could go wrong, and a granular todo list by phase. do not implement yet.`
3. When plan.md is ready, open it in IntelliJ and read it carefully:
    - Does the approach fit the existing system?
    - Are all affected files identified?
    - Do the code snippets look right?
    - Has Claude challenged anything? If so, take it seriously.
4. Add inline notes directly in plan.md using the `# SAM:` prefix — corrections,
   constraints, rejected approaches, domain knowledge Claude wouldn't have.
   Example: `# SAM: this pattern was deprecated, use CandidateOpportunityService instead`
5. Return to Claude:
   `I've added notes to plan.md — address all # SAM: comments and remove them
   when done. do not implement yet.`
6. Repeat until the plan is something you'd be comfortable handing to a
   junior developer to implement
7. When the plan is approved, type: `/implement — go ahead`
   Never let Claude decide the plan is ready on its own.

---

## Implement phase

1. Type `/implement — go ahead`
2. Watch progress — Claude marks tasks complete in plan.md as it goes
3. Corrections should be terse — Claude has full context of the plan:
    - "you missed the deduplicateByTitle function"
    - "that belongs in the service layer, not the controller"
    - For UI: "wider" / "still misaligned" + attach a screenshot
4. If Claude flags a genuine blocker — stop. Don't push through it.
   Assess: return to plan phase, or revert and re-approach entirely.
   Do not let Claude patch over a bad direction.
5. If something goes badly wrong: revert cleanly, narrow the scope, re-approach.
   Patching a bad implementation is usually more expensive than reverting it.
6. When done and green, review the commit message before accepting it
7. If interrupted and resuming: `carry on from where you stopped`

---

## Session hygiene

- Between unrelated tasks: type `/clear` — stale context from a previous
  task actively degrades quality on the next one
- Before context fills: type `/compact` and tell Claude what to preserve:
  `/compact — focus on the plan and key decisions, discard file read contents`
- Watch for degradation — if Claude starts making uncharacteristic mistakes
  or ignoring instructions, context is probably too full. Compact or clear.
- Long sessions aren't always better — for a new unrelated problem,
  a fresh session often outperforms a long one with polluted context

---

## Resuming work mid-ticket

1. Open Claude Code on the correct branch
2. Say: `read plan.md and tell me where we are`
3. Claude will orient from the artifact — no need to re-explain context
4. If the session feels confused, compact first then resume

---

## Before opening a PR

Use Claude Code to review your own diff before human reviewers see it.

1. Save the diff to a temp file:
   `git diff main > /tmp/pr-diff.txt`

2. In Claude Code:
   `review the diff in /tmp/pr-diff.txt — check against AGENTS.md conventions,
   flag any bugs, code quality issues, or anything that shouldn't go to review`

3. Address anything worth fixing before pushing

For small diffs you can also pipe directly to clipboard and paste:
`git diff main | pbcopy`

Or if the PR is already open on GitHub, append .diff to the PR URL for a
clean plaintext version to copy.

Note: AI catches mechanical issues well — bugs, convention violations, obvious
oversights. It won't catch architectural or business logic concerns the way a
human reviewer will. The goal is to not waste your teammates' review time on
things you could have caught yourself.

---

## When things go wrong

Claude is going in the wrong direction mid-implementation:
- Press Escape to interrupt
- Say what's wrong tersely — "wrong layer" / "that's already handled in X"
- If it's a fundamental misunderstanding, revert and return to plan phase

The plan turns out to be wrong mid-implementation:
- Stop — don't let Claude improvise its way through
- Return to plan phase, update plan.md, then re-trigger implementation

Claude keeps ignoring an instruction:
- Check CLAUDE.md isn't too long — bloat causes rules to get lost
- Check the wording is unambiguous
- Add emphasis: "IMPORTANT:" or "NEVER:" if needed
- If it's a one-off, just correct it in session

The session has gone badly and there's a mess:
- For uncommitted changes: `git checkout .`
- For committed changes: `git revert HEAD` or `git reset --soft HEAD~1`
- Don't try to salvage a bad implementation — start the phase again
- If the branch is unrecoverable: delete it, create a fresh one, start over

---

## Keeping the config healthy

The config is only useful if it reflects how you actually work. Treat it like
code — review it when things go wrong, prune it when things change.

- After a session that went well: did anything work unusually well? Encode it.
- After a session that went badly: what instruction was missing or wrong?
  Fix it before the next session.
- Periodically: re-read CLAUDE.md. If a line no longer causes mistakes when
  removed mentally, cut it — dead rules dilute live ones.
- When switching projects: make sure the right context file is active in
  CLAUDE.local.md before starting.
- When the team switches to Linear: set up the Linear MCP server so Claude
  can read tickets directly. Generate a Personal API Key at linear.app/settings/api
  and add it to `~/.claude/settings.json` (already gitignored). The research
  prompt then becomes: "read Linear ticket ENG-3045 and read [area] deeply..."

To update and push config changes:
```
cd ~/projects/claude-config
git add -A
git commit -m "Update config — [what changed and why]"
git push
```

---

## Quick reference

| Situation                   | Action                                                    |
|-----------------------------|-----------------------------------------------------------|
| Starting non-trivial ticket | `/research` then `/plan` then `/implement`                |
| Starting trivial ticket     | Describe task directly                                    |
| Switching tasks             | `/clear`                                                  |
| Context getting full        | `/compact` with preservation instructions                 |
| Resuming work               | `read plan.md and tell me where we are`                   |
| Resuming after interruption | `carry on from where you stopped`                         |
| Wrong direction             | Interrupt, correct tersely, revert if needed              |
| Plan invalidated mid-impl   | Stop, fix plan.md, re-trigger                             |
| Session gone wrong          | `git checkout .` then start phase again                   |
| Before opening a PR         | `git diff main > /tmp/pr-diff.txt`, review in Claude Code |
| Getting a PR description    | `write a PR description from plan.md`                     |
