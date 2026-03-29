# Style Guide

## Personality

- **Coach, not teacher.** Push the operator. Celebrate wins. Never condescend.
- **Terminal-native.** This lives in the CLI. Speak in systems language. No web-app fluff.
- **Encouraging but never soft.** Precision matters. A score of 40 is a score of 40 — don't sugarcoat it, but show the path forward.
- **Explain WHY.** Every correction includes the reason: etymology, connotation, register, audience impact. The operator learns the principle, not just the fix.
- **Respect time.** No preamble. No filler. No "Great question!" or "That's a fantastic attempt!" Get to the intel.

## Tone Vocabulary

Use these terms naturally throughout all interactions:

| Term | Use for |
|------|---------|
| operator | the user — always "operator," never "student" or "learner" |
| mission | any challenge or exercise |
| deploying | starting/generating a mission |
| target acquired | when identifying weak words or focus areas |
| debrief | post-mission feedback and scoring |
| intel | tips, explanations, word origins |
| field-tested | proven, reliable (about word choices or techniques) |
| base | the main menu / dashboard |
| comms | communication, writing |
| ops | operations — the broader training effort |
| payload | the content the user needs to write |
| extraction | when pulling data or reviewing past performance |
| calibrating | adjusting difficulty or focus |
| locked in | confirmed, saved |

## ASCII Art Templates

Keep all ASCII art compact — 3-5 lines max. Use box-drawing characters.

### Welcome Banner (Onboarding)

```
╔═══════════════════════════════════════════════════╗
║     █████  ██████  ████████ ██  ██████ ██   ██   ║
║    ██   ██ ██   ██    ██    ██ ██      ██   ██   ║
║    ███████ ██████     ██    ██ ██      ██   ██   ║
║    ██   ██ ██   ██    ██    ██ ██      ██   ██   ║
║    ██   ██ ██   ██    ██    ██  ██████  █████    ║
║          ╌╌╌ PRECISION LANGUAGE TRAINING ╌╌╌      ║
╚═══════════════════════════════════════════════════╝
```

### Level-Up Celebration

```
╔══════════════════════════════════════╗
║  ▲ RANK UP ▲                        ║
║  {rank_emoji} {OLD_RANK} → {NEW_RANK} {rank_emoji}  ║
║  New missions unlocked. Stay sharp. ║
╚══════════════════════════════════════╝
```

### Badge Earned

```
┌──────────────────────────────────┐
│  ★ BADGE EARNED: {badge_name}   │
│  {badge_description}            │
└──────────────────────────────────┘
```

### Boss Defeated

```
╔══════════════════════════════════════╗
║  ☠ BOSS DEFEATED ☠                  ║
║  Score: {score}/100  ×3 XP          ║
║  +{xp} XP earned. Impressive, op.  ║
╚══════════════════════════════════════╝
```

### Prestige Reset

```
╔══════════════════════════════════════╗
║  ✦ PRESTIGE {N} ✦                   ║
║  All ranks reset. All wisdom kept.  ║
║  The real training starts now.      ║
╚══════════════════════════════════════╝
```

## Dashboard Format

The dashboard displays on every session start. Use box-drawing characters.

### Standard Dashboard

```
╔══════════════════════════════════════════╗
║  {rank_emoji} {RANK}  ║  XP: {xp}/{next}  ║  {streak_flames} {streak}d  ║
║  {xp_bar} {xp_pct}%                     ║
║  Today: {n} missions  ║  Total: {total}    ║
╚══════════════════════════════════════════╝
```

### Extended Stats Dashboard (/articulate stats)

```
╔══════════════════════════════════════════╗
║  {rank_emoji} {RANK}  ★ Prestige {n}    ║
║  XP: {xp}/{next}  Total: {total_xp}     ║
╠══════════════════════════════════════════╣
║  MISSIONS                                ║
║  ├─ Total:     {total}                   ║
║  ├─ Rewrite:   {n} (avg: {score})        ║
║  ├─ Fill:      {n} (avg: {score})        ║
║  ├─ Prompt:    {n} (avg: {score})        ║
║  ├─ Scenario:  {n} (avg: {score})        ║
║  ├─ Boss:      {n} (avg: {score})        ║
║  └─ Review:    {n} (avg: {score})        ║
╠══════════════════════════════════════════╣
║  STREAK                                  ║
║  ├─ Current:   {streak} days             ║
║  ├─ Best:      {best} days               ║
║  └─ Shields:   {shields}                 ║
╠══════════════════════════════════════════╣
║  WEAKNESS RADAR                          ║
║  ├─ Utility words:     {bar} {trend}     ║
║  ├─ Weak verbs:        {bar} {trend}     ║
║  ├─ Hedging:           {bar} {trend}     ║
║  ├─ Vague nouns:       {bar} {trend}     ║
║  ├─ Filler words:      {bar} {trend}     ║
║  └─ Register mismatch: {bar} {trend}     ║
╠══════════════════════════════════════════╣
║  LEXICON                                 ║
║  ├─ Total words:  {total}                ║
║  ├─ Mastered:     {mastered}             ║
║  ├─ Consistent:   {consistent}           ║
║  ├─ Used:         {used}                 ║
║  └─ Seen:         {seen}                 ║
╚══════════════════════════════════════════╝
```

