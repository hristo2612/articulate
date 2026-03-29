# Progression — Weakness Tracking & Radar

> Self-contained reference. An AI agent reading only this file has everything
> needed to detect weaknesses, calculate percentages, render the radar
> visualization, track trends, and trigger the Improver badge.

---

## Six Weakness Categories

Every piece of writing can exhibit weaknesses in these six categories.
Each category includes canonical examples, but detection is not limited to
these exact words — evaluate semantically.

```
━━━ WEAKNESS CATEGORIES ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 Category         Examples
 ───────────────  ────────────────────────────────────────────────────
 utility_words    "good", "nice", "bad", "great", "big", "small",
                  "important", "interesting", "amazing", "awesome",
                  "excellent", "terrible", "wonderful", "significant"

 hedging          "I think", "maybe", "sort of", "kind of", "I guess",
                  "or whatever", "perhaps", "it seems", "arguably",
                  "to be honest", "in my opinion" (when used to soften
                  rather than qualify), "I feel like"

 flat_structure   Monotone sentences — no rhythm, no contrast, no
                  emphasis. All sentences same length and pattern.
                  No subordination, no parallelism, no variation.
                  Subject-verb-object on repeat.

 vague_nouns      "thing", "stuff", "something", "everything",
                  "aspect", "area", "situation", "matter", "issue",
                  "factor", "element", "part" (when a precise noun
                  exists)

 weak_verbs       "do", "make", "get", "have", "be", "go", "put",
                  "take", "give", "use" — ONLY when a more precise
                  verb exists in context. "The door is red" is fine.
                  "The report is good" is weak ("is" + utility word).

 filler_words     "basically", "literally", "actually", "like", "just",
                  "really", "very", "quite", "pretty" (as intensifier),
                  "absolutely", "totally", "honestly", "definitely",
                  "certainly", "simply", "clearly"

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Category Notes

**utility_words:** These are not always wrong. "Good morning" is idiomatic.
Flag them only when a more precise word would improve the writing. Context
matters — "big" in "big picture" is fixed; "big" in "a big problem" is weak.

**hedging:** Distinguish strategic hedging (appropriate in uncertain contexts)
from habitual hedging (used to avoid commitment). "Perhaps the data suggests"
is weak. "The preliminary data suggests" is precise.

**flat_structure:** This is the hardest to detect. Look for:
- All sentences between 8-15 words with no variation
- No sentences with subordinate clauses
- No use of em-dashes, colons, or semicolons for rhythm
- No short punchy sentences mixed with longer ones
- No parallelism or rhetorical structure

**vague_nouns:** "Thing" is the canary. If the operator writes "thing" where
a specific noun exists, they likely have other vague nouns too.

**weak_verbs:** The key qualifier is "when a precise alternative exists."
Not every use of "get" is weak. "Get the package" could be "retrieve the
package" — that is weak. "Get started" is idiomatic — not weak.

**filler_words:** "Just" is the most common offender. "I just wanted to
check" → "I wanted to check" → "Checking in on..." Each removal tightens
the prose. "Very" is almost always deletable — "very important" → "critical."

---

## Detection Rules

After every mission evaluation, analyze BOTH the original challenge text and
the operator's response to identify weaknesses.

### What to Count

**Only count weaknesses the operator KEPT or INTRODUCED — never count
weaknesses they successfully fixed.**

The logic works like this:

```
━━━ DETECTION LOGIC ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 For each weakness category:

 1. SCAN the original challenge text.
    → Record which categories were PRESENTED (had examples in original).

 2. SCAN the operator's response.
    → Record which categories APPEAR in their response.

 3. CLASSIFY:
    a. PRESENTED + FIXED    = operator eliminated it     → NOT counted
    b. PRESENTED + KEPT     = operator failed to fix it  → COUNTED
    c. NOT PRESENTED + INTRODUCED = operator added it    → COUNTED
    d. NOT PRESENTED + ABSENT     = clean on this axis   → NOT counted

 4. For FILL missions: scan the operator's word choice only.
    No "original" text to compare against — just evaluate the answer.

 5. For PROMPT_CRAFT: scan the operator's prompt.
    The "challenge" is the scenario description, not text to rewrite.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Per-Mission Recording

