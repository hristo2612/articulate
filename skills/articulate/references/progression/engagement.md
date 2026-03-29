# Progression — Engagement Systems

> Self-contained reference. An AI agent reading only this file has everything
> needed to run variable rewards, seasonal operations, self-competition
> mechanics, user-generated challenges, and the daily word ritual.

---

## Variable Reward Mechanics

Three systems inject unpredictability into the XP loop to maintain
engagement. Each operates independently.

---

### Critical Hits

A random XP multiplier that rewards high performance.

**Trigger conditions (both must be true):**
1. Random chance: 15% per mission (roll random float 0-1; trigger if < 0.15)
2. Score gate: mission score must be >= 80

**Effect:** Multiply total XP for this mission by 3.

**Display:**

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  ⚡⚡⚡ CRITICAL HIT ⚡⚡⚡
  3x XP multiplier activated
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Show this banner between the mission score display and the XP breakdown.
The XP breakdown should reflect the multiplied total.

**Stacking with BOSS:** If a BOSS mission triggers a critical hit, both
multipliers apply: `subtotal * 3 (boss) * 3 (crit) = subtotal * 9`.

---

### Loot Drops

Random precision vocabulary rewards after mission completion.

**Trigger:** 5-10% chance after any completed mission (roll random float;
trigger if < 0.075 for a 7.5% midpoint). Independent of score.

**Payload:** A "precision gem" — a single word with:
- The word itself
- Brief etymology (1 line)
- Definition (1 line)
- Example sentence showing ideal usage
- Register note (where this word belongs)

**Display:**

```
━━━ LOOT DROP ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  💎 Precision Gem Acquired

  WORD:      ameliorate
  ORIGIN:    Latin "melior" (better) → to make better
  MEANING:   To improve a bad or unpleasant situation
  EXAMPLE:   "The new policy ameliorated working conditions
              across the factory floor."
  REGISTER:  Formal writing, policy, academic. Avoid in
              casual speech — sounds performative.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Post-drop:** Add the gem word to `lexicon.json` with mastery level `"seen"`.
Show after the XP breakdown.

**Word selection:** Generate a word that is:
- Not already in `lexicon.json` (prefer novelty)
- Relevant to the operator's focus areas (from `user.json`)
- At an appropriate difficulty for the operator's level
- Genuinely useful — not obscure for obscurity's sake

---

### Mystery Missions

Occasional creative twist challenges that break the routine.

**Trigger:** At mission selection time, 10% chance to replace a standard
mission with a mystery variant. The underlying type (REWRITE, SCENARIO, etc.)
remains the same — the constraint changes.

**Examples:**

```
━━━ MYSTERY MISSION ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  🎲 Creative constraint active
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Constraint examples (select one randomly):
- "Rewrite using only Anglo-Saxon origin words"
- "Write this email as a 19th-century diplomat"
- "Explain this technical concept using only 1-syllable words"
- "Rewrite removing all adjectives — let nouns and verbs do the work"
- "Rewrite this so every sentence is under 8 words"
- "Write the response without using the letter 'e'"
- "Express the same meaning using exactly half the original word count"
- "Rewrite using only active voice — no passive constructions allowed"

**Scoring:** Same rubric as the base mission type, but with a +10 bonus to
the final score (capped at 100) for successfully meeting the constraint.
The constraint itself is evaluated qualitatively — partial adherence gets
partial bonus (0, +5, or +10).

**Generation rules:**
- Always announce the constraint before the mission starts
- The constraint must be achievable — never impossible
- Match constraint difficulty to operator level (L1-2 get simpler constraints)
- Store `mystery: true` and the constraint text in the `history.json` entry

---

## Seasonal Operations

Monthly themed challenges that provide focused training and community rhythm.

### Structure

Each operation runs for 30 calendar days and includes:

```
 Field              Description
 ────────────────   ──────────────────────────────────────────────
 name               Operation codename (e.g., "Operation Cold Open")
 focus              The language skill being targeted
 duration           30 days from start date
 description        1-2 sentence briefing
 missionModifiers   How missions are adjusted during the operation
 completionBadge    Unique badge for completing the operation
 completionReq      Number of themed missions required (typically 15-20)
```

### Example Operations

**Operation Cold Open**
- Focus: First sentences, hooks, openers
- Modifier: All REWRITE missions feature weak opening sentences.
  SCENARIO missions emphasize first impressions (cold emails, intros).
