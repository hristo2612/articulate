# Roast Mode — The Detective Game

Short, punchy detective game. User's real writing → find the problems yourself → rewrite. Keep it TIGHT — same length rules as missions (8 lines challenge, 12 lines feedback).

## Source Scanning

### `roast` (default) — scan past conversations

Read from these sources in order:

1. `~/.claude/projects/**/*.jsonl` — Claude Code conversations. User messages have `"type": "user"`, text lives in `message.content`
2. `~/.codex/history.jsonl` — Codex conversations. Text in the `text` field
3. `~/.codex/archived_sessions/*.jsonl` — Older Codex sessions, same format

### `roast here` — scan current conversation only

Use messages from the current conversation preceding the `/articulate roast here` invocation.

### Collection rules

- Gather 20-30 substantial user messages
- **Skip:** one-word answers, file paths, CLI commands, code snippets, messages under 10 words
- **Keep:** natural language instructions, explanations, descriptions, requests
- Sort by weakness density (most problems first)

## The Detective Flow

### Phase 1: The Crime Scene

1. `## 🔥 Roast: The Crime Scene` — heading
2. Present the user's ACTUAL passage, quoted exactly
3. **The challenge:** "This message has **{N} problems.** Find as many as you can. Mark each with what's wrong."
4. Don't reveal what the problems are. Don't hint. Let them hunt.
5. `### 🔍 Your analysis` — space for user's detective work
6. `>` blockquote

**This is the key innovation:** Traditional roast mode SHOWS you the weaknesses. Detective mode makes you FIND them. Finding = deeper processing than reading a list.

### Phase 2: The Verdict (after user responds)

1. **Score their detection:** How many of the {N} problems did they catch?
   ```
   **Detection: {caught}/{total}**
   🔍🔍🔍🔍🔍  (filled per caught, empty per missed)
   ```
2. **What they caught** — acknowledge with ✓, validate their reasoning
3. **What they missed** — reveal with ✗, each one explained:
   - Quote the specific words
   - Name the weakness type (emoji coded)
   - Explain WHY it's a problem (1 line)
   - Show the fix (1 line)
4. **The teaching moment** — 2-3 lines explaining the PATTERN behind the missed weaknesses. Connect to etymology or language principle when possible.

### Phase 3: The Rewrite Challenge

1. `### ✏️ Rewrite challenge` — same as before
2. Now they know ALL the problems. Rewrite to fix them.
3. Word limit = essential content words (strip all waste)
4. `>` blockquote

### Phase 4: Scoring

1. **React** — genuine reaction to their rewrite
2. **Before/After comparison:**
   ```
   **Before:** ~{N} words, {M} weaknesses
   **After:**  ~{N} words, {M} weaknesses
   📉 **{X}% compression** — {reaction}
   ```
3. **Score with axis bars:**
   ```
   **Score: {n}/100**
   ├─ Detection:    {n}/25  (how many problems you spotted in Phase 1)
   ├─ Compression:  {n}/25  (waste cut)
   ├─ Precision:    {n}/25  (vague → specific)
   └─ Naturalness:  {n}/25  (reads like a human)
   ```
4. **Gold standard** in blockquote, with WHY bullets

## Weakness Patterns to Find

| # | Pattern | Emoji | Example |
|---|---------|-------|---------|
| 1 | Hedge stacking | 🟡 | "I think maybe we could possibly..." |
| 2 | Vague noun avalanches | 🔴 | "the thing with the stuff in the something" |
| 3 | Filler word bloat | 🟡 | "basically", "literally", "just", "really", "actually" |
| 4 | Weak verb chains | 🔴 | "make it do the thing" instead of a precise verb |
| 5 | Register confusion | 🟠 | Mixing casual slang into formal requests |
| 6 | Buried action | 🟠 | The actual request is in sentence 3 of 5 |
| 7 | Passive deflection | 🟡 | "It was decided" instead of "We decided" |

**Teaching moments (use after revealing missed weaknesses):**
- Hedge stacking: "Every hedge is an apology for having an opinion. Three in one sentence and you're asking permission to exist."
- Vague nouns: "'Thing' is a vocabulary void — your brain had a concept but your words gave up halfway."
- Filler bloat: "Fillers are verbal throat-clearing. They signal 'I'm about to say something' instead of just saying it."
- Weak verbs: "'Make' and 'do' are English's laziest verbs. They work anywhere, which means they mean nothing."
- Register confusion: "Mixing 'gonna' with 'pursuant to' makes you sound like two different people arguing in one email."
- Buried action: "If your reader has to excavate your request from paragraph 3, you're not communicating — you're hiding."
- Passive deflection: "'It was decided' is the grammatical equivalent of leaving the room before anyone can ask who decided."

**Optional 🔍 etymology hook:** If the roast reveals a pattern, drop a 1-line etymology nugget. Example: "🔍 *Fun fact: 'thing' originally meant a public assembly in Old Norse. You're accidentally calling every object a Viking parliament.*"

## Example Session

```markdown
## 🔥 Roast: The Crime Scene

I found this in your recent writing:

> "I think we should maybe try to basically refactor the thing that handles the stuff for the user authentication part of the system."

This message has **6 problems.** Find as many as you can. For each one, quote the words and name what's wrong.

### 🔍 Your analysis

>
```

*[User identifies 4 of 6]*

```markdown
**Detection: 4/6**
🔍🔍🔍🔍⬜⬜

**What you caught:**
✓ "I think" — hedge (correct!)
✓ "maybe" — hedge (correct!)
✓ "basically" — filler (correct!)
✓ "the thing that handles the stuff" — vague noun avalanche (spot on)

**What you missed:**
✗ 🟡 **"try to"** — hedge. "Try to refactor" = "maybe refactor, maybe not." If you're going to do it, say "refactor." If you're proposing it, say "I propose we refactor."
✗ 🟠 **"part of the system"** — padding. Everything is a part of a system. This adds zero information.

**The pattern:** 3 of your 6 problems are hedges. That's not cautious communication — that's a confidence leak. Every hedge gives your reader permission to ignore you.

💡 *Fun fact: "hedge" comes from Old English "hecg" — a fence of bushes. When you hedge in writing, you're literally planting bushes between you and your point so no one can see it clearly.*

### ✏️ Rewrite challenge

Say what you actually mean. Max 6 words.

>
```

## Multi-Round Flow

1. Find **3** weak passages from the source material
2. Present the **worst** one first (as the crime scene)
3. After scoring the rewrite, offer: "🔥 Want crime scene #2?"
4. If yes, present the second, then third

## Privacy Rules

Non-negotiable. NEVER surface:
- **Credentials** — API keys, tokens, passwords, secrets
- **Personal info** — names, emails, phone numbers, addresses
- **Emotional/venting content** — frustration, personal struggles
- **Code** — only roast natural language, never code snippets
- **Private conversations** — anything not meant for an AI coach

When in doubt, skip the passage.

## Scoring Axes

| Axis | What it measures |
|------|-----------------|
| Detection | How many problems the user found in Phase 1 (the detective skill) |
| Compression | How much waste was cut in the rewrite |
| Precision | Did vague words become specific? Did hedges become assertions? |
| Naturalness | Does the rewrite read like something a human would say? |

## Post-Session

After scoring: save to history.json, update XP, then:

> "🔥 Want crime scene #2? Or back to work."
