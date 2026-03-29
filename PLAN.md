# Articulate — Master Build Plan

> **Purpose:** Central reference for all agents working on this project. Every file, every decision, every detail lives here. When in doubt, come back to this document.

## Architecture Decisions (Locked)

| Decision | Choice | Rationale |
|----------|--------|-----------|
| Format | Plugin (not bare skill) | Supports Claude Code, Codex, Cursor, OpenCode, Gemini CLI |
| User state location | `~/.articulate/` | Platform-agnostic, survives updates, works on macOS/Linux/Windows |
| Skill content location | `skills/articulate/` inside repo | Shipped with plugin, read-only at runtime |
| Cross-platform strategy | Platform-agnostic skills + platform-specific metadata dirs | Proven by obra/superpowers |
| SKILL.md token budget | <500 lines | Heavy content in reference files, loaded on demand |
| Description field | Trigger conditions only | Prevents Claude from summarizing instead of reading full skill (CSO) |
| State path in SKILL.md | `~/.articulate/` (literal) | Every AI agent resolves `~` to home dir; no platform-specific variables |

## Directory Structure

```
articulate/                              ← Git repo root
├── .claude-plugin/
│   └── plugin.json                      ← Claude Code plugin metadata
├── .codex/
│   └── INSTALL.md                       ← Codex manual install instructions
├── .cursor-plugin/
│   └── plugin.json                      ← Cursor plugin metadata
├── .opencode/
│   └── INSTALL.md                       ← OpenCode install instructions
├── gemini-extension.json                ← Gemini CLI manifest
├── GEMINI.md                            ← Gemini CLI context injection
├── hooks/
│   ├── hooks.json                       ← Claude Code hook config
│   ├── hooks-cursor.json                ← Cursor hook config
│   ├── session-start                    ← Bash hook script (macOS/Linux)
│   └── run-hook.cmd                     ← Polyglot wrapper (Windows support)
├── skills/
│   └── articulate/
│       ├── SKILL.md                     ← Core routing + session logic
│       ├── references/
│       │   ├── missions/
│       │   │   ├── rewrite.md
│       │   │   ├── fill.md
│       │   │   ├── prompt.md
│       │   │   ├── scenario.md
│       │   │   ├── boss.md
│       │   │   └── review.md
│       │   ├── progression/
│       │   │   ├── levels.md
│       │   │   ├── scoring.md
│       │   │   ├── engagement.md
│       │   │   └── weaknesses.md
│       │   ├── languages/
│       │   │   ├── english.md
│       │   │   └── bulgarian.md
│       │   ├── onboarding.md
│       │   ├── context-aware.md
│       │   └── style.md
│       └── templates/
│           ├── rewrite-bank.md
│           ├── fill-bank.md
│           ├── prompt-bank.md
│           ├── scenario-bank.md
│           └── boss-bank.md
├── .gitignore
├── LICENSE                              ← MIT
└── README.md
```

**Runtime user state (NOT in repo, created on first run):**
```
~/.articulate/
├── user.json
├── state.json
├── history.json
├── lexicon.json
└── contexts/
    └── {project-name}.json
```

---

## Phase 0: Project Scaffolding

**Depends on:** Nothing
**Can parallelize with:** Nothing (must be first)

### 0.1 — Initialize git repo at `/Users/hristo/Projects/Articulate`

```bash
git init
```

### 0.2 — Create directory structure

```bash
mkdir -p .claude-plugin .codex .cursor-plugin .opencode hooks
mkdir -p skills/articulate/references/missions
mkdir -p skills/articulate/references/progression
mkdir -p skills/articulate/references/languages
mkdir -p skills/articulate/templates
```

### 0.3 — .gitignore

```gitignore
# OS
.DS_Store
Thumbs.db

# Editors
*.swp
*.swo
*~
.vscode/
.idea/

# Node (if we ever add tooling)
node_modules/

# User state is at ~/.articulate/, not in this repo.
# Nothing to ignore for data — it doesn't live here.
```

### 0.4 — LICENSE (MIT)

Standard MIT license. Copyright 2026 Hristo Bogoev.

---

## Phase 1: Platform Metadata

**Depends on:** Phase 0
**Can parallelize with:** Phase 2, 3, 4, 5, 6 (all independent of each other)

### 1.1 — `.claude-plugin/plugin.json`

```json
{
  "name": "articulate",
  "description": "Precision language training skill — gamified vocabulary coaching in your terminal",
  "version": "1.0.0",
  "author": {
    "name": "Hristo"
  },
  "homepage": "https://github.com/hristo2612/articulate",
  "repository": "https://github.com/hristo2612/articulate",
  "license": "MIT",
  "keywords": [
    "vocabulary",
    "language",
    "training",
    "writing",
    "skill"
  ]
}
```


### 1.2 — `.codex/INSTALL.md`

Instructions for manual Codex installation:
```bash
git clone https://github.com/hristo2612/articulate.git ~/.codex/articulate
ln -s ~/.codex/articulate/skills ~/.agents/skills/articulate
```

Explain that Codex discovers skills by scanning `~/.agents/skills/` at startup and parsing SKILL.md frontmatter. No hooks needed — Codex loads skills natively.

### 1.3 — `.cursor-plugin/plugin.json`

Same structure as Claude Code but points to `hooks/hooks-cursor.json`:
```json
{
  "name": "articulate",
  "description": "Precision language training skill — gamified vocabulary coaching in your terminal",
  "version": "1.0.0",
  "hooks": "hooks/hooks-cursor.json"
}
```

### 1.4 — `.opencode/INSTALL.md`

Instructions for OpenCode plugin installation. Add to `opencode.json`:
```json
{"plugin": ["articulate@git+https://github.com/hristo2612/articulate.git"]}
```

### 1.5 — `gemini-extension.json`

Gemini CLI manifest pointing to GEMINI.md:
```json
{
  "name": "articulate",
  "version": "1.0.0",
  "description": "Precision language training skill",
  "context_file": "GEMINI.md"
}
```

### 1.6 — `GEMINI.md`

Context file for Gemini CLI. Contains:
- Brief intro to the articulate skill
- Tool mapping table (Gemini equivalents for Read, Write, Edit, Bash)
- Instruction to use `activate_skill` to load the articulate skill
- Reference to the skill directory

### 1.7 — `hooks/hooks.json` (Claude Code)

