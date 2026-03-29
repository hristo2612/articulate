# Progression — Levels, Badges & Rank Systems

> Self-contained reference for managing rank, badges, prestige,
> streak shields, and decay.

---

## Level Table

Seven ranks from RECRUIT to MASTERMIND. XP is cumulative — never resets unless
the user triggers a Prestige reset.

| Level | Rank | XP Threshold | Badge |
|-------|------|-------------|-------|
| 1 | RECRUIT | 0 | ⬜ |
| 2 | INITIATE | 100 | 🟩 |
| 3 | OPERATIVE | 300 | 🟨 |
| 4 | SPECIALIST | 600 | 🟧 |
| 5 | COMMANDER | 1000 | 🔴 |
| 6 | ARCHITECT | 1800 | 💎 |
| 7 | MASTERMIND | 3000 | 👑 |

### Level-Up Rules

All modes (Lucky missions, Roast, Ambient Coach) are available from Level 1.
Levels are motivational milestones, not unlock gates.

1. After every XP award, compare `state.json → xp` against the table above.
2. If XP crosses the next threshold, the user levels up.
3. Show a level-up banner (see `references/style.md` for template).
4. A single XP award can trigger multiple level-ups — check all thresholds.

### Dashboard Display

Show rank with badge emoji, XP progress bar toward next level, and streak:

```
 🟨 OPERATIVE  XP: 342/600  🔥 12d
 ████████████████░░░░░░░ 57%
 Today: 2 sessions  Total: 47
```

For MASTERMIND (max level), show XP total with no "next" threshold:

```
 👑 MASTERMIND  XP: 4210  🔥 45d
 ████████████████████████ MAX
 Today: 1 session  Total: 203
```

---

## Badge Collection

14 badges total. Each has a name, emoji, and unlock condition. Badges are
permanent — once earned, never lost (even through prestige resets or rank decay).

Store earned badges in `state.json → badges` as an array of badge IDs with
the ISO timestamp of when they were earned.

| Badge | Name | Condition |
|-------|------|-----------|
| ⚡ | First Blood | Complete first session |
| 🔥 | On Fire | Achieve a 3-day streak |
| 💀 | Unstoppable | Achieve a 7-day streak |
| 🤖 | Machine | Achieve a 30-day streak |
| 🎯 | Precision Strike | Score 90+ on 5 sessions |
| 🏆 | Sharpshooter | Score 90+ on 20 sessions |
| 🎲 | Lucky Streak | Complete 10 Lucky missions |
| 🔥 | Roast Master | Complete 10 Roast sessions |
| 🎖️ | Veteran | Complete 50 total sessions |
| ⚔️ | Centurion | Complete 100 total sessions |
| 💪 | Powerhouse | Earn 1000 cumulative XP |
| 🌍 | Polyglot | Complete sessions in 2+ languages |
| 📈 | Improver | Any weakness category drops 30+ points from peak |

### Badge Check Logic

After every session completion, run these checks in order:

1. **⚡ First Blood** — `history.json` length >= 1
2. **🔥 On Fire** — `state.json → streak` >= 3
3. **💀 Unstoppable** — `state.json → streak` >= 7
4. **🤖 Machine** — `state.json → streak` >= 30
5. **🎯 Precision Strike** — count entries in `history.json` where `score >= 90` >= 5
6. **🏆 Sharpshooter** — count entries in `history.json` where `score >= 90` >= 20
7. **🎲 Lucky Streak** — `state.json → sessionCounts.lucky` >= 10
8. **🔥 Roast Master** — `state.json → sessionCounts.roast` >= 10
9. **🎖️ Veteran** — `history.json` length >= 50
10. **⚔️ Centurion** — `history.json` length >= 100
11. **💪 Powerhouse** — `state.json → xp` >= 1000
12. **🌍 Polyglot** — distinct `language` values in `history.json` >= 2
13. **📈 Improver** — any weakness category in `state.json → weaknessHistory` dropped 30+ percentage points from its recorded peak

If a badge is newly earned (not already in `state.json → badges`):
- Add it with timestamp
- Show the badge-earned celebration (see `references/style.md`)
- Multiple badges can trigger in a single session — show all

### Badge Display Format

When displaying the badge shelf (e.g., in dashboard or stats):

```
 ⚡ 🔥 💀 ✏️ 🎯 💪            [6/14]
```

Show earned badges in order. Unearned badges are omitted — show the count
`[earned/14]` to indicate progress.

