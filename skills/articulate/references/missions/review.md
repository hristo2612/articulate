# MISSION: REVIEW

> Full operational reference. An AI agent reading ONLY this file can generate, present, evaluate, and debrief a REVIEW mission.

---

## Overview

Spaced repetition for language precision. The operator revisits a challenge they completed 2+ weeks ago and tries again. Their new response is scored against the same rubric and compared side-by-side with their original attempt. This measures real growth -- not just performance on new material, but durable improvement in production vocabulary.

**Unlocks at:** Level 2 (INITIATE, 100 XP)

**Trigger:** Every 5th mission overall (automatic), or on demand via `/articulate review`.

**Principle:** Repetition cements production habits. The operator does not just learn words -- they must prove they can deploy them consistently over time.

---

## Generation Rules

### Selecting a Review Challenge

Pull from `~/.articulate/history.json` using these selection criteria:

#### Step 1: Filter for eligible entries

```
eligible = history entries WHERE:
    1. date is 14+ days old (minimum spacing for spaced repetition)
    2. entry has not been reviewed more than 2 times already
       (prevent infinite loops on the same challenge)
```

#### Step 2: Prioritize

From eligible entries, prefer:

| Priority | Criteria | Rationale |
|---|---|---|
| 1 (highest) | Score < 80 AND 14-30 days old | Recent weak performance -- highest improvement potential |
| 2 | Score < 80 AND 30+ days old | Older weak performance -- test if time helped |
| 3 | Score 80-89 AND 14-30 days old | Good but not great -- room for polish |
| 4 | Any eligible entry | Fallback |

#### Step 3: Handle edge cases

```
if no eligible entries exist:
    Show: "No missions old enough for review yet, operator.
           Keep deploying -- reviews unlock after 14 days of history.
           Current history: {count} missions, oldest: {oldest_date}."
    Offer an alternative mission type instead.

if fewer than 3 eligible entries:
    Select from what is available. No minimum pool required.
```

### What to Present

Present the **original challenge** exactly as it was shown the first time:

- Same sentence (for REWRITE)
- Same blank and sentence (for FILL)
- Same goal and constraints (for PROMPT_CRAFT)
- Same situation/role/audience/goal/word-limit (for SCENARIO)

**CRITICAL:** Do NOT show the operator's previous response. They must produce a fresh answer from their current vocabulary. Showing the old response would create a revision task, not a recall task.

Do show:
- The original mission type and challenge text
- The date of the original attempt
- The original score (so they know the bar to beat)

Do NOT show:
- Their previous response
- The gold standard from the original debrief
- Any hints or vocabulary from the original feedback

---

## Presentation Format

```
━━━ MISSION: REVIEW 🔄 ━━━━━━━━━━━━━━━━━━━━━

REVIEWING: REWRITE mission from {date}
PREVIOUS SCORE: 62/100

Original challenge:

> "The **thing** we built is **really good** and **helps** people
>  **do stuff** faster."

Target: Replace the highlighted weak words.
Your rewrite (fresh attempt):
```

For FILL reviews:

```
━━━ MISSION: REVIEW 🔄 ━━━━━━━━━━━━━━━━━━━━━

REVIEWING: FILL PRECISION mission from {date}
PREVIOUS SCORE: 60/100

Original challenge:

> "The API's response time was [___], often exceeding 3 seconds
>  even for simple queries."

Your word (fresh attempt):
```

For SCENARIO reviews:

```
━━━ MISSION: REVIEW 🔄 ━━━━━━━━━━━━━━━━━━━━━

REVIEWING: SCENARIO mission from {date}
PREVIOUS SCORE: 71/100

Original challenge:

SITUATION: A potential customer emailed asking if your API supports
           batch processing.
ROLE: Founder / sole developer
AUDIENCE: Technical PM at a mid-size SaaS company
GOAL: Confirm, differentiate, close toward trial.
WORD LIMIT: 80 words

Your response (fresh attempt):
```

For PROMPT_CRAFT reviews:

