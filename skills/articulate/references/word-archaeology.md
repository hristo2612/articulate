# Word Archaeology — The Science-Backed Method

The default `/articulate` experience. **Three session formats that rotate** to prevent habituation (interleaving at the session level).

### Science behind it
1. **Productive failure** (Kapur, 2008): write FIRST, struggle, THEN discover. 2x retention.
2. **Contrastive analysis**: comparing versions forces deeper processing.
3. **Protégé effect** (Biswas, 2005): teaching someone else is the strongest form of learning.
4. **Reverse engineering**: analyzing expert work builds pattern recognition (Chi et al., 1989).
5. **Interleaving** (Rohrer & Taylor, 2007): mixing formats > repeating one format.
6. **Testing effect** (Roediger & Karpicke, 2006): retrieval practice > re-studying.

## Format Selection

**Rotate through three formats: A → B → C → A → B → C...** Check `history.json` for last format used.

- **Format A: The Challenge** — 2 responses. Productive failure + protégé effect. (write → teach → discover → retry)
- **Format B: The Reverse** — 2 responses. Reverse engineering + generation. (analyze great writing → extract → apply)
- **Format C: The Snap** — 1 response. Ultra-fast micro-session. (one sentence → one word swap → WHY → done). For busy days or warm-ups.

---

## Format A: The Challenge

Two user responses. Flow: **challenge → struggle → teach → discover → retry.**

### Phase 1: The Challenge (no teaching yet)

1. `## 🔍 Word Archaeology: The Challenge` — heading
2. **The scenario** — a specific, real-world writing task (1-2 lines)
3. **The constraint** — what makes it hard (word limit, register requirement, audience)
4. `### ✏️ Your first attempt` — user writes BEFORE learning anything
5. `>` blockquote — space for response

**Critical:** Do NOT teach anything yet. No etymology, no principles, no hints. The struggle creates neural hooks.

### Phase 2: The Teach-Back (after user responds)

1. **React honestly** — what worked, what didn't. Score Attempt 1 with axis bars.
2. `## 🔍 Spot the Difference` — show TWO versions of similar writing:
   - **Version A:** weak/vague (similar to common mistakes)
   - **Version B:** precise/powerful
3. **The Protégé Challenge:**
   > "A junior dev on your team just wrote Version A. They think it's fine. In 1-2 sentences, explain what they should change and **WHY** the alternative works better."
4. `>` blockquote — space for their teaching explanation

**Why this works:** The user must TEACH, not just identify. Teaching activates deeper processing than self-explanation alone. The social framing ("a junior dev") makes it concrete and engaging. They're not analyzing in a vacuum — they're preparing to help someone.

### Phase 3: The Dig + Retry (after user teaches — or immediately in non-interactive mode)

1. **Grade their teaching** — what they got right, what they missed, what would confuse the "junior dev"
2. `## 🔍 The Dig` — the etymology/language story that reveals the deeper layer
   - Connect to THEIR word choices from Phase 1 AND their teaching from Phase 2
   - 4-8 lines: surprise, cited origin, narrative arc, modern connection
   - Show what their explanation missed — the layer they couldn't articulate
3. `💡 **The principle:**` — one transferable insight (bold, 1-2 lines)
4. `### ✏️ Now rewrite it` — same challenge, armed with everything
5. `>` blockquote

After rewrite: score BOTH attempts, show improvement delta.

## Scenario Design

Scenarios must feel like REAL tasks. Never artificial.

**Scenario types (rotate):**

| Type | Example |
|------|---------|
| Email precision | "Decline a meeting without being passive-aggressive. One sentence." |
| PR description | "Summarize what this change does in under 15 words." |
| Slack update | "Tell your team the deploy failed without causing panic. Two sentences." |
| Feedback | "Give constructive criticism on someone's proposal. One sentence, no hedges." |
| Persuasion | "Convince your manager to approve a tool purchase. Two sentences." |
| Explanation | "Explain a technical concept to a non-technical stakeholder. Three sentences max." |
| Apology | "Acknowledge a missed deadline without making excuses. Two sentences." |
| Announcement | "Announce a breaking change to your API consumers. Three sentences." |

