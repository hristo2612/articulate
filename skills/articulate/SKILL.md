---
name: articulate
description: "Use when the user invokes /articulate — precision language training skill for building active vocabulary through guided writing missions"
---

# Articulate

Precision language training through writing missions. Production over recognition — you write, get scored, level up.

Target session: 5 minutes. Each mission is a focused writing challenge with immediate feedback, XP, and progression tracking. All missions emphasize replacing vague, weak language with precise, high-impact alternatives.

For personality, tone, and formatting templates, read `references/style.md`.

---

## State Management

All state lives at `~/.articulate/`. Create this directory on first run.

### Files

| File | Purpose |
|------|---------|
| `~/.articulate/user.json` | Name, languages, focus areas, preferences |
| `~/.articulate/state.json` | XP, level, rank, streak, badges, weaknesses, mission counts |
| `~/.articulate/history.json` | Last 100 missions (FIFO array) |
| `~/.articulate/lexicon.json` | Mastered words with usage counts and mastery tiers |
| `~/.articulate/contexts/` | Cached project summaries for context-aware missions |

### user.json Schema

```json
{
  "name": "string",
  "languages": ["English"],
  "focusAreas": ["prompt_engineering", "business_communication"],
  "dailyMinutes": 5,
  "selfAssessment": 3,
  "contextAware": true,
  "createdAt": "ISO8601",
  "lastUpdated": "ISO8601"
}
```

### state.json Schema

```json
{
  "xp": 0, "level": 1, "rank": "RECRUIT", "badge": "⬜",
  "streak": 0, "bestStreak": 0, "streakShields": 0,
  "lastPlayedDate": null, "todayMissionCount": 0, "totalCompleted": 0,
  "prestigeStars": 0,
  "missionCounts": { "rewrite": 0, "fill": 0, "prompt": 0, "scenario": 0, "boss": 0, "review": 0 },
  "perfectCount": 0, "highScoreCount": 0, "earnedBadges": [],
  "weaknesses": {
    "utility_words": 0, "hedging": 0, "flat_structure": 0,
    "vague_nouns": 0, "weak_verbs": 0, "filler_words": 0
  },
  "weaknessHistory": {},
  "currentSeason": null, "lastBossDate": null,
  "dailyWord": null, "dailyWordDate": null
}
```

### history.json Entry Schema

```json
{
  "id": "uuid-v4", "date": "ISO8601", "type": "rewrite",
  "language": "English", "projectContext": null,
  "score": 75, "xpEarned": 18, "criticalHit": false,
  "weaknessesFound": ["utility_words"],
  "challenge": "...", "userResponse": "...", "goldStandard": "...", "feedback": "..."
}
```

### lexicon.json Entry Schema

```json
{
  "word": {
    "mastery": "seen|used|consistent|mastered",
    "timesUsed": 1, "firstSeen": "ISO8601", "lastUsed": "ISO8601",
    "etymology": "...", "contexts": ["business email"]
  }
}
```

### First-Run Detection

Check if `~/.articulate/user.json` exists. If missing, this is a first run.

### Read / Write

Read state files at session start. Write updated JSON after every mission. Use Bash `mkdir -p` for directory creation and Read/Write tools for JSON files.

---

## Argument Routing

Route based on `$ARGUMENTS` passed after `/articulate`.

| Argument | Action | Gate |
|----------|--------|------|
| *(empty)* or `go` | Default flow: dashboard, daily word, mission | None |
| `rewrite` | REWRITE mission | L1+ |
| `fill` | FILL_PRECISION mission | L1+ |
| `prompt` | PROMPT_CRAFT mission | L2+ (100 XP) |
| `review` | REVIEW mission | L2+ (100 XP) |
| `scenario` | SCENARIO mission | L3+ (300 XP) |
| `boss` | BOSS mission | L4+ (600 XP) |
| `quick` | Skip dashboard, random mission | None |
| `menu` | Show available missions with unlock status | None |
| `stats` | Full statistics dashboard | None |
| `badges` | Badge collection display | None |
| `lexicon` | Mastered words collection | None |
| `radar` | Weakness radar visualization | None |
| `help` | Commands and tips | None |
| `reset` | Reset progress (require confirmation) | None |
| `config` | Update user preferences | None |

### Unlock Gates

Check `state.json` level before dispatching locked missions. If locked, show the requirement and current progress.

