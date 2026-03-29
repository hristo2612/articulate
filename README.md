```
 █████  ██████  ████████ ██  ██████ ██   ██ ██       █████  ████████ ███████
██   ██ ██   ██    ██    ██ ██      ██   ██ ██      ██   ██    ██    ██
███████ ██████     ██    ██ ██      ██   ██ ██      ███████    ██    █████
██   ██ ██   ██    ██    ██ ██      ██   ██ ██      ██   ██    ██    ██
██   ██ ██   ██    ██    ██  ██████  █████  ███████ ██   ██    ██    ███████
```

**Quick language challenges pulled from your real writing.**

---

## What It Is

Articulate is a Claude Code skill that gives you a surprise language challenge every time you invoke it. Swap a word, trim a phrase, punch up a sentence, snipe your own weak writing. Each session takes under 2 minutes — short, honest feedback with a one-line etymology nugget that makes you think differently about words.

Three modes: **Lucky** (random missions from your writing), **Roast** (find your own weaknesses), **Ambient Coach** (tips while you work).

Works with Claude Code, Codex, Cursor, OpenCode, and Gemini CLI.

---

## Demo

### 🎯 Swap — Replace one word

```
## 🎯 Swap

One word is holding this sentence back:

> "We need to **handle** the migration before the sprint ends."

Replace **handle**. One word.
>
```

You type: `execute`

```
✅ Nailed it. "Handle" is vague — you handle luggage, complaints, exceptions.
"Execute" (Latin exsequī — follow to the end) means carry out a plan with precision.

💡 *"Execute" entered English through legal death warrants. When you execute a
migration, you're following every step to completion. No ambiguity.*

⚡ +28 XP (base 10 + score 9 + streak 9) | 🔥 5d

🎲 Another? go | 💾 Save save | ✌️ Done
```

### 🔍 Snipe — Fix your own writing

```
## 🔍 Snipe

Your words, under the microscope:

> "I think we should maybe try to basically refactor the thing that handles auth"

4 problems. Find and fix them all. Rewrite it.
>
```

You type: `Refactor the auth middleware.`

```
🔍 4/4 caught. Clean sweep. 🔥

✓ "I think" — hedge gone
✓ "maybe" + "basically" — filler gone
✓ "the thing that handles" → "the auth middleware" — named it

📉 14 → 4 words. That's a sentence now.

💡 *"Thing" (Old Norse þing) originally meant a public assembly. You were
accidentally calling every object a Viking parliament.*

⚡ +24 XP | 🔥 3d
```

### 💪 Punch — Make it hit

```
## 💪 Punch

This sentence has zero pulse:

> "The meeting went well and we discussed several important topics."

Make it hit. Same meaning, more impact.
>
```

You type: `We cracked three blockers in 40 minutes. No follow-up needed.`

```
💪 That landed. Numbers + specifics > adjectives.

💡 *"Several important topics" tells nothing. "Three blockers" tells everything.
Numbers are the most precise words in any language — they leave zero room for
interpretation.*

Score: 92/100
```

### 🔥 Roast — Detective game

```
## 🔥 Roast

Your words. My microscope.

> "I basically think we should probably try to implement some kind of
> solution for the thing that keeps breaking"

6 problems. Find them all. Rewrite it.
>
```

### 💡 Ambient Coach

Drops inline tips while you work:

You: *"Can you basically just make the button do the thing?"*

Claude responds normally, then:

> 💡 *You wrote "make the button do the thing" — try "trigger validation on click" for clarity.*

---

## The Six Missions

Every `/articulate` picks a random mission type. You never know what's coming.

| Mission | What you do | Time |
|---------|-------------|------|
| 🎯 **Swap** | Replace one weak word | 15 sec |
| ✂️ **Trim** | Cut a sentence in half | 30 sec |
| 💪 **Punch** | Make a flat sentence hit | 30 sec |
| 🔍 **Snipe** | Fix your own real writing | 1 min |
| 🔄 **Flip** | Rewrite in opposite tone | 30 sec |
| 🧩 **Fill** | One blank, one perfect word | 15 sec |

Plus **surprise twists** (~10% of sessions): Blind Punch, Reverse Swap, Speed Trim.

Missions are personalized from your recent conversations and project context. When you miss a word, you can **practice it** immediately in the next mission.

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

---

## Usage

All commands start with `/articulate`. First run triggers onboarding (name, language, coaching toggle).

| Command | What it does |
|---------|-------------|
| `/articulate` | Random surprise mission |
| `/articulate roast` | Roast your past writing |
| `/articulate roast here` | Roast current conversation |
| `/articulate coach on/off` | Toggle ambient coaching |
| `/articulate stats` | Your progress |
| `/articulate streak` | Streak status |
| `/articulate lexicon` | Words you've learned |
| `/articulate save` | Save progress to disk |
| `/articulate help` | All commands |

Append `--en` or `--bg` to force a language: `/articulate --bg`

### Save System

Progress is kept in memory during your session. Type `save` or `/articulate save` when you're ready to persist. No file I/O slowing you down between missions.

---

## Progression

Seven ranks. All modes available from Level 1 — levels are milestones, not gates.

| Level | Rank | XP | Badge |
|-------|------|-----|-------|
| 1 | RECRUIT | 0 | ⬜ |
| 2 | INITIATE | 100 | 🟩 |
| 3 | OPERATIVE | 300 | 🟨 |
| 4 | SPECIALIST | 600 | 🟧 |
| 5 | COMMANDER | 1000 | 🔴 |
| 6 | ARCHITECT | 1800 | 💎 |
| 7 | MASTERMIND | 3000 | 👑 |

**Badges:** 14 badges for streaks, scores, session counts, and multilingual training. Permanent — survive prestige resets.

**Streaks:** Daily sessions build streaks. Bonus XP up to +20/session. Streak shields at 30, 60, and 100 days.

**Prestige:** At MASTERMIND, optionally reset to RECRUIT with a ★ star. Badges and lexicon carry over.

---

## Languages

Works with **any language**. English and Bulgarian have curated reference files for richer sessions. Want to add yours? See [Contributing](#contributing).

---

## Data

All state at `~/.articulate/`. Nothing in the repo.

| File | What's in it |
|------|-------------|
| `user.json` | Name, languages, coaching toggle |
| `state.json` | XP, level, rank, streak, badges, weaknesses |
| `history.json` | Last 100 sessions (FIFO) |
| `lexicon.json` | Words learned with usage counts |
| `contexts/` | Cached project summaries |

```bash
# Backup
cp -r ~/.articulate ~/.articulate-backup

# Reset (requires confirmation)
/articulate reset
```

---

## Contributing

### Add a Language Pack

1. Create `skills/articulate/references/languages/{lang}.md`
2. Use `english.md` and `bulgarian.md` as reference
3. PR welcome

---

## License

[MIT](LICENSE) — Hristo Bogoev ([@hristo2612](https://github.com/hristo2612))
