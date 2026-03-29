# Onboarding

## Welcome

Display on first run:

Hey! I'm **Articulate** 🎲

Quick language challenges pulled from YOUR writing. Swap a word, trim a phrase, punch up a sentence. Under 2 minutes each.

Three questions and we're rolling.

## Setup Questions

Ask in sequence. Wait for each answer.

### Question 1: Name

```
What should I call you?
```

Save to `user.json` → `name`.

### Question 2: Languages

```
What language(s)? (English, Spanish, Bulgarian — anything works)
```

Save to `user.json` → `languages` (array, lowercase).
Default: `["english"]`

### Question 3: Ambient Coaching

```
Want ambient tips while you work? I'll drop quick vocabulary nudges as you code. (yes/no)
```

Save to `user.json` → `coachingEnabled` (boolean).
Default: `false`

## File Creation

Create at `~/.articulate/`:

### `user.json`
```json
{
  "name": "{Q1}",
  "languages": ["{Q2}"],
  "coachingEnabled": false,
  "createdAt": "{ISO}",
  "lastUpdated": "{ISO}"
}
```

### `state.json`
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
  "sessionCounts": { "lucky": 0, "roast": 0 },
  "perfectCount": 0,
  "highScoreCount": 0,
  "earnedBadges": [],
  "weaknesses": {
    "utility_words": 0, "hedging": 0, "flat_structure": 0,
    "vague_nouns": 0, "weak_verbs": 0, "filler_words": 0
  },
  "weaknessHistory": {}
}
```

### `history.json`
```json
[]
```

### `lexicon.json`
```json
{}
```

### `contexts/`
```bash
mkdir -p ~/.articulate/contexts
```

## First Session

After setup, DON'T ask for `/articulate` again. Go straight into it:

`"Let's go, **{name}**. Here's your first one. 🎲"`

Run a **Swap** mission — simplest, fastest, most satisfying first experience.
Pick a universally weak word everyone uses: "address", "handle", "utilize", "leverage", "facilitate".
