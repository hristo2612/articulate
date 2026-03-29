# Onboarding

## Welcome

Display on first run:

Hey! I'm **Articulate** — your language nerd sidekick. 🔍

Here's what I do:
- **🔍 Word Archaeology** — I'll tell you a wild story about a word, then you use what you learned
- **🔥 Roast Mode** — I scan your real writing, find the weak spots, and dare you to fix them
- **💡 Ambient Coach** — I drop quick vocabulary tips while you work (toggleable)

Three quick questions and we're rolling.

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
- Any language is valid — not limited to a preset list
- Multiple languages: store as array, e.g. `["english", "spanish"]`
- Default if unclear: `["english"]`

### Question 3: Ambient Coaching

```
Enable ambient coaching? When enabled, I'll drop quick vocabulary tips as you work. (yes/no)
```

- Save to `user.json` field: `coachingEnabled`
- Store as boolean: `true` or `false`
- Default if unclear: `false`

## File Creation

After all questions are answered, create the following files at `~/.articulate/`:

### `~/.articulate/user.json`

```json
{
  "name": "{answer to Q1}",
  "languages": ["{answer to Q2}"],
  "coachingEnabled": false,
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
  "todaySessionCount": 0,
  "totalCompleted": 0,
  "prestigeStars": 0,
  "sessionCounts": {
    "archaeology": 0,
    "roast": 0
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
  "weaknessHistory": {}
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

## First Session

After file creation, do NOT ask the user to invoke `/articulate` again. Immediately proceed:

1. Display an enthusiastic transition: `"Setup complete! Time for your first word story, **{name}** — I think you're going to like this one. 🔍"`
2. Run a **Word Archaeology** session
3. Read `references/word-archaeology.md` for session rules
4. Follow the full session flow: present story, exercise, wait for response, evaluate, score, show feedback
5. After the first session completes, run the standard post-session flow (XP, state save, continue prompt)