| Level | Rank | XP | Unlocks |
|-------|------|-----|---------|
| 1 | RECRUIT | 0 | rewrite, fill |
| 2 | INITIATE | 100 | + prompt, review |
| 3 | OPERATIVE | 300 | + scenario |
| 4 | SPECIALIST | 600 | + boss |
| 5 | COMMANDER | 1000 | + user-generated challenges |
| 6 | ARCHITECT | 1800 | + teach mode |
| 7 | MASTERMIND | 3000 | + prestige |

For full level details, badges, prestige rules, and streak shields, read `references/progression/levels.md`.

### Language Override

Append `--en` or `--bg` to any mission command to force a language. Example: `/articulate rewrite --bg`.

---

## First-Run Flow

If `~/.articulate/user.json` does not exist:

1. Read `references/onboarding.md`.
2. Follow that file's onboarding sequence (welcome banner, setup questions, file creation).
3. After onboarding completes, run an easy REWRITE mission immediately.
4. Do NOT make the user invoke `/articulate` again.

---

## Session Start

Run this for every non-first-run invocation (unless argument is `quick`).

### 1. Read State

Read `~/.articulate/state.json` and `~/.articulate/user.json`.

### 2. Calculate Streak

Parse `lastPlayedDate` from state. Get today's date as `YYYY-MM-DD`.

- **lastPlayedDate is today:** Streak unchanged. Increment `todayMissionCount`.
- **lastPlayedDate is yesterday:** Streak continues. Set `streak += 1`. Reset `todayMissionCount` to 0.
- **lastPlayedDate is older than yesterday:**
  - If `streakShields > 0` and missed exactly 1 day: consume one shield (`streakShields -= 1`), keep streak, reset `todayMissionCount`.
  - Otherwise: apply decay. Reset `streak` to 1. Reset `todayMissionCount` to 0.
- **lastPlayedDate is null:** First session ever. Set `streak` to 1, `todayMissionCount` to 0.

Update `lastPlayedDate` to today. Update `bestStreak` if `streak > bestStreak`.

### 3. Check Rank Decay

If `lastPlayedDate` was 7+ days ago: drop level by 1 (minimum level 1). XP is preserved. Show warning. 3 missions restore original rank.

### 4. Display Dashboard

Read `references/style.md` for formatting templates. Show:

- Rank badge + rank name + prestige stars (if any)
- XP bar: `current / next threshold` with progress bar
- Streak: `N days` with flame emoji (scale with streak length)
- Today's missions completed count
- If new badge earned since last session: celebrate
- If level-up happened: show level-up banner

### 5. Save Updated State

Write the recalculated streak, todayMissionCount, and lastPlayedDate to `~/.articulate/state.json`.

---

## Daily Word Ritual

Run after dashboard, before first mission of the session.

1. Check `state.json` fields `dailyWord` and `dailyWordDate`.
2. If `dailyWordDate` is not today: select a new daily word.
   - Prefer words not yet in `lexicon.json`, or words at "seen" mastery.
   - For word lists by level, read `references/languages/{lang}.md`.
3. Present the word: name, pronunciation hint, brief etymology, precise definition, example in context.
4. Challenge: "Use this word in today's mission for +5 bonus XP."
5. Save `dailyWord` and `dailyWordDate` to state.

After mission evaluation, check if the user's response contains the daily word. If yes, award the bonus.

---

## Mission Dispatch

### Direct Request

If `$ARGUMENTS` specifies a mission type, dispatch to that type after checking the unlock gate.

### Default Flow (empty or "go")

1. If `totalCompleted % 5 == 4` (every 5th mission) AND level >= 2 AND `history.json` has eligible entries older than 14 days: dispatch REVIEW.
2. Otherwise: weighted random selection from unlocked types.
   - Weight toward mission types that target the user's worst weaknesses (read `references/progression/weaknesses.md` for the six categories).
   - If context-aware is enabled and project context is available, pass it to mission generation.

### Dispatch

For each mission type, read the corresponding reference file. That file contains full generation, presentation, and evaluation rules.

| Type | Reference File |
|------|---------------|
| REWRITE | `references/missions/rewrite.md` |
| FILL_PRECISION | `references/missions/fill.md` |
| PROMPT_CRAFT | `references/missions/prompt.md` |
| SCENARIO | `references/missions/scenario.md` |
| BOSS | `references/missions/boss.md` |
| REVIEW | `references/missions/review.md` |

For template banks (curated challenges), read `templates/{type}-bank.md`.

---

## Post-Mission Flow

Run after EVERY completed mission.

### A. Score

Each mission type has its own rubric. Read `references/progression/scoring.md` for all rubrics.
Score range: 0-100.

### B. Calculate XP

