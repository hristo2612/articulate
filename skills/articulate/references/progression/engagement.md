# Progression — Engagement Systems

> Reference for variable rewards, seasonal operations, self-competition
> mechanics, and user-generated challenges.
>
> Critical hits and daily word ritual are documented in scoring.md and
> SKILL.md respectively — not duplicated here.

---

## Variable Reward Mechanics

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

**Display example:**

```
 LOOT DROP — Precision Gem Acquired

 WORD:      ameliorate
 ORIGIN:    Latin "melior" (better) → to make better
 MEANING:   To improve a bad or unpleasant situation
 EXAMPLE:   "The new policy ameliorated working conditions
             across the factory floor."
 REGISTER:  Formal writing, policy, academic. Avoid in
             casual speech — sounds performative.
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

**Constraint examples** (select one randomly):
- "Rewrite using only Anglo-Saxon origin words"
- "Rewrite removing all adjectives — let nouns and verbs do the work"
- "Explain this technical concept using only 1-syllable words"

Generate additional constraints dynamically to match operator level and
mission type.

**Scoring:** Same rubric as the base mission type, but with a +10 bonus to
the final score (capped at 100) for successfully meeting the constraint.
Partial adherence gets partial bonus (0, +5, or +10).

**Generation rules:**
- Always announce the constraint before the mission starts
- The constraint must be achievable — never impossible
- Match constraint difficulty to operator level (L1-2 get simpler constraints)
- Store `mystery: true` and the constraint text in `history.json`

---

## Seasonal Operations

Monthly themed challenges that provide focused training and community rhythm.

### Structure

Each operation runs for 30 calendar days and includes:
- **name** — Operation codename (e.g., "Operation Cold Open")
- **focus** — The language skill being targeted
- **duration** — 30 days from start date
- **missionModifiers** — How missions are adjusted during the operation
- **completionReq** — Number of themed missions required (typically 15-20)
- **completionBadge** — Unique badge for completing the operation

### Example Operations

**Operation Cold Open**
- Focus: First sentences, hooks, openers
- Modifier: All REWRITE missions feature weak opening sentences.
  SCENARIO missions emphasize first impressions (cold emails, intros).
- Completion: 15 themed missions / Badge: Cold Opener

**Operation Precision Strike**
- Focus: Eliminating utility words
- Modifier: Missions prioritize challenges heavy with utility words.
  Scoring weights precision axis at 1.5x for REWRITE missions.
- Completion: 20 themed missions / Badge: Precision Striker

Generate additional operations dynamically based on month or rotation.

### Implementation

**State tracking:** Store in `state.json → currentSeason`:

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

---

## Self-Competition Mechanics

Systems that let the operator compete against their own past performance.

**Ghost Races:** After each mission, compare the score to the operator's
average for the same mission type from 30 days ago (28-32 day window from
`history.json`). Display the delta if comparable data exists; skip silently
if not.

**Personal Records:** Track best score per mission type in
`state.json → personalRecords`. After every mission, if the score exceeds
the stored record, update it and announce the new record.

### Teach Mode (Level 6+)

Available at ARCHITECT rank and above. The operator critiques AI-generated
bad rewrites instead of writing their own.

**Flow:**
1. Present an original sentence.
2. Present a deliberately flawed "AI rewrite" with subtle problems
   (wrong register, thesaurus abuse, lost nuance, added hedging, etc.).
3. The operator identifies the problems and writes a better version.
4. Score based on: problem identification accuracy + quality of their rewrite.

**Scoring:** Use REWRITE rubric for the operator's version. Add +5 bonus
(capped at 100) for each correctly identified flaw (max 3 flaws, so max +15,
capped at 100 total).

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

### Why This Matters

User-generated challenges never get stale because the input is the operator's
real work. This is where training meets application — the highest-value loop.

**Storage:** Log in `history.json` with `type: "USER_CHALLENGE"` and
`sourceType` indicating the detected rubric used.

---

## Prestige Mechanics

See `references/progression/levels.md` for full prestige system details.
The prestige system is available at MASTERMIND rank (Level 7) and allows
the operator to reset rank to RECRUIT while preserving badges and history.
Each prestige run adds a star marker to the rank display.
