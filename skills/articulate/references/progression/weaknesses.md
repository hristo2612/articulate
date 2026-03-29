# Progression — Weakness Tracking & Radar

> Self-contained reference for detecting weaknesses, calculating percentages,
> rendering the radar visualization, tracking trends, and triggering the
> Improver badge.

---

## Six Weakness Categories

Every piece of writing can exhibit weaknesses in these six categories.
Each category includes canonical examples, but detection is not limited to
these exact words — evaluate semantically.

| Category | Examples |
|----------|----------|
| utility_words | "good", "nice", "bad", "great", "big", "small", "important", "interesting", "amazing", "awesome", "excellent", "terrible", "wonderful", "significant" |
| hedging | "I think", "maybe", "sort of", "kind of", "I guess", "or whatever", "perhaps", "it seems", "arguably", "to be honest", "in my opinion" (when softening, not qualifying), "I feel like" |
| flat_structure | Monotone sentences — no rhythm, contrast, or emphasis. All sentences same length/pattern. No subordination, parallelism, or variation. |
| vague_nouns | "thing", "stuff", "something", "everything", "aspect", "area", "situation", "matter", "issue", "factor", "element", "part" (when a precise noun exists) |
| weak_verbs | "do", "make", "get", "have", "be", "go", "put", "take", "give", "use" — ONLY when a more precise verb exists in context. "The door is red" is fine. "The report is good" is weak. |
| filler_words | "basically", "literally", "actually", "like", "just", "really", "very", "quite", "pretty" (as intensifier), "absolutely", "totally", "honestly", "definitely", "certainly", "simply", "clearly" |

### Category Notes

- **utility_words:** Flag only when a more precise word would improve the writing. "Good morning" is idiomatic and fine; "a big problem" is weak.
- **hedging:** Distinguish strategic hedging (appropriate uncertainty) from habitual hedging (avoiding commitment). "Perhaps the data suggests" is weak; "The preliminary data suggests" is precise.
- **flat_structure:** Look for: all sentences 8-15 words with no variation, no subordinate clauses, no em-dashes/colons/semicolons for rhythm, no short punchy sentences mixed with longer ones.
- **vague_nouns:** "Thing" is the canary — if it appears where a specific noun exists, other vague nouns are likely present too.
- **weak_verbs:** Key qualifier: "when a precise alternative exists." "Get the package" is weak ("retrieve"); "Get started" is idiomatic.
- **filler_words:** "Just" is the most common offender. "Very" is almost always deletable — "very important" becomes "critical."

---

## Detection Rules

After every mission evaluation, analyze BOTH the original challenge text and
the operator's response to identify weaknesses.

### What to Count

**Only count weaknesses the operator KEPT or INTRODUCED — never count
weaknesses they successfully fixed.**

For each weakness category:
1. **SCAN** the original challenge text. Record which categories were PRESENTED.
2. **SCAN** the operator's response. Record which categories APPEAR.
3. **CLASSIFY:**
   - PRESENTED + FIXED = operator eliminated it → NOT counted
   - PRESENTED + KEPT = operator failed to fix it → COUNTED
   - NOT PRESENTED + INTRODUCED = operator added it → COUNTED
   - NOT PRESENTED + ABSENT = clean on this axis → NOT counted
4. For **FILL** missions: scan the operator's word choice only (no original to compare).
5. For **PROMPT_CRAFT**: scan the operator's prompt (the challenge is a scenario description, not text to rewrite).

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
**WEAKNESS RADAR**

 utility_words  ████████░░░░░░░░  52%  ▇▅▃▂ ↓ improving
 hedging        ██████████████░░  87%  ▂▃▅▇ ↑ worsening
 flat_structure ██████░░░░░░░░░░  38%  ▅▅▃▂ ↓ improving
 vague_nouns    ████████████░░░░  75%  ▇▇▅▃ ↓ improving
 weak_verbs     ██████████░░░░░░  63%  ▃▃▅▅ → stable
 filler_words   ████░░░░░░░░░░░░  25%  ▅▃▂▁ ↓ improving
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
 ⚠ Radar calibrating — complete 5+ missions for full tracking.

 utility_words  ░░░░░░░░░░░░░░░░  ---
 hedging        ░░░░░░░░░░░░░░░░  ---
 flat_structure ░░░░░░░░░░░░░░░░  ---
 vague_nouns    ░░░░░░░░░░░░░░░░  ---
 weak_verbs     ░░░░░░░░░░░░░░░░  ---
 filler_words   ░░░░░░░░░░░░░░░░  ---
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

The **Improver** badge is awarded when the operator demonstrates
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
 utility_words: peak=72, current=35 → drop=37 → TRIGGERS
 hedging:       peak=82, current=82 → drop=0  → no trigger
 filler_words:  peak=60, current=20 → drop=40 → TRIGGERS (if not already earned)
```

---

## Integration with Mission Feedback

After every mission, the weakness detection feeds into the debrief. Show
which weaknesses were present and how the operator handled them.

### Post-Mission Weakness Summary

```
 ✓ FIXED     utility_words — "important" → "critical" (precise)
 ✓ FIXED     filler_words  — removed "basically" and "just"
 ✗ KEPT      hedging       — "I think we should" survived
 ✗ INTRODUCED weak_verbs   — "get" used where "retrieve" fits
```

**Rules for the debrief:**
- Show only categories relevant to this mission (presented, kept,
  introduced, or fixed).
- For FIXED items: show the specific improvement (original → replacement).
- For KEPT items: show what survived and suggest an alternative.
- For INTRODUCED items: show what was added and why it is a weakness.
- Order: FIXED first (positive reinforcement), then KEPT and INTRODUCED.
- Keep it to 2-4 items maximum — highlight the most impactful, not every
  instance.
