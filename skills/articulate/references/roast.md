# Roast Mode — The Detective Game

Your real writing → find the problems yourself → rewrite. Same brevity rules as missions.

## Source Scanning

### `roast` — scan past conversations
1. `~/.claude/projects/**/*.jsonl` — user messages with `"type": "user"`
2. `~/.codex/history.jsonl` — text in `text` field
3. `~/.codex/archived_sessions/*.jsonl` — older sessions

### `roast here` — current conversation only

### Rules
- Grab 20-30 substantial user messages (>10 words, natural language only)
- Skip: one-word answers, file paths, CLI commands, code
- Sort by weakness density (most problems first)
- Find **3** weak passages, present the worst first

## The Flow

### Phase 1: Crime Scene (MAX 8 lines)

```
## 🔥 Roast

Your words. My microscope.

> "I think we should maybe try to basically refactor the thing that handles the stuff for auth"

**{N} problems.** Find them all. Rewrite it.
>
```

Don't reveal the problems. Don't hint. Let them hunt.

### Phase 2: Verdict (MAX 12 lines)

```
🔥 **{caught}/{total}**

✓ "I think" — hedge gone
✓ "basically" — filler gone
✗ "the thing that handles the stuff" — name it: **"the auth middleware"**
✗ "try to" — another hedge hiding in plain sight

> Clean: "Refactor the auth middleware."
> 📉 16 → 4 words. That's a sentence now.

💡 *"Thing" (Old Norse þing) originally meant a public assembly. You're accidentally calling every object a Viking parliament.*

⚡ +24 XP (base 10 + score 7 + streak 7) | 🔥 4d
```

### Phase 3: More?

```
🔥 Crime scene #2? `more` | 📊 Stats `stats` | ✌️ Done
```

Offer up to 3 crime scenes. Worst first.

## Weakness Patterns

| # | Pattern | Emoji | One-liner |
|---|---------|-------|-----------|
| 1 | Hedge stacking | 🟡 | "Every hedge is an apology for having an opinion." |
| 2 | Vague nouns | 🔴 | "'Thing' — your brain had a concept but your words quit halfway." |
| 3 | Filler bloat | 🟡 | "Fillers are verbal throat-clearing." |
| 4 | Weak verbs | 🔴 | "'Make' and 'do' work anywhere, which means they mean nothing." |
| 5 | Tone confusion | 🟠 | "Mixing 'gonna' with 'pursuant to' = two people arguing in one email." |
| 6 | Buried action | 🟠 | "If your reader excavates your request from paragraph 3, you're hiding." |
| 7 | Passive deflection | 🟡 | "'It was decided' = leaving the room before anyone asks who decided." |

## Scoring

```
**Score: {n}/100**
├─ Detection:    {n}/25 (problems you spotted)
├─ Compression:  {n}/25 (waste cut)
├─ Precision:    {n}/25 (vague → specific)
└─ Naturalness:  {n}/25 (reads like a human)
```

## Privacy — Non-negotiable

NEVER surface: credentials, API keys, personal info, emotional/venting content, code.
When in doubt, skip the passage.