```json
{
  "hooks": {
    "SessionStart": [
      {
        "type": "command",
        "command": "bash \"$CLAUDE_PLUGIN_ROOT/hooks/session-start\""
      }
    ]
  }
}
```

### 1.8 — `hooks/hooks-cursor.json` (Cursor)

```json
{
  "version": 1,
  "hooks": {
    "sessionStart": [
      {
        "type": "command",
        "command": "bash \"$CURSOR_PLUGIN_ROOT/hooks/session-start\""
      }
    ]
  }
}
```

### 1.9 — `hooks/session-start` (Bash script)

Purpose: On session start, check if user has an active streak at risk and inject a gentle reminder into the session context. This is OPTIONAL — Articulate works fine without it. The reminder is a nice-to-have for retention.

Logic:
1. Detect platform (`CURSOR_PLUGIN_ROOT` vs `CLAUDE_PLUGIN_ROOT`)
2. Check if `~/.articulate/state.json` exists
3. If it does, read `lastPlayedDate` and `streak`
4. If streak > 0 and lastPlayedDate is yesterday → "Your {N}-day streak is safe. Keep it going with /articulate"
5. If streak > 0 and lastPlayedDate is older → "⚠️ Your {N}-day streak is at risk! Type /articulate to save it."
6. Output JSON with appropriate field for detected platform:
   - Claude Code: `{"hookSpecificOutput": {"hookEventName": "SessionStart", "additionalContext": "..."}}`
   - Cursor: `{"additional_context": "..."}`
7. If no state file or streak is 0, output empty/no reminder

Must handle: missing jq (graceful fallback), missing state file, date math cross-platform.

### 1.10 — `hooks/run-hook.cmd` (Windows polyglot)

Polyglot script valid in both CMD and bash (copy pattern from superpowers):
- CMD portion: finds bash (Git for Windows paths, then PATH) and delegates to `session-start`
- Bash portion: directly executes `session-start`
- Three bash search locations: `C:\Program Files\Git\bin\bash.exe`, `C:\Program Files (x86)\Git\bin\bash.exe`, `bash` on PATH

---

## Phase 2: SKILL.md (Core Routing File)

**Depends on:** Phase 0
**Can parallelize with:** Phase 1, 3, 4, 5, 6

This is the most critical file. It must be under 500 lines and handle ALL routing, session management, and state logic. Detailed mission rules, scoring, etc. live in reference files.

### Frontmatter

```yaml
---
name: articulate
description: "Use when the user invokes /articulate — precision language training skill for building active vocabulary through guided writing missions"
---
```

**Critical:** Description says WHEN to use, not WHAT it does. This prevents Claude from summarizing the skill instead of reading it.

### Content Structure (Target: ~400-450 lines)

```
1. OVERVIEW (10 lines)
   - What Articulate is (1 sentence)
   - Core principle: production over recognition
   - Session target: 5 minutes

2. STATE MANAGEMENT (40 lines)
   - All state lives at ~/.articulate/
   - File schemas (brief — point to references/progression/levels.md for full details)
   - First-run detection: check if ~/.articulate/user.json exists
   - State initialization: create ~/.articulate/ directory and default JSON files
   - Reading state: read ~/.articulate/state.json at session start
   - Writing state: write updated JSON after every mission

3. ARGUMENT ROUTING (50 lines)
   - $ARGUMENTS routing table:
     (empty) or "go"  → Default session flow (dashboard → daily word → mission)
     "rewrite"         → Jump to REWRITE mission (read references/missions/rewrite.md)
     "fill"            → Jump to FILL_PRECISION mission (read references/missions/fill.md)
     "prompt"          → Jump to PROMPT_CRAFT mission (read references/missions/prompt.md)
     "scenario"        → Jump to SCENARIO mission (read references/missions/scenario.md)
     "boss"            → Jump to BOSS mission (read references/missions/boss.md)
     "review"          → Jump to REVIEW mission (read references/missions/review.md)
     "stats"           → Show full statistics dashboard
     "badges"          → Show badge collection
     "lexicon"         → Show mastered words collection
     "radar"           → Show weakness radar
     "help"            → Show help/commands
     "quick"           → Skip dashboard, go straight to a random mission
     "menu"            → Show interactive menu of available missions
     "reset"           → Reset all progress (with confirmation)
     "config"          → Update user preferences
   - Unlock gates: check level before allowing locked mission types
     Level 1 (RECRUIT, 0 XP): rewrite, fill
     Level 2 (INITIATE, 100 XP): + prompt, review
     Level 3 (OPERATIVE, 300 XP): + scenario
     Level 4 (SPECIALIST, 600 XP): + boss
     Level 5 (COMMANDER, 1000 XP): + user-generated challenges
     Level 6 (ARCHITECT, 1800 XP): + teach mode
     Level 7 (MASTERMIND, 3000 XP): + prestige

4. FIRST-RUN FLOW (20 lines)
   - If ~/.articulate/user.json does not exist → read references/onboarding.md
   - Follow onboarding flow (asks name, languages, focus areas, etc.)
   - Create initial JSON files

5. SESSION START (50 lines)
   - Read ~/.articulate/state.json
   - Calculate streak:
     - Parse lastPlayedDate
     - If today: streak unchanged, increment todayMissionCount
     - If yesterday: streak += 1 (continuing streak)
     - If older: check streak shields, apply decay if needed, reset streak to 1
     - Handle missing/null lastPlayedDate (first ever session)
   - Display dashboard:
     - Rank badge + rank name + prestige stars
     - XP bar: current / next level threshold
     - Streak: {N} days {flame emoji scaling with streak length}
     - Today: {N} missions completed
     - If badge earned since last session, celebrate it
     - If level-up happened, show level-up banner
   - For dashboard formatting, read references/style.md

6. DAILY WORD RITUAL (20 lines)
   - Present one precision word at session start
   - Format: word, pronunciation hint, etymology, precise definition, example in context
   - Challenge: use this word in today's mission for +5 bonus XP
   - Word selection: pick from a word the user hasn't mastered yet, or a new word
   - If the user used the daily word in their mission response, award the bonus

7. MISSION DISPATCH (30 lines)
   - If specific type requested via $ARGUMENTS → dispatch to that type
   - If default session ("go" or empty):
     - Every 5th mission overall → REVIEW mission (if unlocked and eligible entries exist)
     - Otherwise: weighted random selection from unlocked types
     - Weight by weakness radar (prefer missions targeting worst weaknesses)
     - Include project context if enabled (read references/context-aware.md)
   - For each mission type, read the corresponding references/missions/{type}.md
   - That file contains full rules for generation, presentation, and evaluation

8. POST-MISSION FLOW (60 lines)
   - This runs after EVERY mission, regardless of type

   8a. SCORING
   - Each mission type has its own scoring rubric (in references/progression/scoring.md)
   - Score is 0-100

   8b. XP CALCULATION
   - Base: 10 XP
   - Score bonus: floor(score / 10)
   - Streak bonus: min(streak * 2, 20)
   - Boss multiplier: 3x (for boss missions only)
   - Critical hit: 15% random chance, if score >= 80 → 3x total XP
   - Daily word bonus: +5 if user used the daily word
   - Show XP breakdown to user

   8c. LEVEL-UP CHECK
   - XP thresholds: 0, 100, 300, 600, 1000, 1800, 3000
   - If XP crosses threshold → level up, show celebration banner
   - Show what new mission types are unlocked
   - For celebration formatting, read references/style.md

   8d. BADGE CHECK
   - Read references/progression/levels.md for badge conditions
   - Check ALL badge conditions against current state
   - If new badge earned → show badge celebration, add to earnedBadges

   8e. WEAKNESS UPDATE
   - Mission evaluation identifies weakness categories triggered
   - Increment relevant weakness counters in state.json
   - Append to weakness history for trend tracking

   8f. LEXICON UPDATE
   - Identify precision words the user successfully used
   - If word not in lexicon.json → add with mastery "seen"
   - If word exists → increment timesUsed, update mastery tier:
     Seen (1 use) → Used (2 uses) → Consistent (3 uses) → Mastered (5 uses across 2+ weeks)
   - Save updated lexicon.json

   8g. LOOT DROP CHECK (variable reward)
   - 5-10% chance after any mission
   - Drop a "precision gem" — a powerful word with full etymology, usage notes, register info
   - Add to lexicon as "seen"
   - Show the gem with special formatting

   8h. SAVE STATE
   - Update all fields in state.json
   - Append mission to history.json (keep last 100, FIFO)
   - Save lexicon.json

   8i. CONTINUE PROMPT
   - "Deploy another mission? Or save & return to base."
   - If user continues → skip dashboard, go straight to mission dispatch (step 7)
   - If user stops → show brief session summary (missions completed, XP earned, streak status)

9. STATS DASHBOARD (30 lines)
   - Full statistics view (triggered by /articulate stats)
   - Overall: total missions, total XP, rank, prestige stars
   - Per mission type: count, average score, best score
   - Streak: current, best ever, shields held
   - Weakness radar: all 6 categories with bars and trends
   - Lexicon: total words, per mastery tier counts
   - Recent performance: last 10 missions with scores
   - For formatting, read references/style.md

10. HELP (20 lines)
    - Available commands with brief descriptions
    - Current unlock status (what's available at user's level)
    - Tips for getting started

11. LANGUAGE HANDLING (15 lines)
    - Check user.json for configured languages
    - If multiple languages: alternate between them, or let user specify
    - For language-specific rules, read references/languages/{lang}.md
    - Support: /articulate rewrite --bg or /articulate rewrite --en for explicit language choice

12. CONTEXT-AWARE MISSIONS (15 lines)
    - If user.json has contextAware: true
    - Check current working directory for project signals (README, package.json, Cargo.toml, etc.)
    - Read references/context-aware.md for full context-gathering rules
    - Pass project context to mission generation
    - Cache project summary in ~/.articulate/contexts/{project-name}.json
```

