# Progression — Scoring Rubrics & XP Formula

> Self-contained reference for scoring any mission type, calculating XP,
> and displaying the breakdown.

---

## Scoring Rubrics by Mission Type

Every mission yields a score from 0 to 100. The rubric depends on the mission
type. All scoring is deterministic — apply these axes exactly as specified.

| Type | Axes | Max | Full rubric |
|------|------|-----|-------------|
| REWRITE | Precision, Conciseness, Impact, Naturalness | 4x25=100 | references/missions/rewrite.md |
| FILL | Exact/Synonym/Acceptable/Weak/Wrong tiers | 100 | references/missions/fill.md |
| PROMPT_CRAFT | Specificity, Constraints, Structure, Clarity, Register | 5x20=100 | references/missions/prompt.md |
| SCENARIO | Word Choice, Register, Goal, Conciseness, Persuasiveness | 5x20=100 | references/missions/scenario.md |
| BOSS | Average of parts (each scored by its type rubric) | 100 | references/missions/boss.md |
| REVIEW | Same rubric as original mission type | 100 | references/missions/review.md |

**Scoring guidelines (4-axis missions, 25-point scale):**
- 25/25: Exceptional — nothing to improve on this axis
- 20-24: Strong — minor room for improvement
- 15-19: Competent — noticeable weaknesses
- 10-14: Developing — significant issues
- 0-9: Needs work — axis not addressed

**Scoring guidelines (5-axis missions, 20-point scale):**
- 20/20: Exceptional — textbook example of this axis
- 16-19: Strong — minor room for improvement
- 12-15: Competent — noticeable weaknesses
- 8-11: Developing — significant issues
- 0-7: Needs work — axis not addressed

**FILL evaluation order:** Check exact match first, then strong synonyms,
then acceptable, then weak. Default to 0 if none match.

**BOSS formula:** `boss_score = floor(sum(part_scores) / number_of_parts)`

**REVIEW:** Use the same rubric as the original mission type. Compare the
new score against the original to show improvement.

---

## XP Formula

XP is calculated after every completed mission. All values are integers
(use floor rounding where needed).

### Formula

| Component | Formula | Range |
|-----------|---------|-------|
| base | 10 | 10 |
| score_bonus | floor(score / 10) | 0-10 |
| streak_bonus | min(streak * 2, 20) | 0-20 |
| daily_word_bonus | 5 if daily word used in response, else 0 | 0 or 5 |
| subtotal | base + score_bonus + streak_bonus + daily_word_bonus | 10-45 |
| BOSS multiplier | if boss mission: subtotal * 3 | x3 |
| Critical Hit | if critical_hit triggers: subtotal * 3 | x3 |
| total_xp | subtotal | — |

### Component Details

**base (10):**
Fixed reward for completing any mission. Always 10.

**score_bonus (0-10):**
`floor(score / 10)`. A score of 73 yields 7. A perfect 100 yields 10.

**streak_bonus (0-20):**
`min(streak * 2, 20)`. Streak is the number of consecutive active days.
Caps at 20 (reached at a 10-day streak). A streak of 0 yields 0.

**daily_word_bonus (0 or 5):**
Flat +5 XP if the operator used the daily word (or its morphological
variants) in their mission response.

**BOSS multiplier (x3):**
Applied when the mission type is BOSS. Multiplies the entire subtotal by 3.
This makes BOSS missions the highest-XP missions available.

**Critical Hit (x3):**
A random variable reward. Triggers when BOTH conditions are met:
1. Random roll: 15% chance (generate random 0-1, trigger if < 0.15)
2. Score gate: mission score must be >= 80

When triggered, multiply the subtotal by 3. Show the critical hit animation
(see `references/progression/engagement.md` for display details).

**BOSS + Critical Hit stacking:**
If a BOSS mission also triggers a critical hit, both multipliers apply
sequentially: `subtotal * 3 * 3 = subtotal * 9`. This is intentional — it
is the jackpot scenario.

### XP Range Examples

| Scenario | XP |
|----------|-----|
| Minimum: score 0, no streak, no bonuses | 10 |
| Typical: score 70, 5-day streak | 10 + 7 + 10 = 27 |
| Strong: score 85, 10-day streak, daily word | 10 + 8 + 20 + 5 = 43 |
| Boss (strong): same as above, boss mission | 43 * 3 = 129 |
| Jackpot: boss + crit hit on score 90 | (10 + 9 + 20 + 5) * 9 = 396 |

---

## Score Display Format

After every mission, show the full scoring breakdown. The operator should
always understand exactly how their score was determined.

### Mission Score Display

For multi-axis missions (REWRITE, PROMPT_CRAFT, SCENARIO):

```
 precision      ████████████████████░░░░░  20/25
 conciseness    ██████████████████░░░░░░░  18/25
 impact         ████████████████████████░  24/25
 naturalness    ██████████████████████░░░  22/25
 ────────────────────────────────────────────────
 TOTAL                                     84/100
```

For FILL missions:

```
 Your answer: "mitigate"
 Target:      "mitigate"
 Tier:        EXACT MATCH
 Score:       100/100
```

For BOSS missions:

```
 Part 1 (REWRITE):   85/100
 Part 2 (FILL):      80/100
 Part 3 (SCENARIO):  90/100
 ────────────────────────────────────────────────
 COMPOSITE:          85/100
```

For REVIEW missions:

```
 Original: 62  →  Review: 78  (+16)
```

### XP Breakdown Display

Always show immediately after the mission score:

```
 base            +10
 score (84)       +8
 streak (12d)    +20
 daily word       +5
 ─────────────────────
 subtotal         43
 TOTAL           +43 XP
```

With BOSS multiplier: add `BOSS (x3)` line before TOTAL.
With Critical Hit: add `CRITICAL HIT (x3)` line before TOTAL.

### Cumulative XP Display

After the XP breakdown, show cumulative progress:

```
 XP: 342 → 385/600  ████████████████░░░░░░░ 64%
 🟨 OPERATIVE → SPECIALIST in 215 XP
```

If a level-up occurs, show the level-up banner instead (see
`references/style.md` for template).
