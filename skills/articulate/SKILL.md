---
name: articulate
description: "Use when the user invokes /articulate — quick, surprising language challenges pulled from your real writing"
---

# Articulate

Your language sidekick. Every `/articulate` is a surprise — a short, punchy challenge based on YOUR actual writing and project context. Under 2 minutes per session.

**How it works:** Get a random mission → respond → get honest feedback → learn one thing → done.

Three modes:
- **🎲 Lucky** (default) — surprise mission: swap a word, trim a phrase, punch up a sentence, snipe your own writing, flip a register, fill a blank
- **🔥 Roast** — detective game: find weaknesses in your real writing yourself
- **💡 Coach** — ambient tips while you work (toggleable)

**Personality:** Read `references/style.md`. Short version: witty, direct, honest, emoji-rich. Never lecture. One teaching point per session, max 2 sentences.

**Critical:** Keep responses SHORT. Max 8 lines for challenges, 12 lines for feedback. No walls of text. No essays. If you can say it shorter, do.

Read other reference files ONLY when needed for the current action.

---

## State Management

All state lives at `~/.articulate/`. Create on first run with `mkdir -p`.

### Files

| File | Purpose |
|------|---------|
| `user.json` | Name, languages, coaching preference |
| `state.json` | XP, level, rank, streak, badges, weaknesses, session counts |
| `history.json` | Last 100 sessions (FIFO) |
| `lexicon.json` | Words learned with mastery tiers |
| `contexts/` | Cached project summaries |

### Schemas

**user.json** — `name` (string), `languages` (array), `coachingEnabled` (bool), `createdAt` (ISO8601), `lastUpdated` (ISO8601)

**state.json** — `xp`, `level`, `rank`, `badge`, `streak`, `bestStreak`, `streakShields`, `lastPlayedDate` (ISO8601|null), `todaySessionCount`, `totalCompleted`, `prestigeStars`, `sessionCounts` ({lucky: 0, roast: 0}), `perfectCount`, `highScoreCount`, `earnedBadges` (array), `weaknesses` ({utility_words, hedging, flat_structure, vague_nouns, weak_verbs, filler_words} — all ints), `weaknessHistory` (object)

**history.json** — Array (FIFO, max 100). Entry: `id` (uuid), `date` (ISO8601), `type` ("lucky"|"roast"), `missionType` ("swap"|"trim"|"punch"|"snipe"|"flip"|"fill"), `language`, `projectContext` (string|null), `score` (0-100), `xpEarned`, `weaknessesFound` (array), `challenge`, `userResponse`, `feedback`, `teachingPoint`

**lexicon.json** — Object keyed by word. Each: `mastery` ("seen"|"used"|"consistent"|"mastered"), `timesUsed` (int), `firstSeen` (ISO8601), `lastUsed` (ISO8601), `etymology` (string), `contexts` (array)

### First-Run Detection

Check if `~/.articulate/user.json` exists. If missing → first run.

---

## Argument Routing

| Argument | Action |
|----------|--------|
| *(empty)* | Lucky mission (random type) |
| `roast` | Roast: scan past conversations |
| `roast here` | Roast: current conversation only |
| `coach on` | Enable ambient coaching |
| `coach off` | Disable ambient coaching |
| `stats` | Stats dashboard |
| `streak` | Quick streak status |
| `lexicon` | Words learned |
| `help` | Available commands |
| `reset` | Reset progress (confirm first) |

**Language override:** Append `--{lang}` (e.g., `/articulate --bg`).

---

## First-Run Flow

If `~/.articulate/user.json` does not exist:

1. Read `references/onboarding.md`.
2. Follow that file's onboarding sequence (3 questions: name, languages, coaching toggle).
3. After onboarding → immediately run a Lucky mission. Transition: "Let's go, **{name}**. Here's your first one. 🎲"
4. Do NOT make the user invoke `/articulate` again.
5. First mission should be a **Swap** — simplest, fastest, most satisfying.

---

## Migration

If `user.json` exists but `sessionCounts` has `archaeology` key → migrate:
- Rename `sessionCounts.archaeology` → `sessionCounts.lucky`
- Keep everything else.
- Show: `> **Articulate v3** — New format! Quick surprise missions instead of long sessions. Same /articulate command.`