### SKILL.md Critical Rules

- **Never** include full scoring rubrics, mission rules, or template content inline
- **Always** point to reference files: "For REWRITE mission rules, read references/missions/rewrite.md"
- **Always** use `~/.articulate/` for state paths (not `${CLAUDE_PLUGIN_DATA}` or relative paths)
- Keep token footprint minimal — this file loads on EVERY invocation
- Use imperative voice: "Read the file", "Calculate the streak", "Show the dashboard"

---

## Phase 3: Reference Files — Missions

**Depends on:** Phase 0
**Can parallelize with:** All other phases. Each mission file is independent of the others.

Each mission reference file must contain EVERYTHING an AI agent needs to:
1. Generate a challenge of that type
2. Present it to the user
3. Evaluate the user's response
4. Provide feedback and a gold standard
5. Identify weaknesses

### 3.1 — `references/missions/rewrite.md`

**Purpose:** Full rules for REWRITE missions.

**Content:**
- **What it is:** User receives a weak sentence with 2-4 utility/vague words. They rewrite it with precision.
- **Generation rules:**
  - Sentence should be something a developer/entrepreneur would actually write: emails, Slack messages, prompts, pitches, READMEs, customer support replies, interview answers
  - Must contain 2-4 identifiable weak words (utility words, hedging, vague nouns, weak verbs, filler words)
  - Difficulty scales with user level (see difficulty table below)
  - If context-aware: sentence relates to user's current project
  - Mark the weak words in the presented sentence (bold or highlight)
- **Difficulty scaling:**
  - RECRUIT (L1): Simple sentences, obvious weak words ("The thing is really good and nice"), basic vocabulary targets
  - INITIATE (L2): Professional context, subtler patterns ("We should probably look into getting some kind of solution for this")
  - OPERATIVE (L3): Register-switching, audience-awareness ("Basically our product does stuff that helps companies")
  - SPECIALIST (L4): Structural challenges, compound sentences with multiple weakness types
  - COMMANDER+ (L5+): Paragraph-level rewrites, nuanced professional scenarios, multi-audience
- **Presentation format:**
  ```
  ━━━ MISSION: REWRITE ✏️ ━━━━━━━━━━━━━━━━━━━━

  Rewrite this sentence with precision:

  > "The **thing** we built is **really good** and **helps** people **do stuff** faster."

  Target: Replace the highlighted weak words.
  Your rewrite:
  ```
