---
name: articulate
description: "Use when the user invokes /articulate — precision language training skill for building active vocabulary through guided writing missions"
---

Read reference files ONLY when needed for the current action. Do not pre-read all references.

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

### Schemas

**user.json** — Fields: `name` (string), `languages` (array, e.g. `["English"]`), `focusAreas` (array, e.g. `["prompt_engineering", "business_communication"]`), `dailyMinutes` (int), `selfAssessment` (1-5), `assessmentMethod` ("conversation_scan" | "dynamic"), `contextAware` (bool), `createdAt` (ISO8601), `lastUpdated` (ISO8601)

**state.json** — Fields: `xp`, `level`, `rank`, `badge`, `streak`, `bestStreak`, `streakShields`, `lastPlayedDate` (ISO8601 or null), `todayMissionCount`, `totalCompleted`, `prestigeStars`, `missionCounts` (object with keys: rewrite, fill, prompt, scenario, boss, review), `perfectCount`, `highScoreCount`, `earnedBadges` (array), `weaknesses` (object: utility_words, hedging, flat_structure, vague_nouns, weak_verbs, filler_words — all ints), `weaknessHistory` (object), `currentSeason`, `lastBossDate`, `dailyWord`, `dailyWordDate`

**history.json** — Array of entries (FIFO, max 100). Entry fields: `id` (uuid-v4), `date` (ISO8601), `type` (mission type), `language`, `projectContext` (string or null), `score` (0-100), `xpEarned`, `criticalHit` (bool), `weaknessesFound` (array of category strings), `challenge`, `userResponse`, `goldStandard`, `feedback`

**lexicon.json** — Object keyed by word. Each value: `mastery` ("seen"|"used"|"consistent"|"mastered"), `timesUsed` (int), `firstSeen` (ISO8601), `lastUsed` (ISO8601), `etymology` (string), `contexts` (array of strings)

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

Append `--{lang}` (first 2-3 letters of the language name) to any mission command to force a language. Example: `/articulate rewrite --bg` for Bulgarian, `/articulate rewrite --es` for Spanish.

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

Parse `lastPlayedDate` from state. Compare to today (`YYYY-MM-DD`):

- **Same day:** streak unchanged, increment `todayMissionCount`.
- **Yesterday:** `streak += 1`, reset `todayMissionCount` to 0.
- **Older:** if `streakShields > 0` and missed exactly 1 day, consume a shield and keep streak; otherwise reset `streak` to 1, `todayMissionCount` to 0.
- **Null (first session):** set `streak` to 1, `todayMissionCount` to 0.

Update `lastPlayedDate` to today. Update `bestStreak` if current streak exceeds it.

**Rank decay:** if 7+ days inactive, drop level by 1 (min 1, XP preserved). Show warning; 3 missions restore original rank.

### 3. Display Dashboard

Read `references/style.md` for formatting. Show rank badge + name + prestige stars, XP progress bar, streak with flame emoji, today's mission count, and any new badge or level-up celebrations.

### 4. Save Updated State

Write recalculated streak, todayMissionCount, and lastPlayedDate to `~/.articulate/state.json`.

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

### Dynamic Difficulty Recalibration

If `assessmentMethod` is `"dynamic"`, re-evaluate effective difficulty every 5 missions: average last 5 scores from `history.json`. If avg > 80, increase difficulty within level. If avg < 50, decrease.

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

XP = base(10) + score_bonus(floor(score/10)) + streak_bonus(min(streak*2, 20)) + daily_word(+5 if used). Boss missions: multiply by 3. Critical hit (15% chance, score>=80): multiply by 3. For full formula details, read `references/progression/scoring.md`. Show the full XP breakdown to the user.

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

Display: overall stats (missions, XP, rank, prestige), per-type breakdown (count, avg/best score from `history.json`), streak info, weakness radar (6 categories — see `references/progression/weaknesses.md`), lexicon summary (words per mastery tier), and last 10 missions.

Sub-commands: `/articulate badges` (all 14, earned highlighted, unearned with conditions), `/articulate lexicon` (words by mastery tier), `/articulate radar` (full weakness visualization).

---

## Help

Triggered by `/articulate help`. Show:

1. Available commands from the Argument Routing table.
2. Mark which commands are unlocked at the user's current level.
3. Mark locked commands with the level required.
4. Tips:
   - "Start with `/articulate` for a full session."
   - "Use `/articulate quick` to skip the dashboard."
   - "Add `--{lang}` to force a language (e.g., `--es` for Spanish)."

---

## Language Handling

Read `~/.articulate/user.json` for configured languages. Any language is supported.

- Single language: use it for all missions.
- Multiple languages: alternate between them across sessions, or respect `--{lang}` flags.
- For languages with a dedicated reference file in `references/languages/`, read it for curated word lists, weakness patterns, and language-specific rules. Shipped examples: `english.md`, `bulgarian.md`.
- For languages WITHOUT a reference file: generate appropriate precision vocabulary, weakness patterns, and exercise content dynamically. Use the same mission structure and scoring rubrics. The English and Bulgarian files serve as format examples.

---

## Context-Aware Missions

Read `~/.articulate/user.json`. If `contextAware` is false, skip this section entirely.

If enabled:

1. Read `references/context-aware.md` for full context-gathering rules.
2. Check if `~/.articulate/contexts/{project-name}.json` exists and is fresh (< 7 days).
3. If missing or stale: scan project signals (README, package.json, Cargo.toml, etc.), extract summary, cache it.
4. Pass project context to mission generation so challenges reference the user's actual work.