After detection, store the results in the `history.json` entry for this
mission:

```json
{
  "missionId": "R-15",
  "type": "REWRITE",
  "score": 78,
  "weaknesses": {
    "presented": ["utility_words", "hedging", "filler_words"],
    "kept": ["hedging"],
    "introduced": ["weak_verbs"],
    "fixed": ["utility_words", "filler_words"]
  }
}
```

The `kept` and `introduced` arrays are what feed the radar calculations.

---

## Percentage Calculation

The radar shows how often the operator retains or introduces each weakness
type, measured over the last 20 missions.

### Formula

For each category:

```
percentage = (times_kept_or_introduced / times_presented_or_applicable) x 100
```

**Detailed calculation:**

```
window = last 20 missions from history.json

For each category C:
  presented_count = number of missions where C was in "presented" OR
                    C was in "introduced" (it was applicable either way)
  failure_count   = number of missions where C was in "kept" OR
                    C was in "introduced"

  if presented_count == 0:
    percentage = 0  (no data — category not encountered)
  else:
    percentage = floor((failure_count / presented_count) x 100)
```

**Edge cases:**
- If fewer than 20 missions exist, use all available missions.
- If a category has never been encountered, show `---%` instead of `0%`.
- New operators (< 5 missions) see a simplified radar with a note:
  `"Radar calibrating — complete 5+ missions for full tracking."`

---

## Radar Visualization

The primary visual output of the weakness tracking system.

### Full Radar Display

```
━━━ WEAKNESS RADAR ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 utility_words  ████████░░░░░░░░  52%  ▇▅▃▂ ↓ improving
 hedging        ██████████████░░  87%  ▂▃▅▇ ↑ worsening
 flat_structure ██████░░░░░░░░░░  38%  ▅▅▃▂ ↓ improving
 vague_nouns    ████████████░░░░  75%  ▇▇▅▃ ↓ improving
 weak_verbs     ██████████░░░░░░  63%  ▃▃▅▅ → stable
 filler_words   ████░░░░░░░░░░░░  25%  ▅▃▂▁ ↓ improving

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Rendering Rules

**Progress bar:** 16 characters wide. Each `█` represents 6.25%. Use `█`
for filled and `░` for empty.

```
 characters_filled = round(percentage / 6.25)
 characters_empty  = 16 - characters_filled
 bar = "█" * characters_filled + "░" * characters_empty
```

**Percentage:** Right-aligned, 3 characters wide. Append `%`.

**Sparkline:** 4 characters using block elements from the set:
`▁ ▂ ▃ ▅ ▇` (5 levels). Each character represents one measurement point
(see Trend Tracking below). Map the percentage at each point to the nearest
block element:

```
 0-20%  → ▁
 21-40% → ▂
 41-60% → ▃
 61-80% → ▅
 81-100% → ▇
```

**Trend indicator:** One of three symbols:
- `↓ improving` — percentage is trending down (lower = better)
- `↑ worsening` — percentage is trending up (higher = worse)
- `→ stable` — percentage is flat (< 5 point change across last 4 points)

**Category label:** Left-aligned, padded to 14 characters.

### Compact Radar (for dashboard)

When space is limited, show a one-line summary:

```
 Radar: ▼util ▲hedge ▼flat ▼vague →verb ▼fill
```

### No-Data State

For new operators or categories without data:

```
━━━ WEAKNESS RADAR ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 ⚠ Radar calibrating — complete 5+ missions for full tracking.

 utility_words  ░░░░░░░░░░░░░░░░  ---
 hedging        ░░░░░░░░░░░░░░░░  ---
 flat_structure ░░░░░░░░░░░░░░░░  ---
 vague_nouns    ░░░░░░░░░░░░░░░░  ---
 weak_verbs     ░░░░░░░░░░░░░░░░  ---
 filler_words   ░░░░░░░░░░░░░░░░  ---

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Trend Tracking

Track how each weakness category changes over time.

### Measurement Points

Store the last 4 measurement points per category in `state.json →
weaknessHistory`. Each point is the percentage calculated at that time.

