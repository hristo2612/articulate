# MISSION: REWRITE

> Full operational reference. An AI agent reading ONLY this file can generate, present, evaluate, and debrief a REWRITE mission.

---

## Overview

The operator receives a weak sentence containing 2-4 utility/vague words. They rewrite it with precision. This is the core mission type -- available from Level 1 (RECRUIT) and the foundation of all vocabulary training.

**Principle:** Production over recognition. The operator must PRODUCE precise language, not select it from options.

---

## Generation Rules

### Sentence Source Material

Generate sentences a developer, founder, or knowledge worker would actually write:

- Slack messages to teammates
- Emails to clients, investors, or hiring candidates
- AI/LLM prompts
- Product pitches and elevator descriptions
- README descriptions and documentation
- Customer support replies
- Interview answers (behavioral and technical)
- PR descriptions and code review comments
- Changelog entries and release notes
- Conference talk proposals

### Weak Word Requirements

Each sentence MUST contain **2-4 identifiable weak words** from these categories:

| Category | Examples |
|---|---|
| Utility words | good, nice, bad, great, big, small, important, interesting |
| Hedging | I think, maybe, sort of, kind of, I guess, probably, or whatever |
| Vague nouns | thing, stuff, something, everything, aspect, area, situation |
| Weak verbs | do, make, get, have, go, help, use (when a precise alternative exists) |
| Filler words | basically, literally, actually, like, just, really, very |

Mark weak words with **bold** in the presented sentence so the operator knows exactly what to target.

### Context-Aware Generation

If the operator has `contextAware: true` in user.json and a cached project context exists in `~/.articulate/contexts/`, generate the sentence using their project domain, product name, audience, and features. This makes the mission immediately applicable to real work.

If context-aware is off or no context is cached, use generic professional scenarios.

---

## Difficulty Scaling

Scale sentence complexity based on the operator's current level:

### L1 -- RECRUIT (0 XP)

Simple sentences with obvious weak words. Basic vocabulary targets.

```
"The thing is really good and nice."
"We made some stuff that helps people do things faster."
"It's basically a very important tool for getting things done."
```

- 2-3 weak words per sentence
- Single clause, straightforward structure
- Target replacements are common precision words (e.g., "compelling", "streamline", "robust")

### L2 -- INITIATE (100 XP)

Professional context, subtler patterns. Weak words are embedded in reasonable-sounding prose.

```
"We should probably look into getting some kind of solution for this."
"The team did a good job making the thing work better."
"I think our approach is basically fine and should help with the situation."
```

- 2-4 weak words per sentence
- Professional register expected in response
- May include hedging patterns alongside utility words

### L3 -- OPERATIVE (300 XP)

Register-switching and audience-awareness. Operator must consider who they are writing for.

```
"Basically our product does stuff that helps companies handle their important processes."
"The update is really great and should make things significantly better for users."
```

- Specify the intended audience (investor, technical lead, customer, hiring manager)
- Operator must match register to audience
- Introduce compound weakness patterns (hedging + vague noun + weak verb)

### L4 -- SPECIALIST (600 XP)

Structural challenges. Compound sentences with multiple weakness types entangled.

```
"I think the thing we built is probably going to be really useful for people who need to do stuff related to managing their various important tasks and things."
```

- 3-4 weak words in a single complex sentence
- Structural rewrite may be needed (not just word swaps)
- Sentences may contain redundancy, circular phrasing, or buried meaning

### L5-L7 -- COMMANDER / ARCHITECT / MASTERMIND (1000+ XP)

Paragraph-level rewrites. Nuanced professional scenarios. Multi-audience considerations.

```
"Our product is basically a really good solution that helps various companies
do important things related to their data. We think it's nice because it
makes stuff easier and people seem to like it a lot."
```

- Full paragraph (2-4 sentences) with 4+ weak words distributed across them
- Multiple registers may need balancing (technical accuracy + persuasive impact)
- Gold standard involves restructuring, not just word replacement
- May specify constraints: "Rewrite for a Series A deck" or "Rewrite as a Hacker News Show HN post"

---

## Presentation Format

