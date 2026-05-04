# claude-config

Personal Claude Code configuration. Portable across jobs and projects.

## Structure

```
claude/                   # symlinked to ~/.claude
  CLAUDE.md               # universal principles, loaded every session
  commands/               # slash commands, loaded on demand
    research.md           # /research — deep codebase read + research.md artifact
    plan.md               # /plan    — implementation plan + annotation cycle
    implement.md          # /implement — execute plan, verify, commit
  contexts/               # project-specific context, imported as needed
    work-client.md        # current employer: TypeScript/Angular + Java Spring
    [sideproject].md      # add per side project
```

## Setup on a new machine

```bash
git clone git@github.com:YOUR_USERNAME/claude-config.git ~/projects/claude-config
mv ~/.claude ~/.claude.backup   # if it exists
ln -s ~/projects/claude-config/claude ~/.claude
```

## Usage

- `/research` — start any non-trivial ticket
- `/plan`    — after reviewing research.md
- `/implement` — after annotating and approving plan.md

To activate a project context, add this to the top of a session or to a
project-level CLAUDE.local.md (gitignored):

```
@~/.claude/contexts/work-client.md
```

## Updating

Treat this like code. When something repeatedly goes wrong or right, update
the relevant file. Commit with a note about what changed and why.