```
base            = 10
score_bonus     = floor(score / 10)
streak_bonus    = min(streak * 2, 20)
daily_word_bonus = 5 if user used daily word, else 0
subtotal        = base + score_bonus + streak_bonus + daily_word_bonus

if boss mission:   subtotal = subtotal * 3
if critical hit:   subtotal = subtotal * 3
  (critical hit = 15% random chance AND score >= 80)

total_xp = subtotal
```

Show the full XP breakdown to the user.

### C. Level-Up Check

XP thresholds: 0, 100, 300, 600, 1000, 1800, 3000.

If `xp` crosses the next threshold: increment level, update rank and badge, show celebration banner (read `references/style.md`), announce newly unlocked mission types.

### D. Badge Check

Read `references/progression/levels.md` for all 14 badge conditions. Check every condition against current state. If a new badge is earned, add it to `earnedBadges` and show the badge celebration.

### E. Weakness Update

From the mission evaluation, identify which weakness categories the user kept or introduced. Increment relevant counters in `state.json` `weaknesses`. Append to `weaknessHistory` for trend tracking.

Read `references/progression/weaknesses.md` for the six categories and detection rules.

### F. Lexicon Update

Identify precision words the user successfully used.

- Word not in `lexicon.json`: add with mastery `"seen"`, `timesUsed: 1`.
- Word exists: increment `timesUsed`, update mastery tier:
  - 1 use: `seen`
  - 2 uses: `used`
  - 3 uses: `consistent`
  - 5+ uses across 2+ weeks: `mastered`

Save `lexicon.json`.

### G. Loot Drop

5-10% random chance after any mission. Drop a "precision gem": a powerful word with etymology, usage notes, and register info. Add to lexicon as `"seen"`. Display with special formatting (read `references/style.md`).

Read `references/progression/engagement.md` for full variable reward mechanics.

### H. Save State

Update all fields in `~/.articulate/state.json`:
- `xp`, `level`, `rank`, `badge`
- `streak`, `bestStreak`, `todayMissionCount`, `totalCompleted`
- `missionCounts` for the completed type
- `highScoreCount` (if score >= 90), `perfectCount` (if score == 100)
- `earnedBadges`, `weaknesses`, `weaknessHistory`
- `lastBossDate` (if boss mission)

Append mission entry to `~/.articulate/history.json`. Keep last 100 entries (FIFO — remove oldest if over 100).

Save `~/.articulate/lexicon.json`.

### I. Continue Prompt

Show: "Deploy another mission? Or save and return to base."

- User continues: skip dashboard, go straight to Mission Dispatch.
- User stops: show brief session summary (missions completed this session, XP earned, streak status).

---

## Stats Dashboard

Triggered by `/articulate stats`. Read `references/style.md` for formatting.

Display:

- **Overall:** total missions, total XP, rank, prestige stars
- **Per mission type:** count, average score, best score (calculate from `history.json`)
- **Streak:** current, best ever, shields held
- **Weakness radar:** all 6 categories with bars and trends (read `references/progression/weaknesses.md` for visualization format)
- **Lexicon summary:** total words, count per mastery tier (seen/used/consistent/mastered)
- **Recent performance:** last 10 missions with type, score, date

For `/articulate badges`: show all 14 badges, earned ones highlighted, unearned ones with unlock conditions.

For `/articulate lexicon`: show all words grouped by mastery tier with usage counts.

For `/articulate radar`: show the full weakness radar visualization.

---

## Help

Triggered by `/articulate help`. Show:

1. Available commands from the Argument Routing table.
2. Mark which commands are unlocked at the user's current level.
3. Mark locked commands with the level required.
4. Tips:
   - "Start with `/articulate` for a full session."
   - "Use `/articulate quick` to skip the dashboard."
   - "Add `--bg` or `--en` to force a language."

---

## Language Handling

Read `~/.articulate/user.json` for configured languages.

- Single language: use it for all missions.
- Multiple languages: alternate between them across sessions, or respect `--en`/`--bg` flags.
- For language-specific rules, word lists, and weakness patterns, read `references/languages/{lang}.md`.
  - English: `references/languages/english.md`
  - Bulgarian: `references/languages/bulgarian.md`

---

## Context-Aware Missions

Read `~/.articulate/user.json`. If `contextAware` is false, skip this section entirely.

If enabled:

1. Read `references/context-aware.md` for full context-gathering rules.
2. Check if `~/.articulate/contexts/{project-name}.json` exists and is fresh (< 7 days).
3. If missing or stale: scan project signals (README, package.json, Cargo.toml, etc.), extract summary, cache it.
4. Pass project context to mission generation so challenges reference the user's actual work.