```json
{
  "weaknessHistory": {
    "utility_words": {
      "points": [72, 65, 48, 35],
      "peak": 72,
      "current": 35,
      "lastUpdated": "2026-03-29"
    },
    "hedging": {
      "points": [30, 45, 60, 82],
      "peak": 82,
      "current": 82,
      "lastUpdated": "2026-03-29"
    },
    "flat_structure": {
      "points": [55, 50, 42, 38],
      "peak": 55,
      "current": 38,
      "lastUpdated": "2026-03-29"
    },
    "vague_nouns": {
      "points": [90, 85, 70, 60],
      "peak": 90,
      "current": 60,
      "lastUpdated": "2026-03-29"
    },
    "weak_verbs": {
      "points": [55, 58, 60, 63],
      "peak": 63,
      "current": 63,
      "lastUpdated": "2026-03-29"
    },
    "filler_words": {
      "points": [60, 45, 30, 20],
      "peak": 60,
      "current": 20,
      "lastUpdated": "2026-03-29"
    }
  }
}
```

### When to Record a New Point

Record a new measurement point every 5 missions. This smooths out
single-mission variance while keeping the data responsive.

**Logic:**
1. After every mission, count total missions since last measurement
   (compare `history.json` length to length at last measurement).
2. If 5 new missions have been completed since the last point:
   - Calculate the current percentage for each category (using last 20
     missions window).
   - Shift the `points` array: drop the oldest, append the new value.
   - Update `peak` if the new value exceeds the stored peak.
   - Update `current` to the new value.
   - Update `lastUpdated`.

### Sparkline Display

The 4 points map directly to the 4-character sparkline:

```
 points: [72, 65, 48, 35]  →  sparkline: ▇▅▃▂  (left=oldest, right=newest)
```

Block element mapping:
```
 0-20%   → ▁
 21-40%  → ▂
 41-60%  → ▃
 61-80%  → ▅
 81-100% → ▇
```

### Trend Classification

Compare the 4 points to determine trend direction:

```
 improving  = points[3] < points[0] by 5+ percentage points
              Display: ↓ improving

 worsening  = points[3] > points[0] by 5+ percentage points
              Display: ↑ worsening

 stable     = |points[3] - points[0]| < 5 percentage points
              Display: → stable
```

If fewer than 4 points exist, show `→ calibrating` instead of a trend.

---

## Improvement Badge Trigger

The **📈 Improver** badge is awarded when the operator demonstrates
measurable improvement in any weakness category.

### Trigger Condition

Any single weakness category drops **30 or more percentage points** from
its recorded peak value.

```
 trigger = (peak - current) >= 30
```

### Check Logic

After every weakness measurement update (every 5 missions):

```
 for each category in weaknessHistory:
   if category.peak - category.current >= 30:
     if "📈" not in state.json → badges:
       award badge "📈 Improver"
       break  (badge only needs to trigger once)
```

### Examples

```
 utility_words: peak=72, current=35 → drop=37 → TRIGGERS ✓
 hedging:       peak=82, current=82 → drop=0  → no trigger
 filler_words:  peak=60, current=20 → drop=40 → TRIGGERS ✓ (if not already earned)
```

### Display on Trigger

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  📈 BADGE EARNED — IMPROVER
  Your {category} weakness dropped from
  {peak}% to {current}% — that's real
  progress, operator.
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Integration with Mission Feedback

After every mission, the weakness detection feeds into the debrief. Show
which weaknesses were present and how the operator handled them.

### Post-Mission Weakness Summary

```
━━━ WEAKNESS DEBRIEF ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

 ✓ FIXED     utility_words — "important" → "critical" (precise)
 ✓ FIXED     filler_words  — removed "basically" and "just"
 ✗ KEPT      hedging       — "I think we should" survived
 ✗ INTRODUCED weak_verbs   — "get" used where "retrieve" fits

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Rules for the debrief:**
- Show only categories that were relevant to this mission (presented, kept,
  introduced, or fixed).
- For FIXED items: show the specific improvement (original → replacement).
- For KEPT items: show what survived and suggest an alternative.
- For INTRODUCED items: show what was added and why it is a weakness.
- Order: FIXED first (positive reinforcement), then KEPT and INTRODUCED.
- Keep it to 2-4 items maximum — highlight the most impactful, not every
  instance.
