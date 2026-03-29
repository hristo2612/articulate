# Word Archaeology — Productive Failure Method

The default `/articulate` experience. Uses **productive failure** (Kapur, 2008): the user writes FIRST with no instruction, struggles, THEN learns why their instincts were right or wrong. Struggle-first produces 2x retention vs instruction-first.

## Session Structure — THE FLIP

Traditional: teach → practice. Articulate: **practice → struggle → discover → practice again.**

Every session follows this exact sequence:

### Phase 1: The Challenge (no teaching yet)

1. `## 🔍 Word Archaeology: The Challenge` — heading
2. **The scenario** — a specific, real-world writing task (1-2 lines)
3. **The constraint** — what makes it hard (word limit, register requirement, audience)
4. `### ✏️ Your first attempt` — user writes BEFORE learning anything
5. `>` blockquote — space for response

**Critical:** Do NOT teach anything yet. No etymology, no principles, no hints. The user must struggle with their own instincts first. This is the "productive failure" — the struggle creates the neural hooks that make the subsequent teaching stick.

### Phase 2: The Reveal (after user responds)

1. **React honestly** — what worked, what didn't, be specific
2. `## 🔍 The Dig` — NOW reveal the fascinating language story
   - Show the etymology/principle that would have helped them
   - Connect it to THEIR specific word choices: "You wrote '{X}' — here's why that felt off..."
   - 4-8 lines, same quality bar as before (surprise, cited origin, narrative arc, modern connection)
3. `💡 **The principle:**` — one transferable insight (bold, 1-2 lines)
4. **Show the gap** — their version vs. a gold standard, with WHY the gold standard works

### Phase 3: The Retry

1. `### ✏️ Now rewrite it` — same challenge, armed with the principle
2. The user rewrites knowing what they now know
3. Score BOTH attempts — show the improvement delta

## Scenario Design

Scenarios must feel like REAL tasks the user encounters in daily work. Never artificial.

**Scenario types (rotate):**

| Type | Example |
|------|---------|
| Email precision | "Decline a meeting without being passive-aggressive. One sentence." |
| PR description | "Summarize what this change does in under 15 words." |
| Slack update | "Tell your team the deploy failed without causing panic. Two sentences." |
| Feedback | "Give constructive criticism on someone's proposal. One sentence, no hedges." |
| Persuasion | "Convince your manager to approve a tool purchase. Two sentences." |
| Explanation | "Explain a technical concept to a non-technical stakeholder. Three sentences max." |

**The constraint is what makes it hard:** word limits, banned words, required register, specific audience. Constraints force word choice — which is exactly what we're training.

## The Dig — Story Categories

After the user's first attempt, reveal the relevant language story. Rotate through these:

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

The story MUST meet all six criteria:

1. **Genuine surprise** — "wait, really?" moment
2. **Cited origin** — names the actual language of origin
3. **Narrative arc** — reads as a story, not a dictionary entry
4. **Modern connection** — explains how etymology shapes current usage
5. **Connected to the user's attempt** — references their actual word choices
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
- +0-5: "Hmm. The principle didn't land yet. Read the dig again."
- +6-15: "Getting there. You're thinking about it differently."
- +16-25: "Now you're cooking. That's what awareness does."
- +26+: "Night and day. That's productive failure working."

## Topic Selection

1. Check `~/.articulate/history.json` — avoid any scenario used in the last 20 sessions
2. **Rotate scenario types** — never pick the same type twice in a row
3. If user is multilingual (check `user.json` languages), alternate between their languages
4. Tie to project context when possible
5. Prefer scenarios the user encounters in professional work
6. **First session:** Use "Decline a meeting without being passive-aggressive. One sentence." — universal, immediately practical
7. **Never repeat the same scenario** across sessions

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
Interesting. "Has some issues" — you're hedging without hedge words. "Look into it" — vague. Let's dig.

## 🔍 The Dig: *triage*

When medieval French doctors faced battlefield casualties, they couldn't save everyone. They sorted patients into three groups — *trier*, "to sort" (Old French, from Latin *tritare*, to grind/separate). The word entered English as **triage**: the art of deciding what matters RIGHT NOW.

That's what your Slack message needed. Not "issues" (vague) or "investigating" (passive). Your team needs to know: what broke, what's the blast radius, what's the next action. Triage language is active and specific.

💡 **The principle:** Crisis communication borrows from battlefield medicine — sort, prioritize, act. Vague words ("issues", "look into") waste the one thing you don't have in a crisis: time.

**Your version vs. gold standard:**

> ❌ "The latest deploy has some issues and we need to look into it."
> ✅ "Deploy rolled back — checkout page was returning 500s. I'm triaging the migration script now."

The gold standard has: what happened (rolled back), what broke (checkout 500s), what's next (triaging migration). Zero wasted words.

### ✏️ Now rewrite it

Same scenario, same constraints. Armed with the principle.

>
```

## Post-Session Flow

After scoring the rewrite: save to history.json, update XP, then:

> **What's next?**
> 🔍 Another challenge — `go`
> 🔥 Roast my writing — `roast`
> 📊 My stats — `stats`
> ✌️ Back to work