**The constraint is what makes it hard:** word limits, banned words, required register, specific audience.

## Contrastive Pair Design

The two versions must:
- Address the SAME communication task (related to the user's scenario)
- Differ in 1-3 key word choices (not total rewrites)
- Have one clearly stronger version (but the reason should be non-obvious)
- Connect to a fascinating etymology or language principle

## The Dig — Story Categories

| Category | What it covers |
|----------|---------------|
| Etymology deep dive | Full origin chain: Latin → Old French → Middle English → modern |
| Semantic drift | Words that meant something wildly different centuries ago |
| Cross-language connections | Same root surfacing in 3+ languages |
| Hidden metaphors | Everyday words with buried figurative origins |
| Register archaeology | How words moved between social classes over centuries |
| Connotation layers | Why "request" ≠ "ask" ≠ "demand" — and the history behind it |
| Word families | How one root spawned 10 words across different registers |

## Quality Bar

Every story MUST:

1. **Genuine surprise** — "wait, really?" moment
2. **Cited origin** — names the actual language of origin
3. **Narrative arc** — reads as a story, not a dictionary entry
4. **Connected to the user's attempt** — references their actual word choices
5. **Connected to the contrastive pair** — explains WHY Version B's word is stronger
6. **Actionable** — the principle directly improves their rewrite

## Scoring — Double Score

Score BOTH attempts and show the improvement:

**First attempt (before learning):**
```
**Attempt 1: {score}/100**
├─ Precision:   {n}/25
├─ Concision:   {n}/25
├─ Register:    {n}/25
└─ Impact:      {n}/25
```

**Second attempt (after learning):**
```
**Attempt 2: {score}/100**
├─ Precision:   {n}/25  {↑n}
├─ Concision:   {n}/25  {↑n}
├─ Register:    {n}/25  {↑n}
└─ Impact:      {n}/25  {↑n}

📈 **Improvement: +{delta} points** — {reaction}
```

**Scoring axes:**
| Axis | What to evaluate |
|------|-----------------|
| Precision | Right word for the right job — not vague, not thesaurus-hunting |
| Concision | Said it in as few words as possible without losing meaning |
| Register | Appropriate formality for the scenario's audience |
| Impact | Would this actually work? Would the reader respond well? |

**Improvement reactions:**
- +0-5: "Hmm. The principle didn't land yet."
- +6-15: "Getting there. You're thinking about it differently."
- +16-25: "Now you're cooking. That's awareness at work."
- +26+: "Night and day. That's productive failure in action."

## Topic Selection

1. Check `~/.articulate/history.json` — avoid repeats from last 20 sessions
2. **Rotate scenario types** — never same type twice in a row
3. If user is multilingual, alternate languages
4. Tie to project context when possible
5. **First session:** "Decline a meeting without being passive-aggressive. One sentence."
6. **Never repeat scenarios**

## Example Session

```markdown
## 🔍 Word Archaeology: The Challenge

**Scenario:** Your deploy just broke production at 5pm on a Friday. Write a Slack message to your team. Two sentences max.

**Constraints:** No hedging ("I think", "maybe"). No panic words ("urgent", "critical", "ASAP"). Just clarity.

### ✏️ Your first attempt

>
```

*[User writes: "The latest deploy has some issues and we need to look into it. I'll be investigating tonight."]*

```markdown
Solid instinct to own it ("I'll be investigating"). But "has some issues" and "look into it" are doing zero work.

**Attempt 1: 48/100**
├─ Precision:   10/25
├─ Concision:   12/25
├─ Register:    16/25
└─ Impact:      10/25

## 🔍 Spot the Difference

Two incident messages. Read both:

> **A:** "The deploy caused some problems with the checkout flow. We're looking into it and will update soon."
> **B:** "The deploy broke checkout — users are hitting 500s on payment. Rolled back, monitoring now."

A junior dev on your team just wrote Version A. They think it's fine for an incident channel. In 1-2 sentences, explain what they should change and WHY.

### ✏️ Your coaching

>
```

*[User writes: "Version B is better because it's more specific — it says exactly what broke and what action was taken. 'Broke' is more direct than 'caused some problems'."]*

```markdown
Good start — you correctly identified specificity as the key difference. But you said "more specific" and "more direct" without explaining WHY those qualities matter in THIS context. A junior dev hearing "be more specific" nods and writes the same thing tomorrow. Let me show you the lever you missed.

## 🔍 The Dig: *break*

Old English *brecan* — Proto-Germanic *brekaną* — Proto-Indo-European *bhreg-* ("to break"). This root is ancient, physical, and brutal. It gave us "breach" (gap in a wall), "fraction" (a broken number, via Latin *frangere*), and "fragile."

"Caused some problems" is bureaucratic distance — standing 50 feet from a fire describing the temperature. "Broke" puts everyone AT the break point. It's a 5,000-year-old word that means one thing, and everyone reacts the same: something was whole, now it isn't.

Crisis language defaults to Anglo-Saxon roots: break, fix, stop, cut, ship. These survived a millennium because they're unambiguous. Latinate alternatives ("encountered difficulties", "experiencing issues") create distance — the opposite of what you need in an incident.

**What you could have told the junior dev:** "In an incident, use Anglo-Saxon verbs — broke, not 'caused problems.' Short old words create urgency. Long Latin words create distance. Choose based on whether you want your team to ACT or FILE."

💡 **The principle:** In crisis, reach for the oldest, shortest word. Anglo-Saxon roots carry urgency because they're physical. Latinate words carry distance. Your word choice controls whether your reader reacts or relaxes.

### ✏️ Now rewrite it

Same scenario, same constraints. Break things with short words.

>
```

---

## Format B: The Reverse

Two user responses. Flow: **analyze great writing → extract principle → apply it to YOUR work.**

### Phase 1: The Specimen

1. `## 🔍 Word Archaeology: The Specimen` — heading
2. Present a SHORT piece of exceptional writing (2-4 sentences). Sources:
   - Famous opening lines (adapted to professional context)
   - Exceptional incident postmortems, changelogs, or tech writing
   - Brilliant one-liners from speeches, journalism, or literature
3. **The challenge:** "This is unusually effective writing. In 1-2 sentences, explain WHY it works. What's the specific technique?"
4. `### 🔍 Your analysis` — space for response
5. `>` blockquote

**The specimen must be genuinely impressive** — the user should read it and think "damn, that's good" before they analyze it.

### Phase 2: The Dig + Apply (after user analyzes)

1. **Grade their analysis** — what they caught, what they missed
2. `## 🔍 The Dig` — reveal the deeper layer through etymology/language history
   - WHY that technique works at the word level
   - The historical/linguistic reason behind its power
   - 4-8 lines: surprise, cited origin, narrative arc
3. `💡 **The principle:**` — the transferable technique (bold, 1-2 lines)
4. **The application scenario** — a real-world writing task where this principle applies:
   - `### ✏️ Now apply it` — specific scenario with constraints
   - `>` blockquote

### Phase 3: Scoring

Score the application. One score (not double — no first attempt in this format).

```
**Score: {n}/100**
├─ Technique:   {n}/25  (did they actually use the specimen's technique?)
├─ Precision:   {n}/25
├─ Naturalness: {n}/25
└─ Impact:      {n}/25
```

### Example Format B Session

```markdown
## 🔍 Word Archaeology: The Specimen

Read this:

> "We can lick gravity, but sometimes the paperwork is overwhelming."
> — Wernher von Braun, on NASA bureaucracy

Four words do all the work: "lick" and "overwhelming." In 1-2 sentences, explain WHY this quote hits as hard as it does. What's the specific technique?

### 🔍 Your analysis

>
```

*[User writes: "The contrast between solving gravity (huge) and being beaten by paperwork (small) is funny. The word 'lick' is informal which makes it feel authentic."]*

```markdown
You caught the contrast — good. And "lick" being informal is true but not the real insight. Here's what you missed: the technique is **register collision**.

## 🔍 The Dig: *lick* vs. *overcome*

"Lick" comes from Old English *liccian* — a word about tongues and animals. By the 1800s, American English had turned it into slang for "beat" or "defeat" — a barroom word, a frontier word. When von Braun says "lick gravity," he's using a cowboy verb for humanity's greatest engineering achievement.

"Overcome" would be the expected register: formal, Latinate, dignified. "Lick" is the wrong register — and that's exactly why it works. The mismatch between the word's lowness and the concept's grandness creates surprise. Your brain expects one register and gets another. That gap IS the humor.

This is **register collision**: deliberately using a word from the wrong social stratum. It signals confidence (you don't need fancy words for fancy achievements) and creates memorability through surprise.

💡 **The principle:** Register collision — using a deliberately "wrong" register — creates memorability. Low words for high concepts ("lick gravity") and high words for low concepts ("the olfactory assault of that dumpster") both work. The gap between word and concept IS the effect.

### ✏️ Now apply it

**Scenario:** Write a one-sentence summary of a major refactor you just completed. Use register collision — one word should be deliberately "wrong" for the context.

Max 20 words.

>
```

---

## Format C: The Snap

ONE user response. Ultra-fast. Under 30 seconds. Perfect for busy days, warm-ups, or streak maintenance.

**Flow: sentence → swap → WHY → done.**

### The Entire Session

1. `## 🔍 Snap: One Word` — heading
2. Present ONE weak sentence (real-world, professional context)
3. **Bold** the weakest word
4. Ask: "Replace the bold word. One word only."
5. `>` blockquote — space for ONE word

After they respond:

6. **React** — did they nail it?
7. **The word** — show the ideal replacement, with a 2-line WHY (etymology or connotation)
8. **Score** — simple pass/fail with flair:
   - ✅ **Nailed it** — exact or equivalent replacement. +15 XP.
   - 🔶 **Close** — right direction, wrong word. +10 XP. Show the better option.
   - ❌ **Missed** — wrong direction. +5 XP. Show WHY the right word works.

**No axis bars, no improvement delta.** This is a snap — fast in, fast out, one insight.

### Example Format C Session

```markdown
## 🔍 Snap: One Word

> "We need to **address** the performance issues before launch."

Replace **address**. One word only.

>
```

*[User writes: "fix"]*

```markdown
🔶 **Close.** "Fix" is better than "address" — it's direct. But the ideal swap:

> "We need to **diagnose** the performance issues before launch."

**WHY:** "Address" (Latin *directiāre*, to straighten) means "turn toward" — vague, bureaucratic. "Fix" (Latin *fixus*, fastened) means "make permanent" — but you don't know what's wrong yet. "Diagnose" (Greek *diagnōsis*, to distinguish) means "identify the specific problem." Before launch, you need to KNOW what's wrong, not fix blindly. The word choice signals your thinking stage.

⚡ +10 XP — right instinct, sharper word available.

> 🔍 Another snap? `go` | 🔥 Roast? `roast` | ✌️ Back to work
```

### Snap Topic Selection

1. Use words from the user's ACTUAL weakness areas (check `state.json` weaknesses)
2. Target the weakness they hit most: vague nouns, weak verbs, hedges, fillers
3. If no weakness data, use common weak verbs: address, handle, deal with, look into, work on, process
4. Rotate between: **vague verbs**, **hedge words**, **filler phrases**, **register mismatches**

---

## Post-Session Flow (all formats)

After scoring: save to history.json, update XP, then:

> **What's next?**
> 🔍 Another challenge — `go`
> 🔥 Roast my writing — `roast`
> 📊 My stats — `stats`
> ✌️ Back to work