Use box-drawing characters. Terminal aesthetic. No decorative elements.

```
━━━ MISSION: REWRITE ✏️ ━━━━━━━━━━━━━━━━━━━━

Rewrite this sentence with precision:

> "The **thing** we built is **really good** and **helps** people **do stuff** faster."

Target: Replace the highlighted weak words.
Your rewrite:
```

For L3+, include audience context:

```
━━━ MISSION: REWRITE ✏️ ━━━━━━━━━━━━━━━━━━━━

AUDIENCE: Technical PM evaluating your API
REGISTER: Professional, precise, confident

Rewrite this sentence with precision:

> "Our **thing** is **basically** a **really good** way to **help** developers **do stuff** with payments."

Target: Replace the highlighted weak words.
Your rewrite:
```

For L5+, paragraph-level:

```
━━━ MISSION: REWRITE ✏️ ━━━━━━━━━━━━━━━━━━━━

AUDIENCE: Investor update email
REGISTER: Confident, data-driven, concise
CONSTRAINT: 2 sentences max

Rewrite this paragraph with precision:

> "Things have been **going really well** lately. We **got** a **lot** of
>  new users and our **stuff** is **basically** working **great**. **I think**
>  we're in a **good** position to **do** more **things** next quarter."

Your rewrite:
```

---

## Evaluation Rubric

**4 axes. 0-25 each. Total: 0-100.**

### Precision (0-25)

Did the operator replace vague words with specific, high-information alternatives?

| Score | Criteria |
|---|---|
| 25 | Every weak word replaced with a precise, contextually perfect alternative |
| 20 | Most weak words replaced well; one could be more precise |
| 15 | Some precision gained, but some weak words remain or replacements are only marginally better |
| 10 | Attempted but replacements are still somewhat vague |
| 5 | Minimal improvement |
| 0 | No meaningful change or worse than original |

### Conciseness (0-25)

Is the rewrite tight? Does every word earn its place?

| Score | Criteria |
|---|---|
| 25 | Every word earns its place, zero filler |
| 20 | Tight with perhaps one unnecessary word |
| 15 | Acceptable but could be trimmed |
| 10 | Added unnecessary words or padding |
| 5 | Significantly more verbose than needed |
| 0 | Bloated or padded with empty language |

### Impact (0-25)

Does the rewrite land? Is it clear, memorable, compelling?

| Score | Criteria |
|---|---|
| 25 | The sentence commands attention -- sharp, vivid, decisive |
| 20 | Strong and clear |
| 15 | Adequate but forgettable |
| 10 | Weak impact, easy to skim past |
| 5 | Confusing or bland |
| 0 | Worse than the original |

### Naturalness (0-25)

Does it sound like a real person wrote it? Not thesaurus-stuffed or overwrought?

| Score | Criteria |
|---|---|
| 25 | Completely natural, fits the register perfectly |
| 20 | Natural with minor awkwardness |
| 15 | Slightly forced or over-written |
| 10 | Sounds like someone used a thesaurus without judgment |
| 5 | Awkward or unnatural phrasing |
| 0 | Incomprehensible or alien-sounding |

---

## Feedback Format

After evaluation, present the debrief using this exact structure:

```
━━━ DEBRIEF ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SCORE: 78/100
├─ Precision:   22/25  ████████████████████░░░░░
├─ Conciseness: 18/25  ██████████████░░░░░░░░░░░
├─ Impact:      20/25  ████████████████░░░░░░░░░
└─ Naturalness: 18/25  ██████████████░░░░░░░░░░░

GOLD STANDARD:
> "The onboarding flow we shipped reduces task completion time by 40%."

WHY IT WORKS:
- "onboarding flow" --> specific noun replacing "thing"
- "shipped" --> decisive verb replacing "built" (implies completion + delivery)
- "reduces task completion time by 40%" --> measurable impact replacing "helps people do stuff faster"

YOUR WINS:
- [List specific word choices the operator got right and WHY they work]

COULD BE SHARPER:
- [List specific word choices that could improve and suggest alternatives with WHY]

WEAKNESSES DETECTED: utility_words, vague_nouns
```