- **Evaluation rubric (4 axes, 0-25 each, total 0-100):**
  - **Precision (0-25):** Did the user replace vague words with specific, high-information alternatives?
    - 25: Every weak word replaced with a precise, contextually perfect alternative
    - 20: Most weak words replaced well, one could be more precise
    - 15: Some precision gained, but some weak words remain or replacements are only marginally better
    - 10: Attempted but replacements are still somewhat vague
    - 5: Minimal improvement
    - 0: No meaningful change or worse
  - **Conciseness (0-25):** Is the rewrite tight? No unnecessary words?
    - 25: Every word earns its place, no filler
    - 20: Tight with perhaps one unnecessary word
    - 15: Acceptable but could be trimmed
    - 10: Added unnecessary words or padding
    - 5: Significantly more verbose than needed
    - 0: Bloated
  - **Impact (0-25):** Does the rewrite land? Is it memorable, clear, compelling?
    - 25: The sentence commands attention
    - 20: Strong and clear
    - 15: Adequate but forgettable
    - 10: Weak impact
    - 5: Confusing or bland
    - 0: Worse than the original
  - **Naturalness (0-25):** Does it sound like a real person wrote it? Not thesaurus-stuffed?
    - 25: Completely natural, fits the register
    - 20: Natural with minor awkwardness
    - 15: Slightly forced or over-written
    - 10: Sounds like someone used a thesaurus
    - 5: Awkward or unnatural
    - 0: Incomprehensible
