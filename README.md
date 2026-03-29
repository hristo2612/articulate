```
 █████  ██████  ████████ ██  ██████ ██   ██ ██       █████  ████████ ███████
██   ██ ██   ██    ██    ██ ██      ██   ██ ██      ██   ██    ██    ██
███████ ██████     ██    ██ ██      ██   ██ ██      ███████    ██    █████
██   ██ ██   ██    ██    ██ ██      ██   ██ ██      ██   ██    ██    ██
██   ██ ██   ██    ██    ██  ██████  █████  ███████ ██   ██    ██    ███████
```

**The vocabulary trainer that knows what you're building.**

---

## What It Is

Articulate is a skill plugin for AI-powered coding assistants that runs precision language training through guided writing missions directly in your terminal. You write, get scored on a 0-100 rubric, earn XP, level up, and build a personal lexicon of field-tested words. Sessions take 5 minutes. Missions adapt to your actual codebase so the language you practice is the language you ship.

Works with Claude Code, Codex, Cursor, OpenCode, and Gemini CLI.

---

## Demo

```
╔══════════════════════════════════════════╗
║  🟨 OPERATIVE  ║  XP: 342/600  ║  🔥🔥 5d  ║
║  ██████████████░░░░░░░░░░░ 57%           ║
║  Today: 1 mission  ║  Total: 47           ║
╚══════════════════════════════════════════╝

━━━ DAILY WORD ━━━━━━━━━━━━━━━━━━━━━━━━━━━
  idempotent  /ˌaɪ.dɛmˈpoʊ.tənt/
  Latin: idem (same) + potent (power)
  Producing the same result no matter how many times applied.
  Use it today for +5 bonus XP.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

━━━ MISSION: REWRITE ✏️ ━━━━━━━━━━━━━━━━━━
  CONTEXT: MoveKit — 3D exercise animation library
  Rewrite this for a pull request description:

  "Made some changes to the API so it handles things
   better when there are errors and stuff."

> Your response:
  "Harden the REST API error pipeline: validate request
   schemas at ingress, propagate typed error codes through
   the animation resolver, and surface actionable diagnostics
   in the response payload."

━━━ DEBRIEF ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  SCORE: 88/100
  ├─ Precision:    23/25  ███████████████████████░░
  ├─ Conciseness:  20/25  ████████████████████░░░░░
  ├─ Impact:       24/25  ████████████████████████░
  └─ Naturalness:  21/25  █████████████████████░░░░

  +10 base  +8 score  +10 streak  = 28 XP

  ┌──────────────────────────────────┐
  │  ★ BADGE EARNED: Precision Strike│
  │  Score 90+ on 5 missions         │
  └──────────────────────────────────┘

  Deploy another mission? Or save and return to base.
```

---

## Installation

### Claude Code

```bash
# Option A: Plugin install
claude plugin install https://github.com/hristo2612/articulate.git

# Option B: Manual clone
git clone https://github.com/hristo2612/articulate.git ~/.claude/skills/articulate
```

### Codex

```bash
git clone https://github.com/hristo2612/articulate.git ~/.codex/articulate
ln -s ~/.codex/articulate/skills ~/.agents/skills/articulate
```

See [`.codex/INSTALL.md`](.codex/INSTALL.md) for details.

### Cursor

```bash
# Option A: Marketplace (if available)
# Search "Articulate" in Cursor extensions

# Option B: Manual clone
git clone https://github.com/hristo2612/articulate.git ~/.cursor/skills/articulate
```

### OpenCode

Add to your `opencode.json`:

```json
{
  "plugin": ["articulate@git+https://github.com/hristo2612/articulate.git"]
}
```

See [`.opencode/INSTALL.md`](.opencode/INSTALL.md) for details.

### Gemini CLI

```bash
gemini extensions install https://github.com/hristo2612/articulate.git
```

Gemini reads `gemini-extension.json` and `GEMINI.md` from the repo root automatically.

---

## Usage

All commands start with `/articulate`. First run triggers onboarding.

| Command | Description |
|---------|-------------|
| `/articulate` | Full session: dashboard, daily word, mission |
| `/articulate go` | Same as above |
| `/articulate quick` | Skip dashboard, jump straight to a mission |
| `/articulate rewrite` | REWRITE mission (L1+) |
| `/articulate fill` | FILL_PRECISION mission (L1+) |
| `/articulate prompt` | PROMPT_CRAFT mission (L2+) |
| `/articulate scenario` | SCENARIO mission (L3+) |
| `/articulate boss` | BOSS mission (L4+) |
| `/articulate stats` | Full statistics dashboard |
| `/articulate badges` | Badge collection display |
| `/articulate lexicon` | Mastered words collection |
| `/articulate radar` | Weakness radar visualization |
| `/articulate config` | Update preferences |
| `/articulate help` | Commands and tips |