---

## Prestige System

Available only at Level 7 (MASTERMIND). Prestige is optional and user-
initiated — never prompt or auto-trigger.

### How It Works

1. Operator reaches MASTERMIND (3000+ XP) and requests prestige reset.
2. Confirm with the user: "Prestige resets your rank to RECRUIT and
   zeroes your XP. Badges are preserved. Proceed?"
3. On confirmation:
   - Set `state.json → level` to 1
   - Set `state.json → rank` to `"RECRUIT"`
   - Set `state.json → xp` to 0
   - Increment `state.json → prestige` by 1
   - DO NOT clear `state.json → badges`
   - DO NOT clear `history.json`
   - DO NOT clear `lexicon.json`
4. Show prestige celebration banner (see `references/style.md`).

### Star Markers

Each prestige run adds one star to the rank display.

```
 Prestige 0:  🟨 OPERATIVE
 Prestige 1:  🟨 OPERATIVE ★
 Prestige 2:  🟨 OPERATIVE ★★
 Prestige 3:  🟨 OPERATIVE ★★★
```

Stars accumulate indefinitely.

### Prestige Focus

Each prestige run can optionally focus on a different language or domain.
Store in `state.json → prestigeFocus`:

```json
{
  "prestige": 2,
  "prestigeHistory": [
    { "run": 1, "focus": "english_business", "completedAt": "2026-02-15" },
    { "run": 2, "focus": "bulgarian_general", "completedAt": null }
  ]
}
```

---

## Streak Shields

Protection against losing a streak due to a single missed day.

### Earning Shields

Shields are awarded at these streak milestones:

| Milestone | Shields Earned |
|-----------|---------------|
| 30-day | +1 shield |
| 60-day | +1 shield |
| 100-day | +1 shield |

Shields are earned the moment the streak hits the milestone. They are stored
in `state.json → streakShields`.

### Shield Rules

- **Maximum held:** 2 shields at any time. If already holding 2 when a
  milestone is reached, the new shield is lost.
- **Auto-consume:** When the system detects a missed day during session start,
  check if shields > 0. If yes: decrement shield count by 1, preserve streak,
  show notification: `"Streak shield deployed — streak preserved at {N} days."`
- **One per gap:** Each shield covers exactly one missed calendar day. Two
  consecutive missed days require two shields.
- **Display:** Show shield count in dashboard: `⛊ x2`

### State Format

```json
{
  "streak": 45,
  "streakShields": 1,
  "lastActiveDate": "2026-03-28"
}
```

---

## Rank Decay

Prevents rank inflation from abandoned training. Encourages consistency.

### Trigger

7 consecutive calendar days with zero completed sessions.

### Effect

- Rank drops by 1 level (e.g., SPECIALIST → OPERATIVE).
- XP is **preserved** — only the rank display changes.
- Cannot decay below RECRUIT (Level 1).
- Each subsequent 7-day inactive period causes another rank drop.

### Detection Logic (Session Start)

```
days_inactive = today - state.json → lastActiveDate

if days_inactive >= 7:
  decay_levels = floor(days_inactive / 7)
  new_level = max(1, state.json → level - decay_levels)

  if new_level < state.json → level:
    state.json → level = new_level
    state.json → rank = RANK_TABLE[new_level]
    show decay notification
```

### Decay Notification

```
 ⚠ {days_inactive} days inactive.
 Rank dropped: {old_rank} → {new_rank}
 XP preserved at {xp}.
 Complete 3 sessions to restore your rank.
```

### Restoration

- After rank decay, the user must complete **3 sessions** to restore
  their rank to the level their XP warrants.
- Track restoration progress in `state.json → decayRecovery`:

```json
{
  "decayRecovery": {
    "active": true,
    "sessionsRequired": 3,
    "sessionsCompleted": 1,
    "targetLevel": 4,
    "targetRank": "SPECIALIST"
  }
}
```

- After each session during recovery, increment `sessionsCompleted`.
- When `sessionsCompleted >= 3`:
  - Set level and rank to what XP warrants (recalculate from XP thresholds).
  - Clear `decayRecovery`.
  - Show restoration message: `"Rank restored: {rank} — welcome back."`

### Interaction with Streak

- Rank decay and streak loss are independent systems.
- Streak resets after 1 missed day (unless shielded).
- Rank decays after 7 missed days.
- Both can trigger simultaneously on a long absence.
