# Articulate — Codex Installation

Codex discovers skills by scanning `~/.agents/skills/` at startup and parsing SKILL.md frontmatter. No hooks are needed — Codex loads skills natively.

## Install

```bash
git clone https://github.com/hristo2612/articulate.git ~/.codex/articulate
ln -s ~/.codex/articulate/skills ~/.agents/skills/articulate
```

## Verify

After installation, start a new Codex session and type `/articulate`. The skill should activate automatically.

## Uninstall

```bash
rm ~/.agents/skills/articulate
rm -rf ~/.codex/articulate
```