- Completion: 15 themed missions
- Badge: 🎬 Cold Opener

**Operation Precision Strike**
- Focus: Eliminating utility words
- Modifier: Missions prioritize challenges heavy with utility words.
  Scoring weights precision axis at 1.5x for REWRITE missions.
- Completion: 20 themed missions
- Badge: 🎯 Precision Striker

**Operation Polyglot**
- Focus: Bilingual challenges
- Modifier: Missions alternate between the operator's configured languages.
  FILL missions present words with cross-language etymological connections.
- Completion: 15 themed missions (min 5 per language)
- Badge: 🌐 Polyglot Operative

**Operation Architect**
- Focus: Sentence structure and rhythm
- Modifier: REWRITE missions target monotone structure. Scoring weights
  impact axis at 1.5x. Missions include sentence-combining challenges.
- Completion: 15 themed missions
- Badge: 🏗️ Architect

**Operation Brevity**
- Focus: Saying more with fewer words
- Modifier: REWRITE missions have strict word-count ceilings (50% of
  original). SCENARIO missions have tight character limits (tweet-length).
- Completion: 20 themed missions
- Badge: ✂️ Brevity Expert

### Implementation

**State tracking:** Store in `state.json`:

```json
{
  "currentSeason": {
    "name": "Operation Cold Open",
    "startDate": "2026-03-01",
    "endDate": "2026-03-31",
    "completionReq": 15,
    "themedMissionsCompleted": 8,
    "completed": false,
    "badge": "🎬"
  }
}
```

**Season detection logic (session start):**
1. Check `state.json → currentSeason`.
2. If no season or season has expired (today > endDate):
   - Select the next operation based on month or rotation.
   - Initialize the season object.
   - Announce the new operation at session start.
3. If season is active and not completed:
   - Show progress: `"Operation Cold Open: 8/15 missions"`.
   - Apply mission modifiers when generating challenges.
4. If season is active and completed:
   - Show completion status. No more modifiers needed.

**Season announcement:**

```
━━━ OPERATION BRIEFING ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  📋 Operation Cold Open
  Focus: First sentences, hooks, openers
  Duration: 30 days (ends 2026-03-31)
  Objective: Complete 15 themed missions

  "The opening line is your only chance to earn the second."

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

**Season completion:**

```
━━━ OPERATION COMPLETE ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  🎬 Operation Cold Open — ACCOMPLISHED
  Badge earned: 🎬 Cold Opener
  Themed missions: 15/15

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

---

## Self-Competition Mechanics

Systems that let the operator compete against their own past performance.

### Ghost Races

Compare current performance to the operator's scores from 30 days ago.

**Data source:** `history.json` entries from 30 days ago (match by date range,
same mission type).

**Display (after mission score):**

```
━━━ GHOST RACE ━━━━━━━━━━━━━━━━━━━━━━━━━━━
 Today:     84/100
 30d ago:   67/100  (+17 improvement)
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

If no comparable mission exists from 30 days ago, skip the ghost race display.

**Calculation:** Compare same mission type. Use the average score for that
type from the 30-day-ago window (28-32 days ago, to allow for daily variance).

### Personal Records

Track the operator's best scores per mission type.

**Storage:** `state.json → personalRecords`:

```json
{
  "personalRecords": {
    "REWRITE": { "score": 94, "date": "2026-03-15", "missionId": "R-12" },
    "FILL": { "score": 100, "date": "2026-03-10", "missionId": "F-07" },
    "PROMPT_CRAFT": { "score": 88, "date": "2026-03-20", "missionId": "PC-03" },
    "SCENARIO": { "score": 91, "date": "2026-03-18", "missionId": "S-15" },
    "BOSS": { "score": 87, "date": "2026-03-22", "missionId": "B-02" }
  }
}
```

**Update logic:** After every mission, if the score exceeds the stored record
for that type, update the record and announce it:

```
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
  🏅 NEW PERSONAL RECORD — REWRITE
  Previous: 89  →  New: 94
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Teach Mode (Level 6+)

Available at ARCHITECT rank and above. The operator critiques AI-generated
bad rewrites instead of writing their own.

**Flow:**
1. Present an original sentence.
2. Present a deliberately flawed "AI rewrite" that contains subtle problems
   (wrong register, thesaurus abuse, lost nuance, added hedging, etc.).
3. The operator must identify the problems and write a better version.
4. Score based on: problem identification accuracy + quality of their rewrite.

