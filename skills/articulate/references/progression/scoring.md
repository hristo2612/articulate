# Progression — Scoring Rubrics & XP Formula

> Self-contained reference. An AI agent reading only this file has everything
> needed to score any mission type, calculate XP, and display the breakdown.

---

## Scoring Rubrics by Mission Type

Every mission yields a score from 0 to 100. The rubric depends on the mission
type. All scoring is deterministic — apply these axes exactly as specified.

---

### REWRITE — 4 axes x 25 points = 100

Evaluate the operator's rewrite against these four axes:

```
━━━ REWRITE SCORING ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 Axis           Max  Criteria
 ─────────────  ───  ──────────────────────────────────────────────────
 Precision       25  Replaced vague/weak words with exact alternatives.
                     Each utility word, hedge, or filler that survives
                     costs points. Bonus for etymologically rich choices.

 Conciseness     25  Reduced word count without losing meaning.
                     Ideal: 20-40% shorter. Penalize padding, redundancy,
                     throat-clearing. Zero-value words should be gone.

 Impact          25  The rewrite lands harder. Stronger verbs, sharper
                     nouns, better rhythm. Does it persuade, clarify, or
                     move the reader more than the original?

 Naturalness     25  Reads like a competent human wrote it — not like a
                     thesaurus exploded. No forced formality, no awkward
                     register shifts, no show-off vocabulary that obscures.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Scoring guidelines:**
- 25/25: Exceptional — nothing to improve on this axis
- 20-24: Strong — minor room for improvement
- 15-19: Competent — noticeable weaknesses
- 10-14: Developing — significant issues
- 0-9: Needs work — axis not addressed

---

### FILL (Fill the Blank) — Tiered Exact Scoring

The operator fills a blank with a single word. Score is determined by
comparing their answer against the target word and acceptable alternatives.

```
━━━ FILL SCORING ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 Tier              Score  Criteria
 ────────────────  ─────  ─────────────────────────────────────────────
 Exact match        100   Matches the target word exactly (case-
                          insensitive). Includes morphological variants
                          (e.g., "mitigate" matches "mitigates").

 Strong synonym      80   A precise synonym that fits the register and
                          context equally well. Defined per challenge in
                          the template bank or evaluated at runtime.

 Acceptable          60   Fits the sentence grammatically and semantically
                          but lacks the precision or register of the target.
                          A correct answer, not the best answer.

 Weak                30   Technically works but misses the point of the
                          challenge. Wrong register, too vague, or too
                          generic. Shows partial understanding.

 Wrong                0   Does not fit grammatically, semantically, or
                          contextually. Includes blanks and nonsense.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Evaluation order:** Check exact match first, then strong synonyms, then
acceptable, then weak. Default to 0 if none match.

---

### PROMPT_CRAFT — 5 axes x 20 points = 100

Evaluate the operator's crafted prompt against these five axes:

```
━━━ PROMPT_CRAFT SCORING ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 Axis           Max  Criteria
 ─────────────  ───  ──────────────────────────────────────────────────
 Specificity     20  Prompt is precise about what it wants. No ambiguity
                     in the desired output. Defines scope clearly.

 Constraints     20  Includes useful constraints (length, format, tone,
                     audience, exclusions). Not over-constrained to the
                     point of being unusable.

 Structure       20  Well-organized. Uses sections, bullets, or numbered
                     steps where appropriate. Easy for an LLM to parse.

 Clarity         20  Language is clear, direct, unambiguous. No jargon
                     without context. Instructions parse on first read.

 Register        20  Appropriate tone for the target audience and use
                     case. Matches the stated scenario.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Scoring guidelines:**
- 20/20: Exceptional — textbook example of this axis
- 16-19: Strong — minor room for improvement
- 12-15: Competent — noticeable weaknesses
- 8-11: Developing — significant issues
- 0-7: Needs work — axis not addressed

---

### SCENARIO — 5 axes x 20 points = 100

Evaluate the operator's scenario response (email, message, pitch, etc.):

```
━━━ SCENARIO SCORING ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 Axis              Max  Criteria
 ────────────────  ───  ──────────────────────────────────────────────
 Word Choice        20  Precise, vivid vocabulary. No utility words or
                        hedging. Every word earns its place.

 Register           20  Matches the stated context (formal email, casual
                        Slack, investor pitch, etc.). No register drift.

 Goal Achievement   20  The response accomplishes what the scenario asks
                        for. If the goal is to decline, it declines. If
                        the goal is to persuade, it persuades.

 Conciseness        20  No wasted words. Tight prose. Appropriate length
                        for the medium (Slack != formal letter).

 Persuasiveness     20  The response would achieve its real-world goal.
                        Compelling, credible, and well-structured for
                        the target audience.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

### BOSS — Composite Scoring

BOSS missions combine multiple parts (e.g., a REWRITE + a FILL + a SCENARIO).
Each part is scored by its respective type rubric above.

```
boss_score = floor(sum(part_scores) / number_of_parts)
```

Example: A BOSS mission with 3 parts scoring 85, 70, 90:
```
boss_score = floor((85 + 70 + 90) / 3) = floor(81.67) = 81
```

Display the breakdown of each part with its type label and score, followed
by the composite score.

---

### REVIEW — Mirror Scoring