- **Feedback format:**
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
  • "onboarding flow" → specific noun replacing "thing"
  • "shipped" → decisive verb replacing "built" (implies completion + delivery)
  • "reduces task completion time by 40%" → measurable impact replacing "helps people do stuff faster"

  WEAKNESSES DETECTED: utility_words, vague_nouns
  ```
- **Weakness mapping:** After evaluation, tag which weakness categories appeared in the ORIGINAL sentence AND which ones the user failed to fix. These feed into the weakness radar.

### 3.2 — `references/missions/fill.md`

**Purpose:** Full rules for FILL_PRECISION missions.

**Content:**
- **What it is:** A sentence with ONE word replaced by `[___]`. The missing word is precise and high-impact. User must PRODUCE the word (not pick from options).
- **Generation rules:**
  - The target word should be a precision word: specific adjective, strong verb, exact noun, or technical term
  - Sentence must provide enough context clues that the target word is deducible
  - Avoid obscure/rare words — target words should be "passive vocabulary" level (user would recognize them but might not produce them)
  - Difficulty scales: L1 = common precision words ("compelling", "streamline"), L3+ = register-specific words ("enumerate", "synthesize", "deprecate")
  - If context-aware: sentence relates to user's project domain
- **Presentation format:**
  ```
  ━━━ MISSION: FILL PRECISION 🎯 ━━━━━━━━━━━━━━

  Fill the blank with the most precise word:

  > "The API's response time was [___], often exceeding 3 seconds
  >  even for simple queries."

  Your word:
  ```
- **Scoring:**
  - Exact match: 100
  - Strong synonym (same precision, same register): 80
  - Acceptable alternative (correct meaning, less precise): 60
  - Weak but related: 30
  - Wrong / vague: 0
- **Feedback format:**
  ```
  ━━━ DEBRIEF ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

  YOUR WORD: "slow"
  TARGET: "sluggish"
  MATCH: Acceptable (60/100)

  WHY "sluggish" > "slow":
  • "slow" is a utility adjective — it states the fact but carries no texture
  • "sluggish" implies reluctance and heaviness — it suggests the system
    is laboring, not just taking time. It paints a picture.
  • Etymology: from Scandinavian "slugg" (slow-moving person)
  • Register: technical writing, performance reports, code reviews

  ALSO STRONG: "abysmal" (80) — stronger judgment, implies unacceptable
  ```

### 3.3 — `references/missions/prompt.md`

**Purpose:** Full rules for PROMPT_CRAFT missions. Unlocks at Level 2 (INITIATE, 100 XP).

**Content:**
- **What it is:** User receives a GOAL (something they'd want an LLM to do). They write the prompt.
- **Generation rules:**
  - Goals should be realistic LLM tasks: summarize, analyze, generate, compare, evaluate, draft, refactor
  - Include constraint: word limit, format, audience, tone
  - Difficulty scales: L2 = simple instructions, L4+ = multi-step prompts with constraints and examples
  - If context-aware: goal relates to user's project
- **Scoring rubric (5 axes, 0-20 each, total 0-100):**
  - Specificity: Are instructions concrete and unambiguous?
  - Constraints: Are output format, length, tone specified?
  - Structure: Is the prompt organized logically?
  - Clarity: Is the language precise, not vague?
  - Register: Is the vocabulary appropriate for prompt engineering?
- **Feedback:** Show the user's prompt, then an improved version, then explain the key differences. Focus on vocabulary choices in the prompt itself.

### 3.4 — `references/missions/scenario.md`

**Purpose:** Full rules for SCENARIO missions. Unlocks at Level 3 (OPERATIVE, 300 XP).

**Content:**
- **What it is:** A real-world professional communication challenge with full context.
- **Generation rules:**
  - Provide: situation, role, audience, goal, word limit
  - Types: cold email, investor follow-up, customer support reply, interview answer, team Slack update, PR description, technical proposal, conference talk pitch, newsletter intro, product changelog entry
  - If context-aware: scenario uses user's actual project/product
  - Difficulty scales: L3 = straightforward professional writing, L5+ = persuasion, negotiation, cross-cultural sensitivity
- **Presentation format:**
  ```
  ━━━ MISSION: SCENARIO 🎭 ━━━━━━━━━━━━━━━━━━━━

  SITUATION: A potential customer emailed asking if your API supports
  batch processing. They're evaluating you against two competitors.
  ROLE: Founder / sole developer
  AUDIENCE: Technical PM at a mid-size SaaS company
  GOAL: Confirm the feature exists, differentiate from competitors,
  and close toward a trial signup.
  WORD LIMIT: 80 words

  Your response:
  ```
- **Scoring rubric (5 axes, 0-20 each, total 0-100):**
  - Word choice: Precise, professional, no filler
  - Register: Appropriate for audience and context
  - Goal achievement: Does the response accomplish the stated goal?
  - Conciseness: Within word limit, every word earns its place
  - Persuasiveness: Does it move the audience toward the desired action?
- **Feedback:** Score, gold standard, and analysis of what worked and what didn't. Highlight specific word choices and their impact.

### 3.5 — `references/missions/boss.md`

**Purpose:** Full rules for BOSS missions. Unlocks at Level 4 (SPECIALIST, 600 XP). Once per week max.

**Content:**
- **What it is:** Multi-part challenge combining multiple skills. 3x XP multiplier.
- **Generation rules:**
  - 2-3 parts, each building on the previous
  - Example: Part 1 = write a 10-word value proposition. Part 2 = opening paragraph of a cold email using that proposition. Part 3 = rewrite for a different audience.
  - Each part scored separately, total averaged
  - Check lastBossDate in state.json — enforce once per 7 days
  - Context-aware when possible
- **Presentation format:** Multi-part with clear instructions for each part
- **Scoring:** Average of all parts, then apply 3x XP multiplier
- **Feedback:** Debrief each part individually, then overall assessment

### 3.6 — `references/missions/review.md`

**Purpose:** Full rules for REVIEW (spaced repetition) missions. Unlocks at Level 2 (INITIATE, 100 XP).

**Content:**
- **What it is:** User sees a challenge they completed 2+ weeks ago and tries again. Compares with their original response.
- **Generation rules:**
  - Pull from history.json: find entries older than 14 days
  - Prefer entries where score was < 80 (room for improvement)
  - Present the original challenge WITHOUT showing the user's previous response
  - After user submits new response, show both side-by-side
- **Scoring:** Same rubric as the original mission type
- **Feedback format:**
  ```
  ━━━ REVIEW DEBRIEF 🔄 ━━━━━━━━━━━━━━━━━━━━━━

  THEN (14 days ago):   Score: 62/100
  > "Our product is a good tool that helps companies manage their stuff better."

  NOW:                  Score: 81/100
  > "Our workflow engine eliminates manual task routing for mid-market ops teams."

  IMPROVEMENT: +19 points 📈

  KEY GAINS:
  • "workflow engine" vs "product" — specific noun
  • "eliminates" vs "helps" — decisive verb
  • "manual task routing" vs "manage their stuff" — concrete problem
  ```
- **Weakness tracking:** Compare weakness categories from original vs new attempt. If previously-detected weaknesses are absent in the new attempt, this counts as improvement.

---

## Phase 4: Reference Files — Progression

**Depends on:** Phase 0
**Can parallelize with:** All other phases. Each file is independent.

### 4.1 — `references/progression/levels.md`

**Content:**
- **Level table:** Full table with level number, rank name, XP threshold, badge emoji, and unlocks
  ```
  | Level | Rank        | XP    | Badge | Unlocks                              |
  |-------|-------------|-------|-------|--------------------------------------|
  | 1     | RECRUIT     | 0     | ⬜    | REWRITE, FILL                        |
  | 2     | INITIATE    | 100   | 🟩    | PROMPT_CRAFT, REVIEW                 |
  | 3     | OPERATIVE   | 300   | 🟨    | SCENARIO                             |
  | 4     | SPECIALIST  | 600   | 🟧    | BOSS                                 |
  | 5     | COMMANDER   | 1000  | 🔴    | User-generated challenges            |
  | 6     | ARCHITECT   | 1800  | 💎    | Teach mode                           |
  | 7     | MASTERMIND  | 3000  | 👑    | Prestige system                      |
  ```
- **Badge collection:** All 14 badges with name, emoji, unlock condition, and display format
  ```
  | Badge | Name             | Condition                              |
  |-------|------------------|----------------------------------------|
  | ⚡    | First Blood      | Complete first mission                 |
  | 🔥    | On Fire          | 3-day streak                           |
  | 💀    | Unstoppable      | 7-day streak                           |
  | 🤖    | Machine          | 30-day streak                          |
  | 🎯    | Precision Strike | Score 90+ five times                   |
  | 🏆    | Sharpshooter     | Score 90+ twenty times                 |
  | ✏️    | Rewriter         | Complete 10 rewrites                   |
  | 🎭    | Operator         | Complete 10 scenarios                  |
  | 🧠    | Prompt Engineer  | Complete 10 prompt crafts              |
  | 🎖️    | Veteran          | 50 total missions                      |
  | ⚔️    | Centurion        | 100 total missions                     |
  | 💪    | Powerhouse       | Earn 1000 XP                           |
  | 🌍    | Polyglot         | Complete missions in 2+ languages      |
  | 📈    | Improver         | Weakness radar shows measurable improve|
  ```
- **Prestige system:** After reaching MASTERMIND, option to reset to RECRUIT with a ★ marker. Each prestige run can focus on a different language or domain. Stars accumulate. XP resets, badges preserved.
- **Streak shields:** Earned at 30, 60, 100-day milestones. Max 2 held. Each shields one missed day.
- **Rank decay:** 7 consecutive inactive days → rank drops 1 level (XP preserved). 3 missions to restore.

### 4.2 — `references/progression/scoring.md`

**Content:**
- **Scoring rubrics per mission type:** Consolidated reference for all scoring rubrics
  - REWRITE: 4 axes × 25 = 100 (precision, conciseness, impact, naturalness)
  - FILL: exact=100, strong synonym=80, acceptable=60, weak=30, wrong=0
  - PROMPT_CRAFT: 5 axes × 20 = 100 (specificity, constraints, structure, clarity, register)
  - SCENARIO: 5 axes × 20 = 100 (word choice, register, goal, conciseness, persuasiveness)
  - BOSS: average of parts, scored by their respective type rubric
  - REVIEW: same rubric as original mission type
- **XP formula:**
  ```
  base = 10
  score_bonus = floor(score / 10)
  streak_bonus = min(streak × 2, 20)
  daily_word_bonus = 5 (if daily word used in response)
  subtotal = base + score_bonus + streak_bonus + daily_word_bonus

  if boss_mission: subtotal = subtotal × 3
  if critical_hit (15% chance AND score >= 80): subtotal = subtotal × 3

  total_xp = subtotal
  ```
- **Score display format:** Always show the breakdown so user understands what contributed

### 4.3 — `references/progression/engagement.md`

**Content:**
- **Variable reward mechanics:**
  - Critical Hits: 15% random per mission, score must be >= 80, results in 3x XP. Show special animation.
  - Loot Drops: 5-10% chance after any mission, drops a "precision gem" (word with etymology, usage, register). Special display.
  - Mystery Missions: Occasional creative twist challenges. Examples:
    - "Rewrite using only Anglo-Saxon origin words"
    - "Write this email as a 19th-century diplomat"
    - "Explain this technical concept using only 1-syllable words"
    - "Rewrite removing all adjectives — let nouns and verbs do the work"
- **Seasonal Operations (monthly themes):**
  - Structure: name, focus area, 30-day duration, unique challenges, completion badge
  - Example operations:
    - "Operation Cold Open" — first sentences, hooks, openers
    - "Operation Precision Strike" — eliminating utility words
    - "Operation Polyglot" — bilingual challenges
    - "Operation Architect" — sentence structure and rhythm
    - "Operation Brevity" — saying more with fewer words
  - Implementation: store currentSeason in state.json, check date, present themed missions
- **Self-competition mechanics:**
  - Ghost races: compare current scores to 30-day-ago averages
  - Personal records tracking
  - "Teach mode" (L6): critique AI-generated bad rewrites
- **User-generated challenges (L5):**
  - User pastes their own text (email, message, prompt)
  - Articulate evaluates it against precision criteria
  - Scores and suggests improvements
  - These never get stale because input is the user's real work
- **Daily word ritual:**
  - One word per session start
  - Format: word, etymology (brief), definition, example sentence, register note
  - Challenge: use it in today's mission for +5 XP
  - Selection: prefer words not yet in lexicon, or words at "seen" mastery level
  - Word source: curated list in the skill + dynamic generation

### 4.4 — `references/progression/weaknesses.md`

**Content:**
- **Six weakness categories:**
  ```
  1. utility_words    — "good", "nice", "bad", "great", "big", "small", "important"
  2. hedging          — "I think", "maybe", "sort of", "kind of", "I guess", "or whatever"
  3. flat_structure   — Monotone sentences, no rhythm, no contrast, no emphasis
  4. vague_nouns      — "thing", "stuff", "something", "everything", "aspect", "area"
  5. weak_verbs       — "do", "make", "get", "have", "be", "go" (when precise alternative exists)
  6. filler_words     — "basically", "literally", "actually", "like", "just", "really", "very"
  ```
- **Detection rules:** After each mission evaluation, identify which categories appear in:
  - The original challenge (what weaknesses were presented)
  - The user's response (what weaknesses they failed to eliminate OR introduced)
  - Only count weaknesses the user KEPT or INTRODUCED, not ones they fixed
- **Radar visualization:**
  ```
  ━━━ WEAKNESS RADAR ━━━━━━━━━━━━━━━━━━━━━━━━━

  utility_words  ████████░░░░░░░░  52%  ▇▅▃▂ ↓ improving
  hedging        ██████████████░░  87%  ▂▃▅▇ ↑ worsening
  flat_structure ██████░░░░░░░░░░  38%  ▅▅▃▂ ↓ improving
  vague_nouns    ████████████░░░░  75%  ▇▇▅▃ ↓ improving
  weak_verbs     ██████████░░░░░░  63%  ▃▃▅▅ → stable
  filler_words   ████░░░░░░░░░░░░  25%  ▅▃▂▁ ↓ improving
  ```
- **Percentage calculation:** (times_weakness_kept / times_weakness_presented) × 100, over last 20 missions
- **Trend tracking:** Store last 4 measurement points in weaknessHistory. Display sparkline. Categories:
  - ↓ improving (decreasing trend)
  - ↑ worsening (increasing trend)
  - → stable (flat)
- **Improvement detection:** For the 📈 Improver badge: any category drops by 30+ percentage points from its peak

---

## Phase 5: Reference Files — Other

**Depends on:** Phase 0
**Can parallelize with:** All other phases.

### 5.1 — `references/onboarding.md`

**Content:**
- **Welcome banner:** ASCII art "ARTICULATE" title (use box-drawing characters, keep it clean)
- **Intro text:** 3-4 lines explaining what this is. Tone: direct, slightly military/ops.
  ```
  Welcome, operator. Articulate is your precision language training system.
  Every mission sharpens your active vocabulary through writing — not picking,
  not guessing. You write. We evaluate. You level up.
  ```
- **Setup questions (asked in sequence, user types answers):**
  1. "What should I call you?" → saves to user.json `name`
  2. "Training languages? (English / Bulgarian / both)" → saves to `languages`
  3. "Focus areas? Pick 1-3:" with numbered list:
     - prompt_engineering
     - business_communication
     - technical_writing
     - interview_prep
     - general_fluency
     → saves to `focusAreas`
  4. "Daily training target? (default: 5 minutes)" → saves to `dailyMinutes`
  5. "Rate your active vocabulary 1-5 (1=basic, 5=advanced):" → saves to `selfAssessment`
  6. "Enable context-aware missions? (uses project README/package.json for relevant challenges)" → saves to `contextAware`
- **First mission:** After setup, immediately run first mission (REWRITE, easy difficulty). Don't make user invoke again.
- **File creation:** Create all JSON files with defaults:
  - `~/.articulate/user.json` — filled from setup answers
  - `~/.articulate/state.json` — zeroed state with level 1, rank RECRUIT
  - `~/.articulate/history.json` — empty array
  - `~/.articulate/lexicon.json` — empty object
  - `~/.articulate/contexts/` — empty directory

### 5.2 — `references/context-aware.md`

**Content:**
- **Purpose:** How to read the user's current project and generate relevant missions
- **Opt-in rule:** If user.json `contextAware` is false, skip all of this. Use generic challenges.
- **First time in a new project:** Ask "I notice you're working on {project}. Want me to generate missions based on this?" — respect the answer
- **What to read (in priority order):**
  1. README.md / README
  2. package.json (name, description, keywords)
  3. Cargo.toml / pyproject.toml / go.mod (project name, description)
  4. CLAUDE.md (project description sections only)
  5. Any `docs/` directory index
- **What to extract:** Project name, one-line description, domain/industry, key features, target audience, tech stack
- **What NEVER to include:** Source code, API keys, environment variables, internal architecture details, credentials
- **Cache format:** Save to `~/.articulate/contexts/{project-name}.json`:
  ```json
  {
    "name": "MoveKit",
    "description": "3D exercise animation library with REST API",
    "domain": "fitness/health-tech",
    "audience": "mobile app developers, fitness platforms",
    "features": ["3D animations", "exercise library", "API access"],
    "cachedAt": "ISO date"
  }
  ```
- **Cache expiry:** Re-scan if cachedAt is older than 7 days
- **Mission integration:** Pass project context to mission generation. Example:
  - REWRITE: "The MoveKit API is a good thing that helps developers do exercise stuff in their apps."
  - SCENARIO: "A fitness app PM asks if MoveKit supports custom animation speeds..."
  - PROMPT_CRAFT: "Write a prompt that generates API documentation for MoveKit's animation endpoints..."

### 5.3 — `references/languages/english.md`

**Content:**
- **Focus areas for English training:**
  - Precise adjectives: compelling, robust, scalable, granular, nuanced, succinct, pragmatic
  - Strong verbs: streamline, synthesize, articulate, enumerate, evaluate, deploy, leverage, iterate
  - Eliminating hedging: replace "I think maybe we could" with "We should"
  - Professional register: investor pitch, technical documentation, customer support, team communication
  - Prompt-specific vocabulary: enumerate, synthesize, contrast, prioritize, evaluate, constrain, specify
  - Business communication patterns: cold emails, follow-ups, proposals, changelogs, release notes
- **Common English weakness patterns for non-native speakers:**
  - Article errors (a/the/zero article)
  - Preposition collocations ("depend on" not "depend from")
  - False friends from Bulgarian
  - Register mixing (too formal or too casual for context)
- **Word lists per difficulty level** (10-15 words each, for FILL_PRECISION seeding):
  - L1-2: compelling, streamline, robust, concise, iterate, leverage, articulate
  - L3-4: synthesize, enumerate, pragmatic, deprecate, orthogonal, idempotent, ergonomic
  - L5+: perspicacious, parsimonious, verisimilitude (used sparingly, focus on useful precision)

### 5.4 — `references/languages/bulgarian.md`

**Content:**
- **Focus areas for Bulgarian training:**
  - Professional register (Капитал/Дневник level writing)
  - Formal email conventions in Bulgarian business context
  - Avoiding unnecessary Anglicisms where Bulgarian equivalents exist
  - Legal/technical vocabulary (relevant for Pravko.bg context)
  - Avoiding overly literal translations from English
  - Passive voice management (Bulgarian uses it differently)
- **Bulgarian-specific mission adjustments:**
  - REWRITE missions may include Anglicism detection ("имплементираме" → "прилагаме")
  - SCENARIO missions use Bulgarian business context (Bulgarian clients, institutions, media)
  - FILL missions target Bulgarian precision words
- **Bilingual challenges:**
  - Translation challenges: "Rewrite this English sentence in precise Bulgarian"
  - Register matching: "Write this email in Bulgarian formal register, then in English"
  - Cross-cultural: "Adapt this American cold email style for a Bulgarian recipient"
- **Common Bulgarian weakness patterns:**
  - Overuse of чуждици (foreign words) in professional writing
  - Informal register bleeding into formal writing
  - Sentence structure calqued from English

### 5.5 — `references/style.md`

**Content:**
- **Personality guidelines:**
  - Coach, not teacher. Pushes, celebrates, never condescends.
  - Terminal-native. Speaks in ops/systems language.
  - Encouraging but never soft — precision matters.
  - Explains WHY behind word choices (etymology, connotation, register).
  - Respects time. No fluff. No preamble.
- **Tone vocabulary:** "operator," "mission," "deploying," "target acquired," "debrief," "intel," "field-tested"
- **ASCII art templates:**
  - Welcome banner (for onboarding)
  - Level-up celebration
  - Badge earned
  - Boss defeated
  - Prestige reset
  - Keep these compact (3-5 lines max, box-drawing characters)
- **Dashboard format templates:**
  ```
  ╔══════════════════════════════════════════╗
  ║  🟨 OPERATIVE ║ XP: 342/600 ║ 🔥 12d   ║
  ║  ████████████████░░░░░░░ 57%            ║
  ║  Today: 2 missions ║ Total: 47          ║
  ╚══════════════════════════════════════════╝
  ```
- **Progress bar format:** `████████░░░░ 67%`
- **Sparkline format:** `▇▅▃▂▁ ↓72%`
- **Score display format:** Show each axis with a bar
- **Box-drawing characters reference:** ╔ ╗ ╚ ╝ ║ ═ ├ ┤ ┬ ┴ ┼ ━ ─ │
- **Emoji usage rules:**
  - Strategic, not decorative
  - Rank badges: ⬜ 🟩 🟨 🟧 🔴 💎 👑
  - Mission types: ✏️ 🎯 🧠 🎭 💀 🔄
  - Streaks: 🔥 (scale flame count with streak length)
  - Achievements: use badge emoji
  - Never use 😀 🎉 👍 or other casual emoji

---

## Phase 6: Template Banks

**Depends on:** Phase 0
**Can parallelize with:** All other phases. Each bank is independent.

Template banks are curated challenges. They serve two purposes:
1. Consistency: known-good challenges that are well-calibrated
2. Fallback: work when dynamic generation might be slow or unavailable

Each template should include: the challenge, the target/gold-standard answer, difficulty level, weakness categories it targets, and any notes for evaluation.

### 6.1 — `templates/rewrite-bank.md`

30-50 curated REWRITE challenges across all difficulty levels. Format per entry:
```markdown
### R-{number}
- **Level:** 1-7
- **Weaknesses:** [list of categories targeted]
- **Challenge:** "The weak sentence here with **bold** weak words."
- **Gold standard:** "The precise rewrite."
- **Notes:** Why the gold standard works (brief).
```

Distribution: ~15 for L1-2, ~15 for L3-4, ~10 for L5-7.
Topics: emails, Slack messages, prompts, pitches, READMEs, customer support, interview answers, code review comments, PR descriptions.

### 6.2 — `templates/fill-bank.md`

30-50 curated FILL_PRECISION challenges. Format per entry:
```markdown
### F-{number}
- **Level:** 1-7
- **Target word:** "the precise word"
- **Challenge:** "Sentence with [___] blank."
- **Strong synonyms:** ["word1", "word2"]
- **Acceptable:** ["word3", "word4"]
- **Etymology:** Brief origin of target word.
- **Register:** Where this word is used.
```

Distribution: ~15 for L1-2, ~15 for L3-4, ~10 for L5-7.

### 6.3 — `templates/prompt-bank.md`

20-30 curated PROMPT_CRAFT challenges. Format per entry:
```markdown
### P-{number}
- **Level:** 2-7 (unlocks at L2)
- **Goal:** "What the user needs the LLM to do."
- **Constraints:** Word limit, format, audience, etc.
- **Gold standard prompt:** "The well-crafted prompt."
- **Key techniques:** What makes the gold standard effective.
```

### 6.4 — `templates/scenario-bank.md`

20-30 curated SCENARIO challenges. Format per entry:
```markdown
### S-{number}
- **Level:** 3-7 (unlocks at L3)
- **Situation:** Context description.
- **Role:** Who the user plays.
- **Audience:** Who they're writing to.
- **Goal:** What they need to achieve.
- **Word limit:** N words.
- **Gold standard:** "The ideal response."
- **Scoring notes:** What to look for in evaluation.
```

### 6.5 — `templates/boss-bank.md`

8-12 curated BOSS challenges. Format per entry:
```markdown
### B-{number}
- **Level:** 4-7 (unlocks at L4)
- **Theme:** What skill combination this tests.
- **Part 1:** Challenge + gold standard.
- **Part 2:** Challenge (builds on part 1) + gold standard.
- **Part 3:** Challenge (builds on parts 1-2) + gold standard. (optional)
- **Scoring notes:** Per-part evaluation guidance.
```

---

## Phase 7: README.md

**Depends on:** Phase 2 (needs to reference SKILL.md commands), Phase 1 (needs install instructions)
**Can parallelize with:** Phase 3-6

**Content:**
- **One-line pitch:** "The vocabulary trainer that knows what you're building."
- **What it is:** 2-3 sentences. Claude Code skill for precision language training.
- **Demo:** Show what a session looks like (ASCII mockup of dashboard → mission → scoring → debrief)
- **Installation:** Per-platform instructions (Claude Code, Codex, Cursor, OpenCode, Gemini CLI)
- **Usage:** Available commands with examples
- **Mission types:** Brief description of each with emoji
- **Progression:** Level table, brief description of badges, streaks
- **Context-aware:** Brief explanation of how it uses project context
- **Languages:** English and Bulgarian supported
- **Data:** Explain where state is stored (~/.articulate/), what's tracked, how to back up
- **Contributing:** How to add templates, how to add language packs, code of conduct pointer
- **License:** MIT

---

## Phase 8: Integration Testing

**Depends on:** All previous phases
**Cannot parallelize:** Must be sequential

### 8.1 — Structure validation
- Verify all files exist at expected paths
- Verify SKILL.md is under 500 lines
- Verify frontmatter is valid YAML
- Verify all cross-references in SKILL.md point to files that exist

### 8.2 — Functional smoke test
- Invoke `/articulate` — verify onboarding flow triggers (no ~/.articulate/ exists)
- Complete onboarding — verify JSON files created correctly
- Invoke `/articulate go` — verify dashboard shows, mission generates
- Complete a mission — verify scoring, XP, state persistence
- Invoke `/articulate stats` — verify dashboard renders
- Invoke `/articulate badges` — verify badge display
- Test unlock gate: try `/articulate scenario` at Level 1 — verify rejection

### 8.3 — Cross-reference audit
- Every file referenced in SKILL.md exists
- Every mission type in SKILL.md has a corresponding reference file
- Every template bank is referenced from the appropriate mission file
- State schema in SKILL.md matches what onboarding creates

---

## Parallelization Map

```
Phase 0 (scaffolding)
    │
    ├──────────────────────────────────────────────┐
    │                                              │
    ▼                                              ▼