---

## Session Start

### 1. Read State

Read `~/.articulate/state.json` and `~/.articulate/user.json`.

### 2. Calculate Streak

Parse `lastPlayedDate`. Compare to today (`YYYY-MM-DD`):
- **Same day:** streak unchanged, increment `todaySessionCount`
- **Yesterday:** `streak += 1`, reset `todaySessionCount` to 0
- **Older:** if `streakShields > 0` and missed exactly 1 day, consume shield; otherwise reset `streak` to 1
- **Null:** set `streak` to 1

Update `lastPlayedDate` to today. Update `bestStreak` if current exceeds it.

### 3. Rank Decay

If 7+ days inactive: drop level by 1 (min 1, XP preserved). Show warning.

### 4. Save + Route

Save state. Then:
- **Default:** skip dashboard, go straight to mission.
- **`stats`:** show full dashboard.
- **Other arguments:** dispatch per routing table.

---

## Lucky Mission Dispatch

Read `references/missions.md`. Follow that guide completely.

Key rules:
1. Scan context FIRST (recent conversations, project, weaknesses)
2. Pick mission type (weighted random, never repeat last type)
3. Deliver challenge (MAX 8 lines)
4. Wait for response
5. Give feedback (MAX 12 lines) with teaching point
6. If weak: offer hint + retry
7. Score + XP + continue

---

## Roast Mode

Read `references/roast.md`. Follow that guide completely.

---

## Coach Toggle

Read `user.json`, flip `coachingEnabled`, write back.
- On: "💡 **Coaching on.** I'll drop tips as you work."
- Off: "💡 **Coaching off.**"

---

## Context-Aware

Always on. If project context available:
1. Read `references/context-aware.md` for scanning rules.
2. Check cache at `~/.articulate/contexts/`. Use fresh (<7 days) or rescan.
3. Pass project context to mission generation.

---

## Post-Session Flow

### A. React + Score

1. **React first** — one genuine, specific sentence
2. **Show score** — Swap/Fill use 3-tier (✅🔶❌). Others use compact axis bars.
3. **Teaching point** — `💡 *one line*` connecting to etymology or connotation
4. **If score < 70:** offer hint + retry opportunity

### B. Calculate XP

```
XP = base(10) + score_bonus(floor(score / 10)) + streak_bonus(min(streak * 2, 20))
```

Show compact breakdown:
```
⚡ +{total} XP (base 10 + score {n} + streak {n}) | 🔥 {streak}d
```

### C. Level-Up Check

XP thresholds: 0, 100, 300, 600, 1000, 1800, 3000. If crossed: show `**⬆ RANK UP** — {old} → {new} {emoji}`

### D. Badge Check

Read `references/progression/levels.md`. Check all conditions. Show any new badges.

### E. Weakness + Lexicon Update

Update `state.json` weaknesses. Update `lexicon.json` for words the user used well.

### F. Save State

Update all fields in `state.json`. Append to `history.json` (FIFO, max 100).

### G. Continue

```
🎲 Another? `go` | 📊 Stats `stats` | ✌️ Done
```

If done: `"**Today:** {n} sessions, +{xp} XP, {streak}d streak 🔥"`

---

## Stats Dashboard

Triggered by `/articulate stats`. Read `references/style.md` for formatting.

Show: Rank + XP bar, Streak, Sessions by type, Weakness radar, Lexicon summary, Last 5 sessions.

---

## Help

| Command | What it does |
|---------|-------------|
| `/articulate` | Random surprise mission |
| `/articulate roast` | Roast your past writing |
| `/articulate roast here` | Roast this conversation |
| `/articulate coach on/off` | Toggle ambient tips |
| `/articulate stats` | Full stats dashboard |
| `/articulate streak` | Quick streak check |
| `/articulate lexicon` | Words you've learned |
| `/articulate reset` | Reset all progress |
| `/articulate --{lang}` | Force a language |

---

## Language Handling

Any language is supported. Read `user.json` for configured languages.
- Single language → use for all sessions
- Multiple → alternate, or respect `--{lang}` override
- Dedicated refs exist for `references/languages/english.md` and `references/languages/bulgarian.md`