Append `--en` or `--bg` to any mission command to force a language:

```
/articulate rewrite --bg
```

---

## Mission Types

| Type | Emoji | Description |
|------|-------|-------------|
| REWRITE | ✏️ | Rewrite vague, bloated text into precise prose. The core drill. |
| FILL | 🎯 | Fill blanks in sentences with the most precise word possible. |
| PROMPT_CRAFT | 🧠 | Write prompts that produce exact outputs. Precision as instruction. |
| SCENARIO | 🎭 | Write for a specific audience, register, and context. Tone control. |
| BOSS | 💀 | Multi-part challenge. 3x XP. Tests everything you've trained. |
| REVIEW | 🔄 | Re-attempt past missions where you scored low. Prove you've grown. |

---

## Progression

### Ranks

| Level | Rank | XP | Badge | Unlocks |
|-------|------|-----|-------|---------|
| 1 | RECRUIT | 0 | ⬜ | REWRITE, FILL |
| 2 | INITIATE | 100 | 🟩 | + PROMPT_CRAFT, REVIEW |
| 3 | OPERATIVE | 300 | 🟨 | + SCENARIO |
| 4 | SPECIALIST | 600 | 🟧 | + BOSS |
| 5 | COMMANDER | 1000 | 🔴 | + User-generated challenges |
| 6 | ARCHITECT | 1800 | 💎 | + Teach mode |
| 7 | MASTERMIND | 3000 | 👑 | + Prestige system |

### Badges

14 badges earned through streaks, score milestones, mission counts, and skill diversity. Badges are permanent — they survive prestige resets and rank decay.

### Streaks

Daily training builds streaks. Streaks add bonus XP per mission (up to +20). Miss a day and the streak resets — unless you have a **streak shield** (earned at 30, 60, and 100-day milestones). Shields absorb one missed day each.

### Prestige

At MASTERMIND, optionally reset to RECRUIT with a ★ star marker. Badges and lexicon carry over. The real training starts at prestige.

---

## Context-Aware Missions

When enabled, Articulate scans your project (README, package.json, Cargo.toml, etc.) and generates missions that reference your actual codebase. A REWRITE mission might ask you to tighten a PR description for your real API. A SCENARIO mission might drop you into a stakeholder email about your real product. The language you practice is the language you deploy.

Toggle via `/articulate config`.

---

## Languages

Currently supported:

- **English** — full word lists, weakness patterns, and mission templates
- **Bulgarian** — full word lists, weakness patterns, and mission templates

Append `--en` or `--bg` to force a language for any mission. Configure default languages during onboarding or via `/articulate config`.

---

## Data

All operator state lives at `~/.articulate/`. Nothing is stored in the repo.

| File | Contents |
|------|----------|
| `user.json` | Name, languages, focus areas, preferences |
| `state.json` | XP, level, rank, streak, badges, weaknesses |
| `history.json` | Last 100 completed missions (FIFO) |
| `lexicon.json` | Mastered words with usage counts and mastery tiers |
| `contexts/` | Cached project summaries for context-aware missions |

### Backup

```bash
cp -r ~/.articulate ~/.articulate-backup
```

### Reset

```
/articulate reset
```

Requires confirmation. Wipes all progress.

---

## Contributing

### Add Mission Templates

Template banks live at `skills/articulate/templates/`. Each file is a Markdown bank of curated challenges:

```
templates/
├── rewrite-bank.md
├── fill-bank.md
├── prompt-bank.md
├── scenario-bank.md
└── boss-bank.md
```

Add entries following the existing format in each bank file. Each entry needs a challenge, a gold standard response, scoring notes, and relevant weakness categories.

### Add a Language Pack

Language packs live at `skills/articulate/references/languages/`. To add a new language:

1. Create `references/languages/{lang}.md` with word lists organized by level, weakness patterns, and detection rules.
2. Use `english.md` and `bulgarian.md` as reference implementations.
3. Update SKILL.md language handling section to include the new language code.

---

## License

[MIT](LICENSE) -- Hristo Bogoev ([@hristo2612](https://github.com/hristo2612))