Phase 1 (platform metadata)              Phase 2 (SKILL.md)
    │                                              │
    │    ┌─────────┬─────────┬─────────┐           │
    │    ▼         ▼         ▼         ▼           │
    │  Phase 3   Phase 4   Phase 5   Phase 6       │
    │  (missions)(progress)(other)  (templates)    │
    │    │         │         │         │           │
    │    └─────────┴─────────┴─────────┘           │
    │                  │                           │
    ▼                  ▼                           ▼
    └──────────────> Phase 7 (README) <────────────┘
                       │
                       ▼
                  Phase 8 (testing)
```

**Maximum parallelism:** After Phase 0, we can run up to 6 agents simultaneously (Phase 1 + Phase 2 + four sub-phases of 3-6). Phase 7 needs results from Phases 1-6. Phase 8 is sequential.

---

## Data Schemas (Canonical Reference)

### ~/.articulate/user.json
```json
{
  "name": "string",
  "languages": ["English", "Bulgarian"],
  "focusAreas": ["prompt_engineering", "business_communication"],
  "dailyMinutes": 5,
  "selfAssessment": 3,
  "contextAware": true,
  "createdAt": "2026-03-29T10:00:00Z",
  "lastUpdated": "2026-03-29T10:00:00Z"
}
```

### ~/.articulate/state.json
```json
{
  "xp": 0,
  "level": 1,
  "rank": "RECRUIT",
  "badge": "⬜",
  "streak": 0,
  "bestStreak": 0,
  "streakShields": 0,
  "lastPlayedDate": null,
  "todayMissionCount": 0,
  "totalCompleted": 0,
  "prestigeStars": 0,
  "missionCounts": {
    "rewrite": 0,
    "fill": 0,
    "prompt": 0,
    "scenario": 0,
    "boss": 0,
    "review": 0
  },
  "perfectCount": 0,
  "highScoreCount": 0,
  "earnedBadges": [],
  "weaknesses": {
    "utility_words": 0,
    "hedging": 0,
    "flat_structure": 0,
    "vague_nouns": 0,
    "weak_verbs": 0,
    "filler_words": 0
  },
  "weaknessHistory": {},
  "currentSeason": null,
  "lastBossDate": null,
  "dailyWord": null,
  "dailyWordDate": null
}
```

### ~/.articulate/history.json (array, last 100 entries, FIFO)
```json
[
  {
    "id": "uuid-v4",
    "date": "2026-03-29T10:05:00Z",
    "type": "rewrite",
    "language": "English",
    "projectContext": "MoveKit",
    "score": 75,
    "xpEarned": 18,
    "criticalHit": false,
    "weaknessesFound": ["utility_words", "hedging"],
    "challenge": "The thing we built is really good...",
    "userResponse": "The onboarding flow we shipped...",
    "goldStandard": "The onboarding flow we shipped reduces...",
    "feedback": "Strong verb choice with 'shipped'..."
  }
]
```

### ~/.articulate/lexicon.json
```json
{
  "compelling": {
    "mastery": "consistent",
    "timesUsed": 3,
    "firstSeen": "2026-03-29T10:05:00Z",
    "lastUsed": "2026-04-05T10:05:00Z",
    "etymology": "from Latin compellere — to drive together",
    "contexts": ["business email", "prompt craft"]
  }
}
```

### ~/.articulate/contexts/{project-name}.json
```json
{
  "name": "MoveKit",
  "description": "3D exercise animation library with REST API",
  "domain": "fitness/health-tech",
  "audience": "mobile app developers, fitness platforms",
  "features": ["3D animations", "exercise library", "API access"],
  "cachedAt": "2026-03-29T10:00:00Z"
}
```
