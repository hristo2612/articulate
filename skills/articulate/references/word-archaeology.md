# Word Archaeology — The Science-Backed Method

The default `/articulate` experience. Stacks four proven learning methods into a tight 2-response session:

1. **Productive failure** (Kapur, 2008): write FIRST, struggle, THEN discover. 2x retention.
2. **Contrastive analysis**: comparing versions forces deeper processing.
3. **Protégé effect** (Biswas, 2005): teaching someone else is the strongest form of learning.
4. **Elaborative interrogation** (Pressley, 1987): generating "WHY" explanations = 2x retention.

## Session Structure

Two user responses. Tight, focused, powerful.

**Flow: challenge → struggle → teach → discover → retry.**

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

## Post-Session Flow

After scoring: save to history.json, update XP, then:

> **What's next?**
> 🔍 Another challenge — `go`
> 🔥 Roast my writing — `roast`
> 📊 My stats — `stats`
> ✌️ Back to work
