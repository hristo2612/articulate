# Roast Mode

Scans the user's real writing, finds weak spots, and challenges them to do better.

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

## What to Find

Rank passages by weakness density. Target these patterns:

| # | Pattern | Emoji | Example |
|---|---------|-------|---------|
| 1 | Hedge stacking | 🟡 | "I think maybe we could possibly..." |
| 2 | Vague noun avalanches | 🔴 | "the thing with the stuff in the something" |
| 3 | Filler word bloat | 🟡 | "basically", "literally", "just", "really", "actually" |
| 4 | Weak verb chains | 🔴 | "make it do the thing" instead of a precise verb |
| 5 | Register confusion | 🟠 | Mixing casual slang into formal requests or vice versa |

## Presentation Format

```markdown
## 🔥 Roast: Your Writing, {timeframe}

I found this:

> "{the offending passage, quoted exactly}"

That's **{N} words** for a **{M}-word message**. Let me count:
- 🟡 "{hedge}" — hedge
- 🔴 "{vague phrase}" — vague
- 🟡 "{filler}" — filler
...

### ✏️ Rewrite challenge
Say what you actually mean. Max {N} words.

>
```

Where `{N}` in the word limit = the essential content words (strip all waste, that's the target).

## Full Example

```markdown
## 🔥 Roast: Your Writing, last 7 days

I found this:

> "I think we should maybe try to basically refactor the thing that handles the stuff for the user authentication part of the system."

That's **23 words** for a **6-word job**. Let me count:
- 🟡 "I think" — hedge
- 🟡 "maybe" — hedge
- 🟡 "try to" — hedge
- 🟡 "basically" — filler
- 🔴 "the thing that handles the stuff" — vague noun avalanche
- 🟠 "part of the system" — padding

**6 weaknesses** in one sentence. That's impressive (not the good kind).

### ✏️ Rewrite challenge
Say what you actually mean. Max 8 words.

>
```

**Gold standard answer:** "Refactor the auth handler." (4 words)

## Scoring

**Feedback format (after user rewrites):**

1. **React first** — genuine reaction: "Now THAT has a spine." or "Better, but you're still hedging."
2. **Before/After comparison:**
   ```
   **Before:** ~90 words, 10 weaknesses
   **After:**  ~12 words, 0 weaknesses
   📉 **87% compression** — that's a gut renovation.
   ```
3. **Score with axis bars:**
   ```
   **Score: 85/100**
   ├─ ✓ Compression:   23/25
   ├─ ✓ Weaknesses:    25/25  ← all 10 eliminated
   ├─ ✓ Precision:     20/25
   └─ ✓ Naturalness:   17/25  ← reads a bit robotic
   ```
4. **Gold standard** — show the ideal version, explain in 1-2 bullets why it works
5. **What you nailed / What to watch** — specific, not generic

| Axis | What it measures |
|------|-----------------|
| Compression | How much waste was cut. Higher ratio = higher score |
| Weakness Elimination | How many flagged weaknesses were removed |
| Precision Gain | Did vague words become specific? Did hedges become assertions? |
| Naturalness | Does it still read like something a human would say? |

## Multi-Round Flow

1. Find **3** weak passages from the source material
2. Present the **worst** one first
3. After scoring the rewrite, offer: "Want the other 2?"
4. If yes, present the second, then third

## Privacy Rules

These are non-negotiable. NEVER surface:

- **Credentials** — API keys, tokens, passwords, secrets
- **Personal info** — names, emails, phone numbers, addresses
- **Emotional/venting content** — frustration, personal struggles, complaints about people
- **Code** — only roast natural language, never code snippets
- **Private conversations** — anything that looks like it wasn't meant for an AI coach

When in doubt, skip the passage and pick the next one.

## Post-Session

After scoring: save to history.json, update XP, then:

> "Want the other 2? Or back to work."
