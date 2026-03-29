# Onboarding

## Welcome

Display on first run:

**ARTICULATE** — Precision Language Training

## Intro Text

```
Welcome, operator. You write. We evaluate. You level up.
Let's configure your training profile.
```

## Setup Questions

Ask these in sequence. Wait for the user's answer to each before proceeding.

### Question 1: Name

```
What should I call you?
```

- Save to `user.json` field: `name`
- Any non-empty string is valid

### Question 2: Languages

```
What language(s) do you want to train in? (e.g., English, Spanish, Bulgarian — any language works)
```

- Save to `user.json` field: `languages`
- Parse the user's answer into an array of language names, normalized to lowercase
- Any language is valid — not limited to English and Bulgarian
- Multiple languages: store as array, e.g. `["english", "spanish"]`
- Default if unclear: `["english"]`

### Question 3: Focus Areas

```
Focus areas? Pick 1-3 (enter numbers, e.g. "1,3,5"):

  1. prompt_engineering
  2. business_communication
  3. technical_writing
  4. interview_prep
  5. general_fluency
```

- Save to `user.json` field: `focusAreas`
- Store as array of strings, e.g. `["prompt_engineering", "technical_writing"]`
- Must pick at least 1, max 3

### Question 4: Daily Training Target

```
Daily training target in minutes? (default: 5)
```

- Save to `user.json` field: `dailyMinutes`
- Must be a positive integer
- Default: `5`

### Question 5: Self-Assessment

```
Want me to scan your recent conversations to assess your vocabulary level? (yes/no)
```

- If **yes**: Analyze the current session's prior messages (the conversation context before `/articulate` was invoked) for: vocabulary precision, hedging frequency, utility word usage, structural variety. Derive a score 1-5 with brief reasoning shown to the user. Save to `user.json` field `selfAssessment`. Save `"assessmentMethod": "conversation_scan"` to `user.json`.
- If **no**: Set `selfAssessment` to `3` (mid-range). Save `"assessmentMethod": "dynamic"`. The system calibrates dynamically from mission performance — no need to self-assess.
- Difficulty calibration:
  - 1-2: start with easiest RECRUIT challenges
  - 3: standard RECRUIT challenges
  - 4-5: slightly harder RECRUIT challenges (still Level 1, but tougher within tier)

### Question 6: Context-Aware Missions

```
Enable context-aware missions? (yes/no)
These use your project's README and package.json to generate relevant challenges.
```

- Save to `user.json` field: `contextAware`
- Store as boolean: `true` or `false`
- Default if unclear: `false`

## File Creation

After all questions are answered, create the following files at `~/.articulate/`:

### `~/.articulate/user.json`

```json
{
  "name": "{answer to Q1}",
  "languages": ["{answer to Q2}"],
  "focusAreas": ["{answers to Q3}"],
  "dailyMinutes": {answer to Q4},
  "selfAssessment": {answer to Q5},
  "assessmentMethod": "{conversation_scan or dynamic}",
  "contextAware": {answer to Q6},
  "createdAt": "{ISO date}",
  "lastUpdated": "{ISO date}"
}
```

### `~/.articulate/state.json`

```json
{
  "xp": 0,
  "level": 1,
  "rank": "RECRUIT",
  "badge": "⬜",
  "streak": 0,
  "bestStreak": 0,
  "streakShields": 0,
  "lastPlayedDate": null,
  "todayMissionCount": 0,
  "totalCompleted": 0,
  "prestigeStars": 0,
  "missionCounts": {
    "rewrite": 0,
    "fill": 0,
    "prompt": 0,
    "scenario": 0,
    "boss": 0,
    "review": 0
  },
  "perfectCount": 0,
  "highScoreCount": 0,
  "earnedBadges": [],
  "weaknesses": {
    "utility_words": 0,
    "hedging": 0,
    "flat_structure": 0,
    "vague_nouns": 0,
    "weak_verbs": 0,
    "filler_words": 0
  },
  "weaknessHistory": {},
  "currentSeason": null,
  "lastBossDate": null,
  "dailyWord": null,
  "dailyWordDate": null
}
```

### `~/.articulate/history.json`

```json
[]
```

### `~/.articulate/lexicon.json`

```json
{}
```

### `~/.articulate/contexts/`

Create as an empty directory:

```bash
mkdir -p ~/.articulate/contexts
```

## First Mission

After file creation, do NOT ask the user to invoke `/articulate` again. Immediately proceed:

1. Display a brief confirmation: `"Profile locked in. Deploying your first mission, {name}."`
2. Run a REWRITE mission at easy difficulty (RECRUIT level)
3. Read `references/missions/rewrite.md` for mission rules
4. Generate a simple sentence with 2-3 obvious weak words
5. If `selfAssessment` is 1-2, use the simplest possible challenge
6. Follow the full mission flow: present challenge, wait for response, evaluate, score, show debrief
7. After the first mission completes, run the standard post-mission flow (XP, state save, continue prompt)
