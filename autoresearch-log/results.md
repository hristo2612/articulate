# Autoresearch Results Log

## Phase 1 Config (iterations 0-20)
- Goal: Make /articulate fascinating, visually polished, and genuinely educational
- Scope: skills/articulate/**/* + hooks/session-start
- Metric: Fascination (0-25) + Teaching Quality (0-25) + Visual Polish (0-25) = 0-75
- Direction: Higher is better
- Guard: SKILL.md < 400 lines
- Iterations: 20
- Final Score: 73/75

## Phase 1 Results

| # | Change | Fascination | Teaching | Visual | Total | Verdict |
|---|--------|-------------|----------|--------|-------|---------|
| 0 | Baseline | 21 | 19 | 19 | 59 | — |
| 10 | All improvements combined | 25 | 24 | 23 | 72 | Best |
| 20 | Final test | 25 | 25 | 23 | 73 | Final |

---

## Phase 2 Config (iterations 21-30) — RADICAL REBUILD
- Goal: Radically reimagine the skill using science-backed learning methods
- Approach: Replace everything. No sacred cows. Test completely different pedagogies.
- Scope: skills/articulate/**/* + hooks/session-start
- Metric: Active Learning (0-25) + Stickiness (0-25) + Practical Transfer (0-25) + Delight (0-25) = 0-100
- Direction: Higher is better
- Guard: SKILL.md < 400 lines
- Iterations: 10
- Test: Fresh state each run, English only, claude -p simulation

### Science-Backed Methods Tested
- **Productive failure** — struggle first, instruction after (Kapur, 2008)
- **Contrastive analysis** — comparing examples forces deep processing
- **Elaborative interrogation** — "WHY does this work?" (Pressley et al., 1987)
- **Protégé effect** — teaching others is strongest learning (Biswas et al., 2005)
- **Reverse engineering** — analyzing expert work builds patterns (Chi et al., 1989)
- **Testing effect** — retrieval practice > re-studying (Roediger & Karpicke, 2006)
- **Spacing effect** — spaced retrieval for long-term retention (Ebbinghaus, 1885)
- **Interleaving** — mixing formats > repeating one (Rohrer & Taylor, 2007)

## Phase 2 Results

| # | Approach | Active | Sticky | Transfer | Delight | Total | Verdict |
|---|----------|--------|--------|----------|---------|-------|---------|
| 20 | Baseline (old format) | 14 | 15 | 13 | 18 | 60 | — |
| 21 | Productive failure (flip the flow) | 23 | 21 | 23 | 21 | 88 | ✓ Keep |
| 22 | + Contrastive analysis | 23 | 22 | 24 | 21 | 90 | ✓ Keep |
| 23 | + Elaborative interrogation | 24 | 23 | 24 | 21 | 92 | ✓ Keep |
| 24 | Roast as detective game | 24 | 22 | 23 | 23 | 92 | ✓ Keep |
| 25 | Protégé effect, tighten to 2 responses | 24 | 23 | 24 | 23 | 94 | ✓ Keep |
| 26 | Format B: reverse engineering rotation | 22 | 24 | 24 | 24 | 94 | ✓ Keep |
| 27 | Format C: micro-sessions (The Snap) | 20 | 21 | 23 | 22 | 86 | ✓ Keep (variety) |
| 28 | Spaced retrieval after sessions | 24 | 24 | 24 | 23 | 95 | ✓ Keep |
| 29 | Callbacks + personality polish | 24 | 25 | 25 | 22 | 96 | ✓ Keep |
| **30** | **Final integration test** | **25** | **25** | **25** | **22** | **97** | **🏆 Best** |

### Key Insights

1. **Productive failure was the biggest single improvement** (+28 points). Flipping from "teach then practice" to "practice then teach" fundamentally changed the learning dynamic.

2. **The protégé effect outperformed elaborative interrogation.** "Teach a junior dev" is more engaging and produces deeper explanations than "explain WHY to yourself."

3. **Format rotation prevents habituation.** Three formats (Challenge, Reverse, Snap) keep the experience fresh. The Snap format scores lower individually but adds essential variety.

4. **Callbacks create continuity.** Referencing previous sessions ("Remember when you learned 'break'?") makes the skill feel like an ongoing relationship, not isolated events.

5. **Spaced retrieval is the compound interest of learning.** One quick quiz after each session, targeting words from 2-7 days ago. Simple to implement, massive long-term impact.

6. **The detective roast mode is more engaging than passive flagging.** "Find the weaknesses yourself" activates deeper processing and feels like a game, not a lecture.

7. **Delight plateaus around 22-23.** Session length is the ceiling — the sessions are dense and educational, but ~3-5 minutes is the upper limit before fatigue sets in.

### What Changed From Phase 1