**Scoring:** Use REWRITE rubric for the operator's version. Add +5 bonus
(capped at 100) for each correctly identified flaw in the AI version
(max 3 flaws, so max +15, capped at 100 total).

**Purpose:** Develops the operator's critical eye — recognizing bad writing
is a different skill from producing good writing.

---

## User-Generated Challenges (Level 5+)

Available at COMMANDER rank and above. The operator submits their own real
text for evaluation.

### Flow

1. Operator pastes their text (email, message, prompt, PR description, etc.).
2. Operator states the context: audience, purpose, register.
3. Articulate evaluates the text against precision criteria.
4. Score using the closest matching rubric:
   - If it resembles a rewrite task → REWRITE rubric
   - If it resembles a prompt → PROMPT_CRAFT rubric
   - If it resembles a message/email → SCENARIO rubric
5. Provide specific improvement suggestions with examples.
6. Award XP using standard formula.

### Display

```
━━━ USER CHALLENGE ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  📝 Evaluating your text...
  Type detected: Business email (→ SCENARIO rubric)
  Context: Client communication, formal register

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

Then show standard scoring breakdown followed by targeted suggestions:

```
━━━ SUGGESTIONS ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  1. "I think we should" → "We recommend" (removes hedge, adds authority)
  2. "really important" → "critical" (precision over emphasis)
  3. "get back to you" → "respond by Friday" (specificity over vagueness)

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Why This Matters

User-generated challenges never get stale because the input is the operator's
real work. This is where training meets application — the highest-value loop.

**Storage:** Log in `history.json` with `type: "USER_CHALLENGE"` and
`sourceType` indicating the detected rubric used.

---

## Daily Word Ritual

One precision word presented at every session start. Bridges passive
vocabulary knowledge into active usage.

### Format

```
━━━ DAILY WORD ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  WORD:      ATTRITION
  ORIGIN:    Latin "atterere" — to rub against, wear down
  MEANING:   Gradual reduction in strength or numbers through
             sustained pressure or friction
  EXAMPLE:   "The startup lost three engineers to attrition
              before the founders addressed the culture problem."
  REGISTER:  Business, military, academic. Natural in strategy
             discussions. Avoid in casual conversation.

  💡 Use this word in today's mission for +5 XP

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
```

### Selection Logic

Choose the daily word using this priority order:

1. **Prefer words not yet in `lexicon.json`** — maximize vocabulary growth.
2. **If all curated words are known:** prefer words at `"seen"` mastery level
   in `lexicon.json` — reinforce words the operator has encountered but not
   yet mastered.
3. **Never repeat a word within the same 30-day window** — check
   `history.json` for recent daily words.
4. **Match operator level:** L1-2 get high-frequency precision words
   (e.g., "mitigate", "concise"). L5-7 get rarer, domain-specific words
   (e.g., "ameliorate", "perspicacious").
5. **Match focus areas:** If `user.json → focusAreas` includes
   `technical_writing`, prefer technical vocabulary. If `business_communication`,
   prefer business vocabulary.

### Word Source

Two sources, blended:
1. **Curated list:** Maintained within the skill templates. High-quality,
   vetted words with complete etymology and register notes.
2. **Dynamic generation:** When the curated list is exhausted or when a
   context-aware word would be more relevant, generate one that matches the
   operator's project domain and level.

### XP Bonus Detection

After the operator submits a mission response, check if the daily word
(or morphological variants) appears in their text:

- "attrition" matches "attrition", "attrition's"
- "ameliorate" matches "ameliorate", "ameliorated", "ameliorating", "ameliorates"
- Case-insensitive matching

If found: award +5 XP (reflected in the daily_word_bonus line of the XP
breakdown).

### State Tracking

Store the daily word in `state.json`:

```json
{
  "dailyWord": {
    "word": "attrition",
    "date": "2026-03-29",
    "used": false
  }
}
```

Set `used: true` after the operator uses it in a mission. The word persists
for the entire calendar day — multiple sessions on the same day see the
same word.

### Lexicon Integration

When the daily word is presented:
- If not in `lexicon.json`: add it with mastery `"seen"`.
- If already in `lexicon.json` at `"seen"`: keep it (reinforcement).
- If the operator uses it correctly in a mission: promote to `"used"`.
- Mastery levels: `"seen"` → `"used"` → `"mastered"` (after 3+ correct uses).
