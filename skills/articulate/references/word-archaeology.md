# Word Archaeology

The default `/articulate` experience. A 60-second fascinating language discovery.

## Session Structure

Every Word Archaeology session follows this exact format:

1. `## 🔍 Word Archaeology: *{word}*` — heading with the word in italics
2. **The story** (4-8 lines) — genuinely interesting etymology, surprising origins, how meaning shifted over time
3. `💡 **The principle:**` — one transferable insight about language (bold, 1-2 lines)
4. `### ✏️ Your turn` — one exercise that flows directly FROM the story
5. `>` blockquote — space for user response

## Story Categories

Rotate through these to keep sessions varied. Track in history.json to avoid clustering.

| Category | What it covers |
|----------|---------------|
| Etymology deep dive | Full origin chain: Latin → Old French → Middle English → modern |
| Semantic drift | Words that meant something wildly different (e.g., "nice" = foolish in 1300) |
| Cross-language connections | Same root surfacing in 3+ languages, false friends, calques |
| Hidden metaphors | Everyday words with buried figurative origins (e.g., "salary" from salt) |
| Register archaeology | How a word moved between social registers over centuries |
| Eponyms | Words born from people (boycott, algorithm, nicotine) |
| Back-formations | Words created by mistakenly removing affixes (edit ← editor) |

## Quality Bar

Every story MUST meet all six criteria:

1. **Genuine surprise** — contains a fact that makes the reader stop and think. Test: would someone say "wait, really?" If not, find a better angle.
2. **Cited origin** — names the actual language of origin (Latin, Old Norse, Proto-Germanic, etc.)
3. **Narrative arc** — reads as a story, not a dictionary entry. Has movement, tension, or irony. Use time markers ("In 1300...", "By the 1920s..."), sensory details, and concrete scenes.
4. **Modern connection** — explains how the etymology shapes the word's current usage or connotation
5. **Sensory anchoring** — include at least one vivid image: a line in the dirt, a printing press, a Roman road junction. Abstract facts don't stick; scenes do.
6. **Emotional hook** — open with the most surprising detail, not chronological background. Lead with irony, paradox, or the "wait, what?" moment. Don't bury the lede.

## Exercise Design

The exercise MUST flow from the story. It should feel like a natural next step, not a disconnected drill.

**Exercise types (pick one per session):**

- Write a sentence applying the principle from the story
- Rewrite a weak sentence using the etymology pattern
- Find a better word by applying the origin insight
- Write a professional passage using the featured word precisely
- Identify a word in your own recent writing that has a similar drift pattern

**Constraints:** ONE exercise per session. Keep instructions to 2-3 lines. Set a word limit when appropriate.

**Exercise formatting:**
- Use `### ✏️ Your turn` heading
- Put the weak/target sentence in a `>` blockquote with weak words in **bold**
- State the constraint clearly (word limit, technique to apply)
- End with an empty `>` for the user's response

**Bonus round (optional, after scoring):** If the user scored 70+, offer a 💎 **Bonus nugget** — one additional fascinating fact related to the session's word that they can take away. Example: "💎 *Fun fact: the word 'nice' went through 7 distinct meanings in 700 years — foolish → wanton → lazy → delicate → precise → agreeable → pleasant. No other English word has drifted this far.*"

## Topic Selection

1. Check `~/.articulate/history.json` — avoid any word used in the last 20 sessions
2. **Rotate categories** — never pick the same story category twice in a row. If last session was "etymology deep dive", pick "semantic drift" or "hidden metaphors" next.
3. If user is multilingual (check `user.json` languages), alternate between their languages
4. Tie to project context when possible — if user works in finance, prefer finance-adjacent etymologies
5. Prefer words the user is likely to encounter in professional writing
6. **First session suggestions** (universally fascinating): salary, trivial, disaster, panic, candidate, nice, muscle, sarcasm — pick one at random

**Avoid:** Overused etymology trivia (OK origins, SOS meaning, etc.). Pick words that professionals USE daily but whose origins they don't know.

## Example Session

```markdown
## 🔍 Word Archaeology: *trivial*

In ancient Rome, the *trivium* was where three roads met — literally "three ways" (Latin *tri-* + *via*). These crossroads became gathering spots where ordinary people chatted about ordinary things.

The word drifted through centuries carrying that association: trivium → trivialis → "commonplace" → "unimportant." A word born from the geometry of roads became our way of dismissing things that don't matter.

Here's the twist: the medieval *trivium* was also the name for the foundational university curriculum (grammar, logic, rhetoric). The "trivial" arts were considered essential — the opposite of how we use the word today.

💡 **The principle:** Words that describe importance often started as words about physical space. "Fundamental" = foundation. "Underlying" = beneath. "Trivial" = crossroads. When you need to convey significance, spatial metaphors hit harder than abstract ones.

### ✏️ Your turn

Rewrite this sentence using a spatial metaphor instead of the abstract language:

> "This issue is very important to the project's success and shouldn't be ignored."

Max 20 words.

>
```

## Scoring & Feedback

After the user responds, give feedback in this order:

1. **React first** — one genuine sentence about what worked or didn't. Be specific: "That verb swap was surgical" or "Close, but 'impacted' is just a dressed-up version of 'affected'."
2. **Show the score** with axis bars:
   ```
   **Score: 72/100**
   ├─ ✓ Precision:   20/25
   ├─ ✓ Creativity:  18/25
   ├─ ✗ Principle:   16/25  ← didn't use a body-rooted verb
   └─ ✓ Naturalness: 18/25
   ```
3. **Gold standard** — show one ideal version in a `>` blockquote. Explain in 1-2 bullets WHY it works, connecting back to the session's principle.
4. **💎 Bonus nugget** (if score ≥ 70) — one additional fascinating fact about the word.

**Scoring axes:**
| Axis | 0-25 | What to evaluate |
|------|------|-----------------|
| Precision | Word accuracy and specificity — did they replace vague with precise? |
| Creativity | Unexpected but effective choices — did they surprise you? |
| Principle Application | Did they apply THIS session's specific principle? |
| Naturalness | Reads like a human, not a thesaurus — would someone actually write this? |

## Post-Session Flow

After scoring: save to history.json, update XP, then:

> "🔍 Another dig? 🔥 Roast my writing? Or back to work."
