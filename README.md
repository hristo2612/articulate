```
 █████  ██████  ████████ ██  ██████ ██   ██ ██       █████  ████████ ███████
██   ██ ██   ██    ██    ██ ██      ██   ██ ██      ██   ██    ██    ██
███████ ██████     ██    ██ ██      ██   ██ ██      ███████    ██    █████
██   ██ ██   ██    ██    ██ ██      ██   ██ ██      ██   ██    ██    ██
██   ██ ██   ██    ██    ██  ██████  █████  ███████ ██   ██    ██    ███████
```

**Your language nerd sidekick for the terminal.**

---

## What It Is

Articulate is a Claude Code plugin that turns your terminal into a language discovery engine. It has three modes: **Word Archaeology** (dig up fascinating etymologies, then apply what you learned), **Roast Mode** (scans your real writing and challenges you to cut the fluff), and **Ambient Coach** (drops one-line vocabulary tips while you work). Sessions take 60 seconds. You earn XP, level up, and build a personal lexicon of words you've actually used.

Works with Claude Code, Codex, Cursor, OpenCode, and Gemini CLI.

---

## Demo

### Word Archaeology

> The default experience. You get a story, a principle, and one exercise.

## 🔍 Word Archaeology: *trivial*

In ancient Rome, the *trivium* was where three roads met — literally "three ways" (Latin *tri-* + *via*). These crossroads became gathering spots where ordinary people chatted about ordinary things.

The word drifted through centuries carrying that association: trivium → trivialis → "commonplace" → "unimportant." A word born from the geometry of roads became our way of dismissing things that don't matter.

Here's the twist: the medieval *trivium* was also the name for the foundational university curriculum (grammar, logic, rhetoric). The "trivial" arts were considered **essential** — the opposite of how we use the word today.

💡 **The principle:** Words that describe importance often started as words about physical space. "Fundamental" = foundation. "Underlying" = beneath. "Trivial" = crossroads. When you need to convey significance, spatial metaphors hit harder than abstract ones.

### ✏️ Your turn

Rewrite this sentence using a spatial metaphor instead of the abstract language:

> "This issue is very important to the project's success and shouldn't be ignored."

Max 20 words.

---

### Roast Mode

> Scans your actual writing. Finds the worst sentence. Makes you fix it.

## 🔥 Roast: Your Writing, last 7 days

I found this:

> "I think we should maybe try to basically refactor the thing that handles the stuff for the user authentication part of the system."

That's **23 words** for a **6-word job**. Let me count:
- 🟡 "I think" — hedge
- 🟡 "maybe" — hedge
- 🟡 "try to" — hedge
- 🟡 "basically" — filler
- 🔴 "the thing that handles the stuff" — vague noun avalanche
- 🟠 "part of the system" — padding

**6 weaknesses** in one sentence. That's impressive (not the good kind).

### ✏️ Rewrite challenge
Say what you actually mean. Max 8 words.

---

### Ambient Coach

> Drops inline tips while you work. One line, never in your way.

You: *"Can you basically just make the button do the thing when someone clicks it?"*

Claude responds normally, then:

> 💡 *You wrote "make the button do the thing" — try "trigger validation on click" for clarity.*

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

| Command | What it does |
|---------|-------------|
| `/articulate` | Word Archaeology session |
| `/articulate roast` | Roast your past writing |
| `/articulate roast here` | Roast current conversation |
| `/articulate coach on/off` | Toggle ambient coaching |
| `/articulate stats` | Your progress |
| `/articulate streak` | Streak status |
| `/articulate lexicon` | Words you've mastered |
| `/articulate help` | All commands |

Append `--en` or `--bg` to any command to force a language:

```
/articulate --bg
```

---

## The Three Modes

### 🔍 Word Archaeology

The default mode. Every session picks a word with a genuinely surprising origin story — semantic drift, hidden metaphors, eponyms, cross-language connections — and tells it like a story, not a dictionary entry. Then you get one exercise that flows directly from the etymology. Takes about 60 seconds. You walk away knowing something interesting and having written something precise.

### 🔥 Roast Mode

Scans your real writing — past Claude/Codex conversations or the current chat — and finds the weakest sentence. Hedge stacking, vague noun avalanches, filler word bloat. It quotes the offending passage, tags every weakness, and challenges you to rewrite it in half the words. Finds 3 passages per session, worst first.

### 💡 Ambient Coach

A background mode. When enabled, Articulate watches your messages and occasionally drops a one-line vocabulary tip after Claude's regular response. "You wrote X — try Y for precision." Max once every 3-4 messages. Stays out of your way when you're debugging or in a hurry. Toggle with `/articulate coach on/off`.

---

## Progression

Seven ranks from newcomer to language architect. All three modes are available from Level 1 — levels are milestones, not gates.

| Level | Rank | XP | Badge |
|-------|------|-----|-------|
| 1 | RECRUIT | 0 | ⬜ |
| 2 | INITIATE | 100 | 🟩 |
| 3 | OPERATIVE | 300 | 🟨 |
| 4 | SPECIALIST | 600 | 🟧 |
| 5 | COMMANDER | 1000 | 🔴 |
| 6 | ARCHITECT | 1800 | 💎 |
| 7 | MASTERMIND | 3000 | 👑 |

**Badges:** 14 badges earned through streaks, score milestones, session counts, and multilingual training. Badges are permanent — they survive prestige resets.

**Streaks:** Daily sessions build streaks. Streaks add bonus XP (up to +20 per session). Miss a day and the streak resets — unless you have a streak shield. Shields are earned at 30, 60, and 100-day milestones.

**Prestige:** At MASTERMIND, optionally reset to RECRUIT with a ★ star marker. Badges and lexicon carry over. Stars accumulate indefinitely.

---

## Languages

Articulate works with **any language** — the AI generates etymology stories and exercises on the fly. English and Bulgarian have curated reference files with word lists, weakness patterns, and coaching templates for richer sessions.

Want to add your language? See [Contributing](#contributing).

---

## Data

All state lives at `~/.articulate/`. Nothing is stored in the repo.

| File | What's in it |
|------|-------------|
| `user.json` | Name, languages, preferences, coaching toggle |
| `state.json` | XP, level, rank, streak, badges, weaknesses |
| `history.json` | Last 100 completed sessions (FIFO) |
| `lexicon.json` | Words you've mastered with usage counts |

**Backup:**

```bash
cp -r ~/.articulate ~/.articulate-backup
```

**Reset:**

```
/articulate reset
```

Requires confirmation. Wipes all progress.

---

## Contributing

### Add a Language Pack

Language packs live at `skills/articulate/references/languages/`. To add a new language:

1. Create `references/languages/{lang}.md` with word lists organized by level, weakness patterns, and detection rules.
2. Use `english.md` and `bulgarian.md` as reference implementations.
3. Update SKILL.md language handling section to include the new language code.

PRs welcome.

---

## License

[MIT](LICENSE) — Hristo Bogoev ([@hristo2612](https://github.com/hristo2612))
