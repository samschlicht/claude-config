# claude-config

Personal Claude Code configuration. Portable across jobs and projects.

Much indebted to Boris Tane's [How I use Claude Code](https://boristane.com/blog/how-i-use-claude-code/).

## Structure

```
claude/                   # symlinked to ~/.claude
  CLAUDE.md               # universal principles, loaded every session
  commands/               # slash commands, loaded on demand
    research.md           # /research — deep codebase read + research.md artifact
    plan.md               # /plan    — implementation plan + annotation cycle
    implement.md          # /implement — execute approved plan
  contexts/               # project-specific context, imported per session
    talent-catalog.md     # Talent Catalog project
    _template.md          # template for new projects
PLAYBOOK.md               # human-facing workflow reference
```

## Setup on a new machine

```bash
git clone git@github.com:samschlicht/claude-config.git ~/projects/claude-config
mv ~/.claude ~/.claude.backup   # if it exists
ln -s ~/projects/claude-config/claude ~/.claude
```

## Usage

- `/research` — start any non-trivial ticket
- `/plan` — after reviewing research.md
- `/implement — go ahead` — after annotating and approving plan.md

To activate a project context, create a gitignored CLAUDE.local.md in the
repo root:

```
@~/.claude/contexts/[project].md
```

See `claude/contexts/` for available context files, or copy `_template.md`
to create a new one.

## Updating

Treat this like code. When something repeatedly goes wrong or right, update
the relevant file. Commit with a note about what changed and why.
