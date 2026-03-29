# Word Archaeology — The Science-Backed Method

The default `/articulate` experience. Stacks three proven learning methods:

1. **Productive failure** (Kapur, 2008): user writes FIRST, struggles, THEN discovers the principle. 2x retention.
2. **Contrastive analysis**: comparing two versions forces deeper processing than studying either alone.
3. **Elaborative interrogation** (Pressley, 1987): asking "WHY does this work?" produces 2x retention vs being told.

## Session Structure

Traditional: teach → practice. Articulate: **challenge → struggle → compare → explain → discover → retry.**

Every session follows this exact sequence:

### Phase 1: The Challenge (no teaching yet)

1. `## 🔍 Word Archaeology: The Challenge` — heading
2. **The scenario** — a specific, real-world writing task (1-2 lines)
3. **The constraint** — what makes it hard (word limit, register requirement, audience)
4. `### ✏️ Your first attempt` — user writes BEFORE learning anything
5. `>` blockquote — space for response

**Critical:** Do NOT teach anything yet. No etymology, no principles, no hints. The struggle creates neural hooks.

### Phase 2: Compare + Explain (after user responds)

1. **React honestly** — what worked, what didn't in their attempt. Score Attempt 1.
2. `## 🔍 Spot the Difference` — show TWO versions of a similar piece of writing:
   - **Version A:** weak/vague language (similar to common mistakes)
   - **Version B:** precise/powerful language
3. **Ask TWO questions (elaborative interrogation):**
   - "Which is stronger?"
   - "WHY does that word work better? What does it do that the other doesn't?"
4. `>` blockquote — space for their explanation

**This is the key move.** The user must GENERATE the explanation, not consume it. Self-explanation activates deeper encoding than reading someone else's explanation.

### Phase 3: The Dig (after user explains — or immediately in non-interactive mode)

1. **React to their explanation** — what they got right, what they missed
2. `## 🔍 The Dig` — the etymology/language story that reveals the FULL picture
   - Connect to THEIR word choices from Phase 1 AND their explanation from Phase 2
   - 4-8 lines: surprise, cited origin, narrative arc, modern connection
   - Show them what their explanation missed — the deeper layer
3. `💡 **The principle:**` — one transferable insight (bold, 1-2 lines)

### Phase 4: The Retry

1. `### ✏️ Now rewrite it` — same challenge, armed with everything they've learned
2. Score BOTH attempts — show the improvement delta

### Phase 3: The Retry

1. `### ✏️ Now rewrite it` — same challenge, armed with the principle AND the comparison
2. Score BOTH attempts — show the improvement delta

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

**The constraint is what makes it hard:** word limits, banned words, required register, specific audience.

## Contrastive Pair Design

The two versions must:
- Address the SAME communication task (related to the user's scenario)
- Differ in 1-3 key word choices (not total rewrites)
- Have one clearly stronger version (but the reason should be non-obvious)
- Connect to a fascinating etymology or language principle

**Example contrastive pair:**
> **A:** "We need to revisit the timeline because some deliverables are at risk."
> **B:** "We need to compress the timeline — three deliverables ship late if we don't cut scope by Friday."

**The key difference:** "revisit" (vague, implies maybe-later) vs. "compress" (active, implies urgency + specific action). Plus: "at risk" (hedge) vs. specific consequence + deadline.

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
Solid instinct to own it personally ("I'll be investigating"). But "has some issues" is doing zero work — which issues? Where? How bad?

## 🔍 Spot the Difference

Two incident messages. Which is stronger? What's the ONE word that makes the biggest difference?

> **A:** "The deploy caused some problems with the checkout flow. We're looking into it and will update soon."
> **B:** "The deploy broke checkout — users are hitting 500s on payment. Rolled back, monitoring now."

---

**The word:** "broke" vs. "caused some problems."

"Caused some problems" is 3 words to say nothing. "Broke" is 1 word that says everything. But here's the deeper reason...

## 🔍 The Dig: *break*

Old English *brecan* — from Proto-Germanic *brekaną*, from Proto-Indo-European *bhreg-* ("to break"). This root is ancient, physical, and brutal. It gave us: "breach" (a gap in a wall), "fraction" (a broken number, via Latin *frangere*), and "fragile" (easily broken).

"Caused some problems" is bureaucratic distance — you're standing 50 feet from the fire describing the temperature. "Broke" puts everyone AT the break point. It's a 5,000-year-old word that means exactly one thing, and everyone who reads it reacts the same way: something was whole, now it isn't.

This is why crisis language defaults to Anglo-Saxon roots: break, fix, stop, cut, ship. These words survived a millennium because they're unambiguous. Latinate alternatives ("encountered difficulties", "experiencing issues") survived because they create distance — which is exactly what you DON'T want in an incident.

💡 **The principle:** In crisis communication, reach for the oldest, shortest word. Anglo-Saxon roots (break, fix, cut, stop) carry urgency because they're physical. Latinate words (encounter, experience, investigate) carry distance. Choose based on whether you want your reader to feel or to file.

### ✏️ Now rewrite it

Same scenario, same constraints. But this time — break things with short words.

>
```

## Post-Session Flow

After scoring: save to history.json, update XP, then:

> **What's next?**
> 🔍 Another challenge — `go`
> 🔥 Roast my writing — `roast`
> 📊 My stats — `stats`
> ✌️ Back to work
