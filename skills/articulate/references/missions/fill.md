# MISSION: FILL PRECISION

> Full operational reference. An AI agent reading ONLY this file can generate, present, evaluate, and debrief a FILL_PRECISION mission.

---

## Overview

The operator sees a sentence with ONE word replaced by `[___]`. The missing word is precise and high-impact. The operator must PRODUCE the word from memory -- no multiple choice, no hints, no word bank. Pure recall.

**Available from:** Level 1 (RECRUIT, 0 XP)

**Principle:** Activate passive vocabulary. The operator knows these words when they read them, but can they summon them on demand?

---

## Generation Rules

### Target Word Selection

The blank must be a **precision word** -- a word that carries specific meaning, texture, or force beyond its generic equivalent. Categories:

| Word Type | Examples |
|---|---|
| Specific adjective | sluggish, granular, robust, succinct, scalable, compelling |
| Strong verb | streamline, synthesize, deprecate, enumerate, iterate, articulate |
| Exact noun | bottleneck, cadence, leverage, bandwidth, throughput, scaffold |
| Technical term | idempotent, orthogonal, ergonomic, deterministic, ephemeral |
| Register word | stakeholder, deliverable, blocker, runway, traction |

### Sentence Requirements

1. The sentence MUST provide enough **context clues** that the target word is deducible by someone with strong passive vocabulary
2. The surrounding words should narrow the semantic field -- the blank should not be guessable as 50 different words
3. Avoid obscure or rare words at low levels -- target "passive vocabulary" (operator would recognize the word but might not produce it unprompted)
4. The sentence should feel real -- something from a code review, product doc, investor email, Slack thread, or technical article

### Context-Aware Generation

If `contextAware: true` and a project context exists, generate sentences using the operator's project domain:

```
"The [___] between our API gateway and the downstream services caused
 a 200ms increase in response time."  (target: latency)
```

If context-aware is off, use generic professional/technical scenarios.

### Difficulty Scaling

**L1-L2 (RECRUIT / INITIATE):** Common precision words. Broadly useful across professional contexts.

Target words: compelling, streamline, robust, concise, iterate, leverage, articulate, succinct, granular, pragmatic

```
"Her pitch was [___] -- every investor in the room leaned forward."  (compelling)
"We need to [___] the onboarding flow to reduce drop-off."  (streamline)
```

**L3-L4 (OPERATIVE / SPECIALIST):** Register-specific words. Technical precision. Domain vocabulary.

Target words: synthesize, enumerate, pragmatic, deprecate, orthogonal, idempotent, ergonomic, bottleneck, deterministic, ephemeral

```
"The old authentication endpoint has been [___] since v3 -- stop calling it."  (deprecated)
"These two concerns are completely [___]; changing one has zero effect on the other."  (orthogonal)
```

**L5-L7 (COMMANDER+):** Nuanced precision. Words that carry connotation, register weight, or etymological depth. Used sparingly -- focus stays on genuinely useful precision.

Target words: perspicacious, parsimonious, verisimilitude, ameliorate, obfuscate, reticent, sycophantic, perfunctory

```
"His code review comments were [___] -- technically correct but clearly
 rushed, with no real engagement in the design decisions."  (perfunctory)
```

---

## Presentation Format

```
**MISSION: FILL PRECISION 🎯**

> "The API's response time was [___], often exceeding 3 seconds
>  even for simple queries."

Your word:
```

For L3+, optionally include a register hint:

```
**MISSION: FILL PRECISION 🎯**

> "The committee's feedback was [___] at best -- they acknowledged
>  the proposal but offered no substantive critique."

REGISTER: Formal written English, professional evaluation context

Your word:
```

---

## Scoring

FILL_PRECISION uses a tier-based scoring system, not a rubric. One word, one score.

| Tier | Score | Criteria |
|---|---|---|
| **Exact match** | **100** | Operator produced the target word (or its exact morphological variant: deprecate/deprecated, compelling/compellingly) |
| **Strong synonym** | **80** | Different word, same precision level, same register. Fits the sentence perfectly. Example: "lethargic" for target "sluggish" |
| **Acceptable alternative** | **60** | Correct general meaning, less precise or slightly off-register. Example: "slow" for target "sluggish" |
| **Weak but related** | **30** | In the right semantic neighborhood but vague or imprecise. Example: "bad" for target "sluggish" |
| **Wrong / vague** | **0** | Incorrect meaning, nonsensical, or a generic utility word that adds nothing. Example: "interesting" for target "sluggish" |

### Scoring Judgment Calls

