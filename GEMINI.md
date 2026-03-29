# Articulate — Gemini CLI Context

Articulate is a precision language training skill that coaches vocabulary through guided writing missions directly in your terminal. It is gamified with XP, streaks, levels, and badges.

## Tool Mapping

Articulate was designed for multi-platform use. When executing skill instructions, use these Gemini CLI equivalents:

| Skill instruction | Gemini CLI equivalent |
|---|---|
| Read a file | `read_file` |
| Write a file | `write_file` |
| Edit a file | `edit_file` |
| Run a shell command | `run_bash` |

## Activation

To load the Articulate skill, read the skill definition file:

```
Read: skills/articulate/SKILL.md
```

Then follow the instructions in SKILL.md to run the session flow.

## Skill Directory

All skill content lives under `skills/articulate/` in this repository:

- `SKILL.md` — Core routing and session logic
- `references/` — Detailed rules for missions, progression, languages, and style
- `templates/` — Mission content banks

## User State

User progress is stored at `~/.articulate/` (created on first run). This directory is outside the repo and persists across updates.