| Aspect | Phase 1 (old) | Phase 2 (new) |
|--------|--------------|---------------|
| Flow | Teach → Practice | Practice → Struggle → Discover → Retry |
| Scenarios | Artificial sentences | Real professional tasks (PR titles, Slack messages, feedback) |
| Exercise types | 6 types, disconnected | Built into the scenario — the exercise IS the scenario |
| Roast mode | Passive flagging | Detective game (find weaknesses yourself) |
| Session formats | 1 format | 3 rotating formats (Challenge, Reverse, Snap) |
| Retention | None | Spaced retrieval quiz after every session |
| Continuity | None | Callbacks to previous sessions |
| Scoring | After learning only | Before AND after (improvement delta is the feedback) |
| Science basis | None cited | 8 research-backed methods cited |

---

## Phase 3 Config (iterations 31-40) — MISSION SYSTEM
- Goal: Make /articulate short, surprising, personalized, and genuinely fun
- Problem: Phase 2 was too long and wordy. Archaeology sessions were 50-80 lines. Boring walls of text.
- Approach: Drop archaeology. Replace with 6 short mission types. Max 8 lines per challenge. Personalized from user's real writing.
- Scope: skills/articulate/**/*
- Metric: Brevity (0-25) + Surprise (0-25) + Teaching (0-25) + Fun (0-25) = 0-100
- Direction: Higher is better
- Guard: SKILL.md < 400 lines
- Iterations: 10

### The Six Missions
- **🎯 Swap** — Replace one bold weak word. One word answer.
- **✂️ Trim** — Cut a bloated sentence in half.
- **💪 Punch** — Make a flat sentence hit harder.
- **🔍 Snipe** — Fix N problems in your own real writing.
- **🔄 Flip** — Rewrite in opposite tone (casual↔formal).
- **🧩 Fill** — One blank, one perfect word.

## Phase 3 Results

| # | Change | Brevity | Surprise | Teaching | Fun | Total | Verdict |
|---|--------|---------|----------|----------|-----|-------|---------|
| 30 | Baseline (Phase 2 archaeology) | 12 | 10 | 15 | 10 | 47 | — |
| 31 | Radical rewrite to mission system | 22 | 19 | 20 | 20 | 81 | ✓ Keep |
| 32 | Opening hooks + surprise teaching | 21 | 22 | 23 | 22 | 88 | ✓ Keep |
| 33 | Back-and-forth + Quick Tap | 22 | 22 | 24 | 23 | 91 | ✓ Keep |
| 34 | Simplify roast, honest bad feedback | 23 | 22 | 23 | 24 | 92 | ✓ Keep |
| 35 | Opener variety + surprise twists | 22 | 25 | 24 | 25 | 96 | ✓ Keep |
| 36 | Simplify jargon (register→tone) | 24 | 20 | 21 | 22 | 87 | ✓ Keep (first-run) |
| 37 | Callbacks + milestones | 20 | 24 | 25 | 24 | 93 | ✓ Keep |
| 38 | Context-aware integration | 23 | 23 | 24 | 24 | 94 | ✓ Keep |
| 39 | Consistency pass (stale refs) | — | — | — | — | — | Cleanup |
| **40** | **Final integration test** | **22** | **25** | **25** | **25** | **97** | **🏆 Best** |

### Key Insights

1. **Brevity was the #1 improvement.** Phase 2 sessions ran 50-80 lines. Phase 3 sessions run 15-25. Shorter = more fun, more likely to be used again.

2. **6 mission types > 3 formats.** More variety means the user never knows what's coming. The "I'm Feeling Lucky" factor keeps sessions fresh.

3. **Surprise twists prevent habituation.** Blind Punch, Reverse Swap, Speed Trim — showing up ~10% of the time, these curveballs keep even veteran users engaged.

4. **Quick Tap creates the back-and-forth.** A 5-second follow-up after the main mission makes it feel like a conversation, not a quiz. Builds on the same principle for reinforcement.

5. **Honest bad feedback is more engaging than gentle bad feedback.** "That landed flat." creates motivation to try again. Sugar-coating creates indifference.

6. **Opening hooks > headings.** "Your words, under the microscope:" is more engaging than "## 🔍 Snipe". The hook creates curiosity before the challenge.

7. **"Tone" > "register".** Simpler words for linguistic concepts make the skill accessible to non-linguists. The teaching stays deep; the labels stay simple.

8. **One teaching point > etymology lecture.** A single "wait, really?" moment sticks better than a paragraph of origins. "'Decide' literally means 'to cut off'" > a 200-word etymology story.

### What Changed From Phase 2

| Aspect | Phase 2 (old) | Phase 3 (new) |
|--------|--------------|---------------|
| Core experience | Word Archaeology (3 formats) | 6 Mission types + surprise twists |
| Session length | 50-80 lines | 15-25 lines |
| Challenge length | 15-20 lines | 3-8 lines |
| Teaching | Etymology stories (4-8 lines) | One-line "wait really?" moments |
| Back-and-forth | Teach-back + rewrite | Quick Tap (5-sec follow-up) |
| Personalization | Generic scenarios | From user's real writing + project context |
| Bad feedback | Constructive but gentle | Direct and honest |
| Variety | 3 rotating formats | 6 missions + surprise twists |
| Jargon | "Register", "contrastive analysis" | "Tone", plain language |
| Science citations | Inline "(Kapur, 2008)" | None visible (science informs design, not UI) |
