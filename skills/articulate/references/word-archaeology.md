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

Every story MUST meet all four criteria:

1. **Genuine surprise** — contains a fact that makes the reader stop and think
2. **Cited origin** — names the actual language of origin (Latin, Old Norse, Proto-Germanic, etc.)
3. **Narrative arc** — reads as a story, not a dictionary entry. Has movement, tension, or irony
4. **Modern connection** — explains how the etymology shapes the word's current usage or connotation

## Exercise Design

The exercise MUST flow from the story. It should feel like a natural next step, not a disconnected drill.

**Exercise types (pick one per session):**

- Write a sentence applying the principle from the story
- Rewrite a weak sentence using the etymology pattern
- Find a better word by applying the origin insight
- Write a professional passage using the featured word precisely
- Identify a word in your own recent writing that has a similar drift pattern

**Constraints:** ONE exercise per session. Keep instructions to 2-3 lines. Set a word limit when appropriate.

## Topic Selection

1. Check `~/.articulate/history.json` — avoid any word used in the last 20 sessions
2. If user is multilingual (check `user.json` languages), alternate between their languages
3. Tie to project context when possible — if user works in finance, prefer finance-adjacent etymologies
4. Prefer words the user is likely to encounter in professional writing

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

## Scoring Rubric

After the user responds, score using the Archaeology rubric:

| Axis | 0-25 |
|------|------|
| Precision | Word choice accuracy, specificity |
| Creativity | Unexpected but effective choices |
| Principle Application | How well they applied the session's principle |
| Naturalness | Reads like a human wrote it, not a thesaurus |

Use the axis bar format from style.md for display.

## Post-Session Flow

After scoring: save to history.json, update XP, then:

> "Another dig? Or back to work."