REVIEW missions present a previous mission for the operator to re-attempt.
The scoring rubric is the same as the original mission type.

- If reviewing a REWRITE, use REWRITE rubric.
- If reviewing a SCENARIO, use SCENARIO rubric.
- Compare the new score against the original to show improvement.

```
━━━ REVIEW COMPARISON ━━━━━━━━━━━━━━━━━━━
 Original: 62  →  Review: 78  (+16)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## XP Formula

XP is calculated after every completed mission. All values are integers
(use floor rounding where needed).

### Formula

```
━━━ XP CALCULATION ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 Component          Formula                    Range
 ────────────────   ─────────────────────────  ──────
 base               10                         10
 score_bonus        floor(score / 10)          0-10
 streak_bonus       min(streak * 2, 20)        0-20
 daily_word_bonus   5 if daily word used       0 or 5
                    in response, else 0

 subtotal           base + score_bonus
                    + streak_bonus
                    + daily_word_bonus         10-45

 BOSS multiplier    if boss mission:           x3
                    subtotal = subtotal * 3

 Critical Hit       if critical_hit triggers:  x3
                    subtotal = subtotal * 3

 total_xp           subtotal

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Component Details

**base (10):**
Fixed reward for completing any mission. Always 10.

**score_bonus (0-10):**
`floor(score / 10)`. A score of 73 yields 7. A perfect 100 yields 10.

**streak_bonus (0-20):**
`min(streak * 2, 20)`. Streak is the number of consecutive active days.
Caps at 20 (reached at a 10-day streak). A streak of 0 yields 0.

**daily_word_bonus (0 or 5):**
Flat +5 XP if the operator used the daily word (from the daily word ritual)
in their mission response. Detection: check if the daily word (or its
morphological variants) appears in the operator's submitted text.

**BOSS multiplier (x3):**
Applied when the mission type is BOSS. Multiplies the entire subtotal by 3.
This makes BOSS missions the highest-XP missions available.

**Critical Hit (x3):**
A random variable reward. Triggers when BOTH conditions are met:
1. Random roll: 15% chance (generate random 0-1, trigger if < 0.15)
2. Score gate: mission score must be >= 80

When triggered, multiply the subtotal by 3. Show the critical hit animation
(read `references/progression/engagement.md` for display details).

**BOSS + Critical Hit stacking:**
If a BOSS mission also triggers a critical hit, both multipliers apply
sequentially: `subtotal * 3 * 3 = subtotal * 9`. This is intentional — it
is the jackpot scenario.

### XP Range Examples

```
 Scenario                                    XP
 ─────────────────────────────────────────   ────
 Minimum: score 0, no streak, no bonuses     10
 Typical: score 70, 5-day streak             10 + 7 + 10 = 27
 Strong: score 85, 10-day streak, daily word 10 + 8 + 20 + 5 = 43
 Boss (strong): same as above, boss mission  43 * 3 = 129
 Jackpot: boss + crit hit on score 90        (10 + 9 + 20 + 5) * 9 = 396
```

---

## Score Display Format

After every mission, show the full scoring breakdown. The operator should
always understand exactly how their score was determined.

### Mission Score Display

For multi-axis missions (REWRITE, PROMPT_CRAFT, SCENARIO):

```
━━━ MISSION SCORE ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 precision      ████████████████████░░░░░  20/25
 conciseness    ██████████████████░░░░░░░  18/25
 impact         ████████████████████████░  24/25
 naturalness    ██████████████████████░░░  22/25
 ────────────────────────────────────────────────
 TOTAL                                     84/100

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

For FILL missions:

```
━━━ MISSION SCORE ━━━━━━━━━━━━━━━━━━━━━━━━
 Your answer: "mitigate"
 Target:      "mitigate"
 Tier:        EXACT MATCH
 Score:       100/100
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

For BOSS missions:

```
━━━ BOSS SCORE ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 Part 1 (REWRITE):   85/100
 Part 2 (FILL):      80/100
 Part 3 (SCENARIO):  90/100
 ────────────────────────────────────────────────
 COMPOSITE:          85/100

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### XP Breakdown Display

Always show immediately after the mission score:

```
━━━ XP EARNED ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 base            +10
 score (84)       +8
 streak (12d)    +20
 daily word       +5
 ─────────────────────
 subtotal         43
 ─────────────────────
 TOTAL           +43 XP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

With BOSS multiplier:

```
━━━ XP EARNED ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 base            +10
 score (85)       +8
 streak (10d)    +20
 daily word       +5
 ─────────────────────
 subtotal         43
 BOSS (x3)      x  3
 ─────────────────────
 TOTAL          +129 XP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

With Critical Hit:

```
━━━ XP EARNED ━━━━━━━━━━━━━━━━━━━━━━━━━━━━
 base            +10
 score (92)       +9
 streak (6d)     +12
 daily word       +0
 ─────────────────────
 subtotal         31
 ⚡ CRITICAL HIT  x  3
 ─────────────────────
 TOTAL           +93 XP
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Cumulative XP Display

After the XP breakdown, show cumulative progress:

```
 XP: 342 → 385/600  ████████████████░░░░░░░ 64%
 🟨 OPERATIVE → SPECIALIST in 215 XP
```

If a level-up occurs, show the level-up banner instead (read
`references/style.md` for template).
