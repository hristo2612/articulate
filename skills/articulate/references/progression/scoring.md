# Progression — Scoring Rubrics & XP Formula

> Self-contained reference for scoring any session type, calculating XP,
> and displaying the breakdown.

---

## Scoring Rubrics by Session Type

Every session yields a score from 0 to 100. The rubric depends on the session
type. All scoring is deterministic — apply these axes exactly as specified.

### 🔍 Word Archaeology Rubric

| Axis | Max | What it measures |
|------|-----|------------------|
| Precision | 25 | Exact, specific word choices — no vague substitutes |
| Creativity | 25 | Inventive application of the word/principle — goes beyond the obvious |
| Principle Application | 25 | Demonstrates understanding of the etymology/connotation taught in the story |
| Naturalness | 25 | Reads like something a human would actually write — not forced or awkward |

### 🔥 Roast Rubric

| Axis | Max | What it measures |
|------|-----|------------------|
| Compression | 25 | Reduced word count without losing meaning — tighter is better |
| Weakness Elimination | 25 | Targeted weaknesses (hedging, vague nouns, fillers) are gone |
| Precision Gain | 25 | Replacement words are sharper, more specific, more vivid |
| Naturalness | 25 | Rewrite flows naturally — not robotic or over-edited |

For Roast sessions, always show the before/after comparison:

```
> **Before:** "I think we should basically try to make the system better and stuff."
> **After:**  "We need to optimize the caching layer."
>
> 🔻 12 → 7 words (42% compression)
> ✗ "I think", "basically", "stuff" eliminated
> ✓ "optimize the caching layer" — specific and actionable
```

### Scoring Guidelines (25-point scale)

- **25/25:** Exceptional — nothing to improve on this axis
- **20-24:** Strong — minor room for improvement
- **15-19:** Competent — noticeable weaknesses
- **10-14:** Developing — significant issues
- **0-9:** Needs work — axis not addressed

---

## XP Formula

XP is calculated after every completed session. All values are integers
(use floor rounding where needed).

### Formula

| Component | Formula | Range |
|-----------|---------|-------|
| base | 10 | 10 |
| score_bonus | floor(score / 10) | 0-10 |
| streak_bonus | min(streak × 2, 20) | 0-20 |
| **total_xp** | **base + score_bonus + streak_bonus** | **10-40** |

### Component Details

**base (10):**
Fixed reward for completing any session. Always 10.

**score_bonus (0-10):**
`floor(score / 10)`. A score of 73 yields 7. A perfect 100 yields 10.

**streak_bonus (0-20):**
`min(streak × 2, 20)`. Streak is the number of consecutive active days.
Caps at 20 (reached at a 10-day streak). A streak of 0 yields 0.

### XP Range Examples

| Scenario | XP |
|----------|-----|
| Minimum: score 0, no streak | 10 |
| Typical: score 70, 5-day streak | 10 + 7 + 10 = 27 |
| Strong: score 85, 10-day streak | 10 + 8 + 20 = 38 |
| Perfect: score 100, 10+ day streak | 10 + 10 + 20 = 40 |

---

## Score Display Format

After every session, show the full scoring breakdown. The user should
always understand exactly how their score was determined.

### Session Score Display

```
 precision        ████████████████████░░░░░  20/25
 creativity       ██████████████████░░░░░░░  18/25
 principle        ████████████████████████░  24/25
 naturalness      ██████████████████████░░░  22/25
 ────────────────────────────────────────────────
 TOTAL                                       84/100
```

### XP Breakdown Display

Always show immediately after the session score:

```
 base            +10
 score (84)       +8
 streak (12d)    +20
 ─────────────────────
 TOTAL           +38 XP
```

### Cumulative XP Display

After the XP breakdown, show cumulative progress:

```
 XP: 342 → 380/600  ████████████████░░░░░░░ 63%
 🟨 OPERATIVE → SPECIALIST in 220 XP
```

If a level-up occurs, show the level-up banner instead (see
`references/style.md` for template).
