# MISSION: BOSS

> Full operational reference. An AI agent reading ONLY this file can generate, present, evaluate, and debrief a BOSS mission.

---

## Overview

Multi-part challenge combining multiple language skills in a connected sequence. Each part builds on the previous. The operator faces the hardest test of precision, conciseness, and register-awareness -- and earns 3x XP for it.

**Unlocks at:** Level 4 (SPECIALIST, 600 XP)

**Frequency:** Once per 7 calendar days. Enforce via `lastBossDate` in `~/.articulate/state.json`.

**XP Multiplier:** 3x applied to the total XP earned from this mission.

**Principle:** Real professional communication is not isolated sentences. It is connected, multi-step, audience-shifting work. Boss missions train that connected precision.

---

## Frequency Enforcement

Before generating a BOSS mission, check `lastBossDate` in `~/.articulate/state.json`:

```
if lastBossDate exists AND (today - lastBossDate) < 7 days:
    DENY the mission.
    Show: "Boss missions deploy once per week, operator.
           Next available: {lastBossDate + 7 days}.
           Current cooldown: {days remaining} days."
    Offer alternative mission types instead.

if lastBossDate is null OR (today - lastBossDate) >= 7 days:
    ALLOW the mission.
    After completion, update lastBossDate to today's date.
```

---

## Generation Rules

### Structure

Every BOSS mission has **2-3 parts**, presented sequentially. Each part builds on the previous:

| Parts | Structure |
|---|---|
| 2-part | Part 1: Foundation piece. Part 2: Transform or extend it for a different context. |
| 3-part | Part 1: Core statement. Part 2: Extend to a specific audience. Part 3: Adapt for a contrasting audience or constraint. |

### Part Design Principles

1. **Part 1** always establishes the core idea -- a value proposition, a key message, a technical explanation, or a stance
2. **Part 2** forces the operator to deploy that idea in a specific professional context -- an email, a Slack message, a PR description, a prompt
3. **Part 3** (if present) introduces a twist -- different audience, tighter constraint, opposing perspective, or format change

### Boss Challenge Types

| Type | Parts Description |
|---|---|
| **The Elevator** | P1: Write a 10-word value proposition. P2: Opening paragraph of a cold email using that proposition. P3: Rewrite the email for a non-technical audience. |
| **The Pivot** | P1: Write a product description for developers. P2: Rewrite for investors (same product, different register). P3: Rewrite as a 280-character tweet. |
| **The Incident** | P1: Write a 1-sentence root cause summary. P2: Full incident postmortem email to affected customers (60 words). P3: Internal Slack message to the engineering team about prevention. |
| **The Pitch** | P1: Write a problem statement in 15 words. P2: Solution description in 25 words. P3: Cold email integrating both, targeted at a specific buyer persona. |
| **The Diplomat** | P1: Write a direct rejection (decline a feature request). P2: Rewrite the rejection for a VIP customer. P3: Rewrite as a public roadmap update that addresses the request without promising it. |
| **The Teacher** | P1: Explain a technical concept in 1 sentence for a junior developer. P2: Explain the same concept for a non-technical PM. P3: Write an LLM prompt that would generate a good explanation for either audience. |
| **The Closer** | P1: Write a follow-up email after a demo (prospect seemed lukewarm). P2: Rewrite after learning they are evaluating a competitor. P3: Final follow-up if they go silent for a week. |

### Context-Aware Generation

If `contextAware: true`, anchor the BOSS mission in the operator's actual project:

```
BOSS MISSION: THE ELEVATOR

PART 1: Write a 10-word value proposition for {project}.
PART 2: Use that value proposition in the opening paragraph of a cold email
         to a {relevant audience from project context}.
PART 3: Rewrite the email for a non-technical executive at a Fortune 500.
```

### Difficulty Scaling

BOSS missions are always high-difficulty, but scale within L4-L7:

**L4 (SPECIALIST):** 2-part bosses. Clear constraints. Single domain.

**L5 (COMMANDER):** 3-part bosses. Tighter word limits. Audience-switching.

**L6 (ARCHITECT):** 3-part bosses with format constraints (tweet, subject line, Slack message). Extreme conciseness.

**L7 (MASTERMIND):** 3-part bosses with competing goals (be honest AND persuasive, be brief AND comprehensive). Meta-challenges (write a prompt that generates the ideal version of Part 2).

---

## Presentation Format

Present all parts at once so the operator can plan their approach, but mark them clearly as sequential.

### 2-Part Boss

```
━━━ BOSS MISSION 💀 ━━━━━━━━━━━━━━━━━━━━━━━━
              3x XP MULTIPLIER ACTIVE

THE ELEVATOR

PART 1 of 2:
Write a 10-word value proposition for your product.
Constraint: exactly 10 words, no filler, every word must earn its place.

PART 2 of 2:
Use that value proposition in the opening paragraph of a cold email
to a VP of Engineering at a Series B fintech startup.
Constraint: 60 words max. Professional, direct, end with a clear CTA.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Submit Part 1 first, then Part 2.
```

### 3-Part Boss

```
━━━ BOSS MISSION 💀 ━━━━━━━━━━━━━━━━━━━━━━━━
              3x XP MULTIPLIER ACTIVE

THE PIVOT

PART 1 of 3:
Write a one-paragraph product description aimed at backend engineers.
Constraint: 40 words max. Technical precision, no marketing fluff.

PART 2 of 3:
Rewrite that description for a seed-stage investor.
Constraint: 40 words max. Focus on market opportunity and traction.

PART 3 of 3:
Compress the core message into a 280-character tweet.
Constraint: Must be engaging enough to earn clicks. No hashtag spam.

━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

Submit each part in order.
```

---