### Score Bar Rendering

Each axis gets a 25-character bar. Fill proportionally:

- Score 25 = `█████████████████████████` (25 filled)
- Score 20 = `████████████████████░░░░░` (20 filled, 5 empty)
- Score 15 = `███████████████░░░░░░░░░░` (15 filled, 10 empty)
- Score 10 = `██████████░░░░░░░░░░░░░░░` (10 filled, 15 empty)
- Score 5  = `█████░░░░░░░░░░░░░░░░░░░░` (5 filled, 20 empty)
- Score 0  = `░░░░░░░░░░░░░░░░░░░░░░░░░` (0 filled, 25 empty)

### Gold Standard

ALWAYS provide a gold standard rewrite. This is the "ideal" version -- the sentence as a precision language expert would write it. The gold standard:

- Replaces every weak word with the strongest contextually-appropriate alternative
- Is tight -- no unnecessary words
- Sounds natural -- not overwrought or thesaurus-stuffed
- Matches the specified register and audience (if given)

### WHY Explanations

For EVERY word replacement in the gold standard, explain:

1. **What changed:** The specific word swap (old --> new)
2. **Why the new word is better:** What information, texture, or precision it adds
3. **What the old word lacked:** Why the original was weak in this context

These explanations are the core learning mechanism. Never skip them.

### YOUR WINS Section

Always acknowledge what the operator did well. Be specific:

- Name the exact word choices that were strong
- Explain why they work (register fit, precision, connotation)
- This reinforces correct behavior and builds confidence

### COULD BE SHARPER Section

Only include if the operator missed opportunities. Be constructive:

- Name the specific weak word that survived or was replaced with a still-weak alternative
- Suggest 1-2 stronger alternatives with brief explanations
- Frame as opportunity, not failure: "could be sharper" not "you failed"

---

## Weakness Mapping

After evaluation, identify weakness categories from two sources:

### 1. Weaknesses in the ORIGINAL sentence (what was presented)

Tag which of the 6 weakness categories appeared in the challenge sentence:

- `utility_words` -- "good", "nice", "bad", "great", "big", "small", "important"
- `hedging` -- "I think", "maybe", "sort of", "kind of", "I guess"
- `flat_structure` -- monotone rhythm, no contrast, no emphasis
- `vague_nouns` -- "thing", "stuff", "something", "everything", "aspect"
- `weak_verbs` -- "do", "make", "get", "have", "be", "go"
- `filler_words` -- "basically", "literally", "actually", "like", "just", "really", "very"

### 2. Weaknesses the operator FAILED TO FIX or INTRODUCED

Only count weaknesses the operator:
- **Kept** from the original (weak word was there and they did not replace it)
- **Introduced** in their rewrite (new weak word not in the original)

Do NOT count weaknesses the operator successfully eliminated. Those are wins.

### Output

Report detected weaknesses in the `WEAKNESSES DETECTED:` line of the debrief. These feed into the weakness radar in `~/.articulate/state.json` for trend tracking.

Format: comma-separated category names. Example:

```
WEAKNESSES DETECTED: utility_words, vague_nouns
```

If the operator eliminated all weaknesses cleanly:

```
WEAKNESSES DETECTED: none -- clean sweep
```

---

## Daily Word Bonus

If the operator's session included a daily word, check whether it appears in their rewrite response. If so, award +5 bonus XP and note it in the debrief:

```
DAILY WORD BONUS: +5 XP ("streamline" deployed in the field)
```

---

## Edge Cases

- **Operator rewrites but adds new weak words:** Score Precision based on net improvement. Note introduced weaknesses in the COULD BE SHARPER section.
- **Operator completely restructures the sentence:** This is fine and often desirable at L4+. Evaluate the final product, not whether they preserved the original structure.
- **Operator's rewrite changes the meaning:** Dock Impact points. Note in feedback that precision must serve the original intent.
- **Operator uses an obscure/unusual word correctly:** Award full Precision and Naturalness only if the word fits the register. A technically precise word that sounds out of place loses Naturalness points.
- **Operator submits a one-word response or refuses:** Score 0/100. Encourage them to try again.
