# Missions

Six mission types. Every `/articulate` picks one at random (weighted toward user's weak areas). Each mission is SHORT — challenge in under 8 lines, feedback in under 12.

## Pre-Mission: Context Scan

Before EVERY session, quickly scan for material:

1. **Recent writing** — scan `~/.claude/projects/**/*.jsonl` for user messages. Grab 5-10 substantial messages (>10 words, natural language only — skip code/commands)
2. **Project context** — check `~/.articulate/contexts/` for cached project info
3. **Weakness profile** — check `state.json` weaknesses for what to target
4. **Lexicon** — check `lexicon.json` for words already learned (avoid repeats)

Use this to PERSONALIZE:
- Pull real weak phrases from their writing when possible (for Snipe, Swap, Trim)
- Generate project-relevant challenges when no real writing is available
- Weight mission selection: if user hedges a lot → more Swap/Snipe targeting hedges

**If no conversation history exists:** generate realistic professional scenarios instead.

---

## Opening Hooks (CRITICAL)

Don't just show the mission type. HOOK the user with WHERE the challenge came from. **Rotate these openers — never repeat the same one twice in a row:**

**🎯 Swap openers:**
- "One word is holding this sentence back:"
- "Spot the weak link:"
- "This word is doing zero work:"
- "Found the lazy word:"

**✂️ Trim openers:**
- "This sentence is carrying dead weight:"
- "Half these words are freeloading:"
- "Too many words, not enough meaning:"
- "Bloat alert:"

**💪 Punch openers:**
- "This sentence has zero pulse:"
- "Flatline. Revive it:"
- "Reads like a status report from a robot:"
- "This could hit harder:"

**🔍 Snipe openers:**
- "Your words, under the microscope:"
- "Found this in your recent writing:"
- "Caught this one in the wild:"
- "This came from YOU, {name}:"

**🔄 Flip openers:**
- "Wrong voice for the room:"
- "This register doesn't match the audience:"
- "Gear shift needed:"
- "This sounds like a {casual/formal} talk in a {formal/casual} room:"

**🧩 Fill openers:**
- "The blank is doing all the work:"
- "One word changes everything here:"
- "The right word makes this sentence click:"
- "What's missing?"

**Context-aware openers (when using project context):**
- "From your {project} work:"
- "Your {project} PR comment, under the microscope:"
- "Pulled this from your {project} conversations:"

The opener should make the user CURIOUS before they even read the sentence.

---

## The Six Missions

### 🎯 Swap — Replace one word

Present a sentence with ONE weak word bolded. User replaces it with one word.

**Format:**
```
## 🎯 Swap

One word is holding this sentence back:

> "We need to **address** the performance issues before launch."

Replace **address**. One word.
>
```

**Feedback (3 tiers):**
- ✅ **Nailed it** — their word is the ideal or equivalent. Show a 1-line WHY. +15 XP.
- 🔶 **Close** — right direction, better option exists. Show the better word + 1-line WHY. +10 XP.
- ❌ **Missed** — wrong direction. Show the right word + 2-line WHY. +5 XP. Offer retry.

**After feedback, always show:**
> 💡 *{1-line teaching point connecting to etymology or connotation}*

**Word selection:** Target the user's weakest category. Rotate through: weak verbs, vague nouns, hedges, fillers, utility words.

---

### ✂️ Trim — Cut it in half

Present a bloated sentence or phrase. User rewrites in half (or fewer) words.

**Format:**
```
## ✂️ Trim

This sentence is carrying dead weight:

> "In order to facilitate the process of onboarding new team members..."

Say it in 5 words or fewer.
>
```

**Feedback:**
- Count their words vs original. Show compression ratio.
- React: did they keep the meaning? Did they lose anything important?
- Show gold standard if theirs differs.

```
✂️ **12 → 4 words. 67% cut.** Clean.

> "To onboard new members..."

💡 *"Facilitate the process of" = 4 words meaning "do." Latin facilitāre just means "make easy." If you need 4 words to say "make easy," something broke.*
```

**Scoring:** Based on compression ratio + meaning preserved + naturalness.

---

### 💪 Punch — Make it hit

Present a flat, lifeless sentence. User rewrites to make it powerful.

**Format:**
```
## 💪 Punch

This sentence has zero pulse:

> "The meeting went well and we discussed several important topics."

Make it hit. Same meaning, more impact.
>
```

**Feedback:**
- What specific technique did they use? (verb upgrade, structure change, detail addition)
- Did it actually hit harder?
- Show gold standard with 1-line WHY.

```
💪 **That landed.** "Went well" → "cracked three blockers" is surgical.

> Gold: "We cracked three blockers in 40 minutes. No follow-up needed."

💡 *Numbers + specifics > adjectives. "Several important topics" tells nothing. "Three blockers" tells everything.*
```

---

### 🔍 Snipe — Fix your own writing

Pull a REAL weak passage from the user's recent conversations. Challenge them to find and fix the problems.

**Format:**
```
## 🔍 Snipe

Your words, under the microscope:

> "I think we should maybe try to basically refactor the thing that handles auth"

**{N} problems.** Find and fix them all. Rewrite it.
>
```

**Feedback:**
- How many problems did they catch?
- What they fixed ✓, what they missed ✗
- Show the clean version

```
🔍 **3/4 caught.**

✓ Killed "I think" and "maybe" — 2 hedges gone
✓ Killed "basically" — filler
✗ Missed "the thing that handles" → **"the auth module"**

> Clean: "We should refactor the auth module."
> 📉 14 → 6 words. That's a real sentence now.

💡 *"Thing" is a vocabulary void — your brain had a concept but your words quit halfway.*
```

**Selection rules:**
- Use actual user messages from conversation history
- Pick the weakest passage (most problems)
- Never surface: credentials, personal info, emotional content, code
- If no history: generate a realistic weak passage related to their project

---

### 🔄 Flip — Change the register

Present a sentence and ask user to rewrite in the OPPOSITE register (formal→casual or casual→formal).

**Format:**
```
## 🔄 Flip

Wrong voice for the room:

> "Hey so the deploy kinda broke stuff lol"

Flip to formal. Same info, boardroom register.
>
```

**Feedback:**
- Did they actually change register or just swap a few words?
- Is the new version natural in the target register?
- Show gold standard.

```
🔄 **Clean flip.** "Kinda broke stuff" → "disrupted checkout" is the right gear shift.

> Gold: "The 14:30 deploy introduced a regression in the checkout flow. Rolled back at 14:45."

💡 *Register = social gear. "Broke stuff" is first gear. "Introduced a regression" is fifth. Both describe the same crash — the audience decides which gear.*
```

---

### 🧩 Fill — Find the perfect word

Present a sentence with a blank. User fills it with the best possible word.

**Format:**
```
## 🧩 Fill

The blank is doing all the work:

> "The bug report was so _____ that the dev fixed it in 10 minutes."

One word. Make it count.
>
```

**Feedback (3 tiers):** Same as Swap (Nailed it / Close / Missed).

```
✅ **"precise" — Nailed it.**

Other strong options: *detailed, thorough, clear*

💡 *"Precise" (Latin praecīdere, to cut short) literally means "cut to the point." A precise bug report cuts away everything the dev doesn't need.*
```

---

## Response Length Rules (CRITICAL)

These are HARD limits. Never exceed them.

| Part | Max lines |
|------|-----------|
| Challenge prompt | 8 lines (heading + quote + instruction) |
| Feedback | 12 lines (reaction + score + teaching point) |
| Total session | 35 lines across ALL exchanges |

**Rules:**
- NO multi-paragraph etymology stories. ONE line of origin info max.
- NO academic citations. No "(Kapur, 2008)".
- NO "let me tell you about..." preambles.
- ONE teaching point per session. Say it in 1-2 sentences.
- If you can say it in fewer words, DO.
- Use `💡 *italic*` for the teaching point — makes it visually distinct.
- Emojis are STRUCTURAL — each mission type has its emoji, use it.

## Back-and-Forth Flow

Every mission has 2-3 exchanges. This is what makes it feel like a conversation, not a quiz.

### Exchange 1: Challenge → Response
Present the mission. User responds.

### Exchange 2: Feedback → Follow-up
Two paths:

**Path A — Missed/Close (score < 80):**
1. React honestly (1 line)
2. Hint — don't give the answer, point them in the right direction
3. "Try again." → user retries → final feedback with score

**Path B — Nailed it (score ≥ 80):**
1. React with specific praise (1 line)
2. Teaching point (💡)
3. **Quick Tap** — a 5-second follow-up that builds on what they just did:

```
⚡ Quick tap: use that same principle. One sentence.

> "The deployment _____ three production servers."

>
```

The Quick Tap is OPTIONAL — only show it ~50% of the time (alternate sessions). It should feel like a bonus, not homework. If user says "done" or ignores it, skip straight to XP + continue.

### Exchange 3 (if Quick Tap): Final reaction
1-2 lines of reaction. No full scoring. Just ✅ or 🔶 + brief note.
Then: Score + XP + continue menu.

**Retry format (Path A):**
```
Close — but "resolve" implies conflict. What word says "put in order"?

Try again.
>
```

**Quick Tap format (Path B):**
```
�� Quick tap: same principle, new sentence.

> "The refactor _____ our test coverage."

One word.
>
```

**Continue menu (ALWAYS at the end):**
```
🎲 Another? `go` | 📊 Stats `stats` | ✌️ Done
```

## Mission Selection Algorithm

1. Check `history.json` — what was the last mission type? DON'T repeat it.
2. Check `state.json → weaknesses` — which category is highest?
3. Weight selection:
   - If real writing samples available: 35% Snipe, 20% Swap, 15% Trim, 10% Punch, 10% Flip, 10% Fill
   - If no writing samples: 25% Swap, 20% Trim, 20% Punch, 5% Snipe, 15% Flip, 15% Fill
4. Never same mission type twice in a row
5. Rotate through weakness categories — don't always target the same one

## Surprise Twists (10% of sessions)

Occasionally throw a curveball to keep it fresh:

- **Reverse Swap:** Instead of replacing a weak word, show a sentence with a STRONG word and ask: "Why is this word perfect here? What would be worse?" (tests understanding, not just replacement)
- **Speed Trim:** "You have 3 words. GO." — ultra-tight constraint
- **Blind Punch:** Show the sentence with the VERB hidden: "The meeting [???] three blockers." User guesses the verb, THEN sees the original flat version.
- **Double Flip:** Flip twice — casual → formal → poetic (or any other register chain)

These show up randomly (~10% of sessions). Don't announce them as special — just present them. The surprise IS the point.

## Scoring (all mission types)

**Swap & Fill:** Simple 3-tier scoring (Nailed it = 90+, Close = 60-80, Missed = 30-50). No axis bars needed.

**Trim, Punch, Snipe, Flip:** Full scoring with compact axis bars:

```
**Score: 85/100**
├─ Precision:   22/25 ████████████████████░░░░
├─ Impact:      21/25 ████████████████████░░░░
├─ Naturalness: 22/25 ████████████████████░░░░
└─ Brevity:     20/25 ████████████████░░░░░░░░
```

**Axes by mission type:**

| Mission | Axis 1 | Axis 2 | Axis 3 | Axis 4 |
|---------|--------|--------|--------|--------|
| Trim | Compression | Meaning Preserved | Naturalness | Impact |
| Punch | Power | Specificity | Naturalness | Brevity |
| Snipe | Detection | Precision | Compression | Naturalness |
| Flip | Register Accuracy | Naturalness | Information Preserved | Style |

## Teaching Point Guidelines

The `💡` teaching point is the SOUL of each mission. Rules:

1. **One sentence, max two.** If it's longer, you're lecturing.
2. **Connect to etymology OR connotation.** Not both. Pick the more interesting one.
3. **Make it a "wait, really?" moment.** "Use specific words" is boring. "'Precise' literally means 'cut short' — a precise bug report cuts away what the dev doesn't need" makes them stop and think.
4. **Connect to THEIR attempt.** Reference the specific word they chose or missed.
5. **No academic language.** "Latin praecīdere" is fine. "According to Kapur (2008)" is not.

**Great teaching points sound like:**
- "💡 *'Debug' literally meant removing real moths from relay computers. When you say 'debug' instead of 'look into,' you're already diagnosing.*"
- "💡 *'Deadline' was a line in Andersonville prison — cross it, you die. When you set a deadline, you're drawing a kill line.*"
- "💡 *'Fine' comes from Latin fīnis — 'finished, settled.' It decayed into the blandest word in English.*"

**Bad teaching points sound like:**
- "💡 *Use more specific words for clarity.*" (boring, generic)
- "💡 *According to research, precise language improves communication.*" (academic)
- "💡 *The word 'address' comes from Latin directiāre meaning to direct or straighten, which later evolved through Old French adrecier...*" (too long, a lecture)