## Scoring

### Per-Part Scoring

Each part is scored individually using the rubric appropriate to its type:

| Part Type | Rubric Used |
|---|---|
| Value proposition / core statement | REWRITE rubric (4 axes x 25 = 100) |
| Email / message / reply | SCENARIO rubric (5 axes x 20 = 100) |
| Prompt / instruction | PROMPT_CRAFT rubric (5 axes x 20 = 100) |
| Single-word or short-phrase challenge | FILL rubric (tier scoring) |

If a part does not clearly map to an existing mission type, use the REWRITE rubric (Precision, Conciseness, Impact, Naturalness) as the default.

### Total Score Calculation

```
total_score = average(part_1_score, part_2_score, [part_3_score])
```

Round to the nearest integer. This averaged score is what feeds into the XP formula.

### XP Calculation

```
base = 10
score_bonus = floor(total_score / 10)
streak_bonus = min(streak * 2, 20)
daily_word_bonus = 5 (if daily word used in any part)
subtotal = base + score_bonus + streak_bonus + daily_word_bonus

boss_total = subtotal * 3    <-- 3x BOSS MULTIPLIER

if critical_hit (15% chance AND total_score >= 80):
    boss_total = boss_total * 3    <-- stacks with boss multiplier = 9x

total_xp = boss_total
```

The 3x multiplier makes BOSS missions the highest-XP opportunity in the game. A critical hit on a boss is the rarest and most rewarding event possible (9x base XP).

---

## Feedback Format

Debrief EACH PART individually, then give an overall assessment.

```
━━━ BOSS DEBRIEF 💀 ━━━━━━━━━━━━━━━━━━━━━━━━

PART 1: Value Proposition
SCORE: 82/100
├─ Precision:   22/25  ████████████████████░░░░░
├─ Conciseness: 20/25  ████████████████████░░░░░
├─ Impact:      22/25  ████████████████████░░░░░
└─ Naturalness: 18/25  ██████████████░░░░░░░░░░░

YOUR VERSION:
> "Ship API monitoring that catches failures before your customers do."

GOLD STANDARD:
> "Detect API failures 30 seconds before your customers notice them."

ANALYSIS:
- "Ship" is strong but "Detect" is more precise for a monitoring product
- "catches" is good; "detect... before" adds temporal specificity
- "30 seconds" adds a concrete metric that "catches" lacks
- Strong overall -- tight, active, clear benefit

─────────────────────────────────────────────

PART 2: Cold Email
SCORE: 71/100
├─ Word Choice:      16/20  ████████████████░░░░
├─ Register:         18/20  ██████████████████░░
├─ Goal Achievement: 14/20  ██████████████░░░░░░
├─ Conciseness:      12/20  ████████████░░░░░░░░
└─ Persuasiveness:   11/20  ███████████░░░░░░░░░

[... part 2 details ...]

─────────────────────────────────────────────

OVERALL
━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━
TOTAL SCORE: 77/100  (avg of 82, 71)
XP EARNED: (10 + 7 + streak_bonus) * 3 = {calculated} XP
         💀 3x BOSS MULTIPLIER APPLIED

CONNECTED PRECISION:
- [How well the parts built on each other]
- [Whether the core message stayed consistent across transformations]
- [Register shifts that worked / didn't work]

WEAKNESSES DETECTED: filler_words, hedging
```

### CONNECTED PRECISION Section

Unique to BOSS debriefs. Evaluate how well the parts connect:

- Did the core idea/value proposition carry through all parts?
- Did the operator successfully shift register between audiences?
- Did constraints (word limits) get tighter gracefully, or did the message collapse?
- Did the operator make each part self-contained while maintaining the thread?

This section is 2-4 sentences, specific and actionable.

---

## Weakness Mapping

Aggregate weaknesses across all parts. If `utility_words` appeared in Part 1 and Part 3, it still counts as one `utility_words` tag -- but note in the debrief that it was a recurring pattern.

```
WEAKNESSES DETECTED: filler_words, hedging (recurring across parts 1 and 3)
```

---

## State Updates

After a completed BOSS mission:

1. Update `lastBossDate` in `~/.articulate/state.json` to today's ISO date
2. Append the full mission to `~/.articulate/history.json` with:
   - `type: "boss"`
   - `subtype: "the_elevator"` (or whichever boss type)
   - `parts: [{score, response}, ...]`
   - `totalScore: averaged_score`
   - `xpEarned: calculated_total`
3. Update XP, check level-up, check badge conditions
4. Update weakness radar with detected weaknesses

---

## Daily Word Bonus

If the operator uses the session's daily word in ANY part of the boss mission:

```
DAILY WORD BONUS: +5 XP ("pragmatic" deployed in Part 2)
```

The bonus is awarded once, even if the word appears in multiple parts.

---

## Edge Cases

- **Operator submits all parts at once:** Accept and score them. The sequential presentation is ideal but not mandatory.
- **Operator's Part 2 contradicts Part 1:** Note the inconsistency in the CONNECTED PRECISION section. Dock Goal Achievement points on the part that diverges.
- **Operator asks to skip a part:** All parts are required. Respond: "All parts are mandatory for a boss mission, operator. No shortcuts at this rank."
- **Operator attempts a BOSS mission before 7-day cooldown:** Deny with the cooldown message. Offer alternative mission types. Never override the cooldown.
- **Operator scores below 50 overall:** Still award the 3x multiplier on whatever XP they earn. The multiplier rewards the attempt at a harder challenge, not just success.
- **Critical hit on a BOSS mission:** 9x total XP (3x boss * 3x crit). Display with special emphasis: "CRITICAL HIT on a BOSS MISSION -- 9x XP MULTIPLIER."