```
━━━ MISSION: REVIEW 🔄 ━━━━━━━━━━━━━━━━━━━━━

REVIEWING: PROMPT CRAFT mission from {date}
PREVIOUS SCORE: 68/100

Original challenge:

GOAL: Get an LLM to draft a cold outreach email to a potential
      API integration partner.
CONSTRAINTS:
  - Under 100 words
  - Professional but not stiff
  - Include a specific value proposition
  - End with a clear call to action

Your prompt (fresh attempt):
```

---

## Scoring

Use the **same rubric as the original mission type:**

| Original Type | Rubric |
|---|---|
| REWRITE | 4 axes x 25 = 100 (Precision, Conciseness, Impact, Naturalness) |
| FILL_PRECISION | Tier scoring (100/80/60/30/0) |
| PROMPT_CRAFT | 5 axes x 20 = 100 (Specificity, Constraints, Structure, Clarity, Register) |
| SCENARIO | 5 axes x 20 = 100 (Word Choice, Register, Goal, Conciseness, Persuasiveness) |

Score the new response independently. Do not grade on a curve relative to the original. An 85 is an 85 regardless of whether the original was 40 or 80.

---

## Feedback Format -- Side-by-Side Comparison

This is the unique element of REVIEW debriefs. After scoring the new response, reveal the old one and compare.

```
━━━ REVIEW DEBRIEF 🔄 ━━━━━━━━━━━━━━━━━━━━━━

THEN ({N} days ago):     Score: 62/100
> "Our product is a good tool that helps companies manage their stuff better."

NOW:                     Score: 81/100
> "Our workflow engine eliminates manual task routing for mid-market ops teams."

IMPROVEMENT: +19 points

KEY GAINS:
- "workflow engine" vs "product" -- specific noun replaces vague noun
- "eliminates" vs "helps" -- decisive verb replaces weak verb
- "manual task routing" vs "manage their stuff" -- concrete problem replaces vague action
- "mid-market ops teams" vs "companies" -- defined audience replaces generic noun

STILL ROOM TO GROW:
- [Any weaknesses that persisted or new ones that appeared]

GOLD STANDARD:
> "Our workflow engine automates task routing, cutting manual
>  handoffs by 60% for mid-market operations teams."

WEAKNESS COMPARISON:
  THEN: utility_words, vague_nouns, weak_verbs
  NOW:  none -- clean sweep
  ELIMINATED: utility_words, vague_nouns, weak_verbs
```

### For FILL reviews:

```
━━━ REVIEW DEBRIEF 🔄 ━━━━━━━━━━━━━━━━━━━━━━

THEN ({N} days ago):
  YOUR WORD: "slow"     Score: 60/100 (Acceptable)

NOW:
  YOUR WORD: "sluggish"  Score: 100/100 (Exact)

IMPROVEMENT: +40 points

ANALYSIS:
- 14 days ago, you reached for the utility adjective "slow"
- Today, you produced the precision word "sluggish" from active vocabulary
- This word has moved from passive to active recall

WORD MASTERY: "sluggish" --> Mastery level updated
```

### Improvement Tracking

Calculate and display the point difference:

```
improvement = new_score - original_score
```

| Improvement | Display |
|---|---|
| +20 or more | "SIGNIFICANT IMPROVEMENT" with emphasis |
| +10 to +19 | "SOLID IMPROVEMENT" |
| +1 to +9 | "MARGINAL IMPROVEMENT -- keep pushing" |
| 0 | "HOLDING STEADY -- aim higher next review" |
| Negative | "REGRESSION -- {N} points below your previous attempt. Review the gold standard." |

### KEY GAINS Section

For every meaningful improvement between the old and new response:

1. **Name the specific change:** old word/phrase vs new word/phrase
2. **Categorize the gain:** specific noun, decisive verb, tighter structure, better register, etc.
3. **Explain why the new version is stronger:** what precision or impact was added

This section is the core learning output. It shows the operator exactly what changed in their vocabulary over time.