- **Morphological variants** of the target word count as exact (100): "deprecated" / "deprecate" / "deprecating" are all exact matches for target "deprecated"
- **British/American spelling** variants are both exact: "optimise" = "optimize"
- **Strong synonyms** must be genuinely interchangeable in the sentence without losing precision or changing register
- **Acceptable alternatives** are words that convey the right idea but lack the specificity, texture, or register-fit of the target
- When in doubt between tiers, favor the higher tier -- reward the operator for getting close

---

## Feedback Format

The debrief for FILL_PRECISION focuses on etymology, register, and the precision gap between the operator's word and the target.

```
**DEBRIEF**

YOUR WORD: "slow" | TARGET: "sluggish" | MATCH: Acceptable (60/100)

**Why "sluggish" > "slow":**
- "slow" states the fact but carries no texture
- "sluggish" implies reluctance and heaviness -- a system laboring
- Etymology: Scandinavian "slugg" (slow-moving creature)
- Register: technical writing, performance reports, code reviews

ALSO STRONG: "abysmal" (80) -- implies unacceptable; "glacial" (80) -- vivid metaphor
```

### Debrief Structure (required elements)

1. **YOUR WORD / TARGET / MATCH** -- on one line
2. **Why [target] > [their word]:** -- precision gap explanation including: what the operator's word lacks, what the target adds, **etymology** (1 line), **register** (where the word lives)
3. **ALSO STRONG:** -- 1-2 alternative 80-scoring synonyms with brief notes

### When the Operator Nails It (100/100)

```
**DEBRIEF**

YOUR WORD: "sluggish" | TARGET: "sluggish" | MATCH: Exact (100/100)

TARGET ACQUIRED. Direct hit.

**Word intel:** Etymology: Scandinavian "slugg" (slow-moving creature). Register: technical writing, performance analysis. Connotation: heaviness, reluctance.

ALSO STRONG: "abysmal" -- harsher judgment; "glacial" -- vivid, informal technical tone
```

### When the Operator Misses Completely (0/100)

```
**DEBRIEF**

YOUR WORD: "interesting" | TARGET: "sluggish" | MATCH: Wrong (0/100)

**Miss analysis:** "interesting" is a utility word with zero information content. The sentence describes poor performance -- context clues ("exceeding 3 seconds", "even for simple queries") point to something heavy and laboring.

**Target word:** "sluggish" -- reluctance, heaviness, a system dragging its feet. Etymology: Scandinavian "slugg". Register: technical writing, performance reports.

ALSO STRONG: "abysmal" (80), "glacial" (80)
```

Be direct but not harsh. Explain the miss, teach the context-reading skill, deliver the word.

---

## Weakness Mapping

FILL_PRECISION missions detect weaknesses differently from REWRITE:

- If the operator submitted a **utility word** (good, bad, nice, great, etc.) --> tag `utility_words`
- If the operator submitted a **vague noun** (thing, stuff, something) --> tag `vague_nouns`
- If the operator submitted a **weak verb** (do, make, get, have) --> tag `weak_verbs`
- If the operator submitted a **filler word** (basically, really, very) --> tag `filler_words`
- If the operator's word was in the right area but lacked register-awareness --> tag `flat_structure` (indicates they are not thinking about audience/context)

If the operator scored 80+ (strong synonym or exact), no weaknesses are tagged.

Report in the debrief:

```
WEAKNESSES DETECTED: utility_words
```

Or if clean:

```
WEAKNESSES DETECTED: none -- precision locked
```

---

## Daily Word Bonus

If the operator's submitted word happens to be the session's daily word, award +5 bonus XP:

```
DAILY WORD BONUS: +5 XP (daily word deployed)
```

---

## Lexicon Integration

After scoring:

- If the **target word** is not in `~/.articulate/lexicon.json`, add it with mastery "seen"
- If the operator produced the **target word** (exact match), increment its `timesUsed` and update mastery tier
- If the operator produced a **strong synonym** (80), add THAT word to the lexicon as well with mastery "seen"
- The `ALSO STRONG` words in the debrief should also be added to the lexicon as "seen" if not already present

This ensures every FILL_PRECISION mission expands the operator's tracked vocabulary by 2-4 words.

---

## Edge Cases

- **Operator submits multiple words:** Take the first word only. Note in feedback: "FILL_PRECISION is a single-word mission. Taking your first word."
- **Operator submits a phrase instead of a word:** Score 0. Explain the mission requires a single precise word.
- **Operator's word is a different part of speech:** Score based on semantic proximity, but note the part-of-speech mismatch. "You submitted a noun; the sentence needs an adjective."
- **Target word has multiple valid exact matches:** If the generation allows for two equally precise, equally fitting words, accept both as exact (100). This should be rare -- good sentence design narrows to one primary target.
- **Operator asks for a hint:** Do not provide hints. Respond: "No hints in the field, operator. Trust your vocabulary. Submit your best word."