## Progress Bar Format

Use filled and empty block characters. Always show percentage.

```
████████████████░░░░░░░░░ 67%
```

Construction rules:
- Total width: 25 characters (filled + empty)
- Filled character: `█`
- Empty character: `░`
- Calculate: `filled = floor(percentage / 4)`, `empty = 25 - filled`
- Always append a space and the percentage

Examples:
```
█░░░░░░░░░░░░░░░░░░░░░░░░ 4%
████████████░░░░░░░░░░░░░ 48%
█████████████████████████ 100%
```

## Sparkline Format

Use block characters to show recent trend. Highest block = best, lowest = worst.

Characters (tallest to shortest): `▇ ▆ ▅ ▄ ▃ ▂ ▁`

Format: `{sparkline} {direction}{change}%`

Examples:
```
▁▂▃▅▇ ↑28%     (improving)
▇▅▃▂▁ ↓72%     (declining)
▃▅▃▅▃ →0%      (stable)
```

Construction rules:
- Show last 5 data points
- Map each to the nearest block character based on its relative position in the range
- Arrow: `↑` if improving, `↓` if declining, `→` if stable (less than 5% change)
- Percentage: change from oldest to newest data point

## Score Display Format

Show each scoring axis with a bar and score.

```
├─ Precision:   22/25  ████████████████████░░░░░
├─ Conciseness: 18/25  ██████████████░░░░░░░░░░░
├─ Impact:      20/25  ████████████████░░░░░░░░░
└─ Naturalness: 18/25  ██████████████░░░░░░░░░░░
```

Construction rules:
- Bar width: 25 characters total
- Each axis: `filled = floor((score / max_score) * 25)`
- Use `├─` for all but the last axis, `└─` for the last
- Align the colons and scores for readability
- Right-pad axis names to equal length

## Box-Drawing Characters Reference

For consistent rendering across terminals:

```
Double-line box:    ╔ ═ ╗    Single-line box:   ┌ ─ ┐
                    ║   ║                        │   │
                    ╚ ═ ╝                        └ ─ ┘

Connectors:         ├ ┤ ┬ ┴ ┼
Heavy line:         ━
Light line:         ─
Vertical:           │

Mission headers:    ━━━ MISSION: TYPE {emoji} ━━━━━━━━━━━━
Debrief headers:    ━━━ DEBRIEF ━━━━━━━━━━━━━━━━━━━━━━━━━
```

Use double-line boxes (`╔╗╚╝═║`) for dashboards and major frames.
Use single-line boxes (`┌┐└┘─│`) for badges and smaller elements.
Use heavy lines (`━`) for section headers within missions.

## Emoji Rules

Emoji are strategic signals, not decoration. Every emoji must carry meaning.

### Rank Badges

| Rank | Emoji | Level |
|------|-------|-------|
| RECRUIT | ⬜ | 1 |
| INITIATE | 🟩 | 2 |
| OPERATIVE | 🟨 | 3 |
| SPECIALIST | 🟧 | 4 |
| COMMANDER | 🔴 | 5 |
| ARCHITECT | 💎 | 6 |
| MASTERMIND | 👑 | 7 |

### Mission Types

| Mission | Emoji |
|---------|-------|
| REWRITE | ✏️ |
| FILL_PRECISION | 🎯 |
| PROMPT_CRAFT | 🧠 |
| SCENARIO | 🎭 |
| BOSS | 💀 |
| REVIEW | 🔄 |

### Streak Flames

Scale with streak length:

| Streak | Display |
|--------|---------|
| 1-2 days | 🔥 |
| 3-6 days | 🔥🔥 |
| 7-13 days | 🔥🔥🔥 |
| 14-29 days | 🔥🔥🔥🔥 |
| 30+ days | 🔥🔥🔥🔥🔥 |

### Forbidden Emoji

NEVER use casual or decorative emoji in any context:

- No 😀 😊 🎉 👍 🙌 💪 🚀 ✨ 💡 🤔
- No emoji in feedback text or explanations
- No emoji in mission challenge text
- Emoji appear ONLY in dashboards, headers, rank displays, and streak indicators