### STILL ROOM TO GROW Section

Only include if weaknesses remain or new ones appeared. Be specific:

- Name the word/phrase that is still weak
- Suggest a stronger alternative
- Frame constructively: "still room to grow" not "you still failed at"

### WEAKNESS COMPARISON Section

Compare weakness tags from the original evaluation to the new one:

```
WEAKNESS COMPARISON:
  THEN: utility_words, vague_nouns, weak_verbs
  NOW:  hedging
  ELIMINATED: utility_words, vague_nouns, weak_verbs
  NEW: hedging
```

This directly feeds into weakness radar trend tracking. Eliminated weaknesses count as improvement. New weaknesses are noted but contextualized (the operator may have been experimenting with a new style).

---

## Weakness Mapping

REVIEW missions track weaknesses in the new response using the same rules as the original mission type. Additionally:

### Improvement Detection

Compare the weakness profile of the original attempt to the new attempt:

- **Eliminated weakness:** A category tagged in the original that is NOT tagged in the new attempt. This is a WIN.
- **Persistent weakness:** A category tagged in BOTH attempts. This needs more training.
- **New weakness:** A category tagged in the new attempt but NOT in the original. Note but do not overweight -- it may be a one-off.

Feed this data into `~/.articulate/state.json` weakness tracking:

- For eliminated weaknesses: decrement the weakness counter
- For persistent weaknesses: increment the weakness counter (still struggling)
- For new weaknesses: increment the weakness counter

### Badge Trigger

The "Improver" badge (any weakness category drops by 30+ percentage points from its peak) can be triggered by REVIEW missions showing consistent elimination of a weakness category.

---

## State Updates

After a completed REVIEW mission:

1. Append the new attempt to `~/.articulate/history.json` with:
   - `type: "review"`
   - `originalMissionId: "{id or index of the original mission}"`
   - `originalDate: "{date of original}"`
   - `originalScore: {score}`
   - `newScore: {score}`
   - `improvement: {delta}`
   - Standard fields: date, response, weaknesses, xpEarned
2. Increment the `reviewCount` on the original history entry (to enforce the max 2 reviews per challenge)
3. Update XP, check level-up, check badges
4. Update weakness radar with the comparison data

---

## XP Calculation

REVIEW missions use the standard XP formula (no special multiplier):

```
base = 10
score_bonus = floor(new_score / 10)
streak_bonus = min(streak * 2, 20)
daily_word_bonus = 5 (if daily word used in response)
total_xp = base + score_bonus + streak_bonus + daily_word_bonus

if critical_hit (15% chance AND new_score >= 80):
    total_xp = total_xp * 3
```

**Improvement bonus:** If improvement is +20 or more, award an additional flat +5 XP:

```
if improvement >= 20:
    total_xp = total_xp + 5
```

This incentivizes reviewing weak challenges where the improvement potential is highest.

---

## Daily Word Bonus

If the operator uses the session's daily word in their review response:

```
DAILY WORD BONUS: +5 XP ("iterate" deployed in review)
```

---

## Edge Cases

- **Original mission was a BOSS:** Do not review BOSS missions. They are multi-part and would require reviewing all parts. Skip BOSS entries when selecting review candidates.
- **Operator's new response is identical to the original:** Score it the same. Note: "Your response is identical to your previous attempt. Challenge yourself to find sharper words."
- **Operator remembers the gold standard from the original debrief:** This is acceptable and even desirable -- it means the feedback stuck. Score the response on its own merits. If it closely matches the gold standard, full marks.
- **Original mission data is incomplete:** If the history entry lacks the challenge text or score, skip it and select another entry. Do not attempt to reconstruct a challenge from incomplete data.
- **Operator requests review of a specific past mission:** If they specify ("review my rewrite from two weeks ago"), search history.json for a matching entry. If found and eligible (14+ days), use it. If not found, explain and offer the next eligible review.
- **Operator has only FILL missions in history:** Fine. FILL reviews work well and are a valid review type. Do not force variety.
