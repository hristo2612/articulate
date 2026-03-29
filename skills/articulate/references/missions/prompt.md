# MISSION: PROMPT CRAFT

> Full operational reference. An AI agent reading ONLY this file can generate, present, evaluate, and debrief a PROMPT_CRAFT mission.

---

## Overview

The operator receives a GOAL -- something they would want an LLM to accomplish. They write the prompt. This mission trains precise instruction-writing: the vocabulary of control, specification, and constraint.

**Unlocks at:** Level 2 (INITIATE, 100 XP)

**Principle:** Prompt engineering IS precision language. Vague prompts produce vague outputs. Every word in a prompt either adds signal or adds noise.

---

## Generation Rules

### Goal Design

Generate realistic LLM task goals. These should be things the operator would genuinely ask an AI to do:

| Category | Example Goals |
|---|---|
| Summarize | "Summarize a 2000-word product requirements doc into 5 bullet points for the engineering team" |
| Analyze | "Compare two database schemas and identify breaking changes" |
| Generate | "Write a cold email to a VP of Engineering introducing your API monitoring tool" |
| Draft | "Draft a changelog entry for a major version release with breaking changes" |
| Refactor | "Rewrite this function's documentation to be implementation-agnostic" |
| Evaluate | "Assess whether this pull request description is clear enough for async review" |
| Compare | "Compare three pricing strategies and recommend one for a developer tool" |
| Transform | "Convert this technical spec into a non-technical stakeholder summary" |

### Constraint Inclusion

Every goal MUST include at least one constraint the operator needs to address in their prompt:

- **Word/length limit:** "Keep the output under 100 words"
- **Format constraint:** "Output as a numbered list" or "Use markdown table"
- **Audience specification:** "For a non-technical PM" or "For a senior backend engineer"
- **Tone/register:** "Professional but approachable" or "Direct and technical"
- **Exclusion:** "Do not include pricing information" or "Avoid jargon"

At higher levels, stack multiple constraints.

### Context-Aware Generation

If `contextAware: true`, generate goals using the operator's actual project:

```
"Write a prompt that generates API documentation for {project}'s
authentication endpoints, targeting frontend developers who have
never used the API before. Output as markdown with code examples."
```

### Difficulty Scaling

**L2 (INITIATE):** Simple, single-step instructions. One clear task, one constraint.

```
GOAL: Get an LLM to summarize a meeting transcript into action items.
CONSTRAINT: Output as a bulleted list, max 5 items.
```

**L3 (OPERATIVE):** Multi-constraint tasks. Operator must specify format, audience, and scope.

```
GOAL: Get an LLM to draft a release announcement for a developer tool update.
CONSTRAINTS: Under 150 words, aimed at existing users, mention breaking changes
first, end with migration steps.
```

**L4 (SPECIALIST):** Multi-step prompts with examples and edge cases.

```
GOAL: Get an LLM to analyze customer feedback emails and categorize them
by sentiment and feature request.
CONSTRAINTS: Use a JSON output schema you define, handle ambiguous emails
gracefully, include confidence scores, process emails in batch.
```

**L5+ (COMMANDER+):** System prompt design. Role definition. Chain-of-thought scaffolding. Few-shot example crafting.

```
GOAL: Design a system prompt for an LLM that acts as a code review assistant.
CONSTRAINTS: It must enforce your team's style guide, explain WHY behind
suggestions (not just WHAT), handle 5 programming languages, and refuse to
auto-approve code with security implications.
```

---

## Presentation Format

```
━━━ MISSION: PROMPT CRAFT 🧠 ━━━━━━━━━━━━━━━━

Write a prompt that accomplishes this goal:

GOAL: Get an LLM to draft a cold outreach email to a potential
      API integration partner.
CONSTRAINTS:
  - Under 100 words
  - Professional but not stiff
  - Include a specific value proposition
  - End with a clear call to action

Your prompt:
```

For L4+, include additional context:

```
━━━ MISSION: PROMPT CRAFT 🧠 ━━━━━━━━━━━━━━━━

Write a prompt that accomplishes this goal:

GOAL: Design a system prompt for an LLM acting as a technical
      interviewer for backend engineering candidates.
CONSTRAINTS:
  - Must evaluate system design thinking, not just syntax
  - Should ask follow-up questions based on candidate responses
  - Difficulty should adapt to candidate's experience level
  - Must not reveal evaluation criteria to the candidate
CONTEXT: The LLM will be used via API with structured JSON output.

Your prompt:
```

---

## Evaluation Rubric

**5 axes. 0-20 each. Total: 0-100.**

### Specificity (0-20)

Are the instructions concrete and unambiguous? Could a different LLM interpret this prompt in only one way?

| Score | Criteria |
|---|---|
| 20 | Instructions are unambiguous -- only one reasonable interpretation exists |
| 16 | Clear with minor ambiguity in one area |
| 12 | Generally understandable but leaves room for divergent outputs |
| 8 | Multiple reasonable interpretations possible |
| 4 | Vague instructions that would produce inconsistent results |
| 0 | So vague the LLM would have to guess what is wanted |

### Constraints (0-20)

Are output format, length, tone, and scope explicitly specified?

| Score | Criteria |
|---|---|
| 20 | All relevant constraints addressed: format, length, tone, audience, scope, edge cases |
| 16 | Most constraints specified, one minor gap |
| 12 | Key constraints present but some left implicit |
| 8 | Only basic constraints mentioned |
| 4 | Constraints mostly absent |
| 0 | No constraints whatsoever |

### Structure (0-20)

Is the prompt organized logically? Sections, ordering, hierarchy?

| Score | Criteria |
|---|---|
| 20 | Excellent structure: context first, then task, then constraints, then output format |
| 16 | Well-organized with minor sequencing issues |
| 12 | Readable but could be better organized |
| 8 | Stream-of-consciousness, hard to parse |
| 4 | Disorganized, instructions buried |
| 0 | No discernible structure |

### Clarity (0-20)

Is the language precise? No vague words, no hedging, no filler?

| Score | Criteria |
|---|---|
| 20 | Every word is precise and necessary -- zero filler |
| 16 | Clean language with one vague term |
| 12 | Generally clear but some soft/vague language |
| 8 | Multiple vague terms or hedging phrases |
| 4 | More vague than precise |
| 0 | Dominated by utility words and filler |

### Register (0-20)

Is the vocabulary appropriate for prompt engineering? Does it use the right control words?

| Score | Criteria |
|---|---|
| 20 | Uses precise prompt vocabulary: "enumerate", "constrain", "format as", "exclude", "prioritize by" |
| 16 | Mostly uses effective prompt language |
| 12 | Mix of strong and weak prompt vocabulary |
| 8 | Generic language that works but lacks precision |
| 4 | Casual/conversational when precision is needed |
| 0 | Language actively undermines the prompt's effectiveness |

**Strong prompt vocabulary examples:** enumerate, synthesize, constrain, prioritize, evaluate, contrast, specify, exclude, structure as, format output as, given [context] produce [output], respond only with, do not include, if [condition] then [action].

**Weak prompt vocabulary examples:** "maybe", "try to", "something like", "I guess", "kind of", "do some stuff with", "make it good".

---

## Feedback Format

Show the operator's prompt, then an improved version, then explain key differences.

```
━━━ DEBRIEF ━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━━

SCORE: 72/100
├─ Specificity: 16/20  ████████████████░░░░
├─ Constraints: 14/20  ██████████████░░░░░░
├─ Structure:   12/20  ████████████░░░░░░░░
├─ Clarity:     16/20  ████████████████░░░░
└─ Register:    14/20  ██████████████░░░░░░

YOUR PROMPT:
> "Write a cold email to a partner. It should be short and professional.
>  Mention what our API does and why they should integrate. End with
>  asking for a meeting."

IMPROVED VERSION:
> "Draft a 80-word cold outreach email to a VP of Engineering at a
>  mid-size SaaS company. Structure: 1) one-sentence hook referencing
>  their product, 2) specific integration value prop with one metric,
>  3) call to action requesting a 15-minute demo call. Register:
>  professional, direct, zero fluff. Do not use 'synergy', 'leverage',
>  or 'circle back'. Output as plain text."

KEY DIFFERENCES:
- "short" --> "80-word" -- quantified constraint replaces vague adjective
- "a partner" --> "VP of Engineering at a mid-size SaaS" -- specific audience
- "Mention what our API does" --> "specific integration value prop with one metric" -- precise deliverable
- "asking for a meeting" --> "requesting a 15-minute demo call" -- concrete CTA with time commitment
- Added structure (numbered sections), anti-patterns (excluded cliche words), and format spec
- The improved version uses prompt-native vocabulary: "structure", "register", "output as"

WEAKNESSES DETECTED: vague_nouns, hedging
```

### Score Bar Rendering

Each axis gets a 20-character bar:

- Score 20 = `████████████████████` (20 filled)
- Score 16 = `████████████████░░░░` (16 filled, 4 empty)
- Score 12 = `████████████░░░░░░░░` (12 filled, 8 empty)
- Score 8  = `████████░░░░░░░░░░░░` (8 filled, 12 empty)
- Score 4  = `████░░░░░░░░░░░░░░░░` (4 filled, 16 empty)
- Score 0  = `░░░░░░░░░░░░░░░░░░░░` (0 filled, 20 empty)

### Improved Version

ALWAYS provide an improved version of the operator's prompt. This is the gold standard. It must:

- Address every constraint from the goal
- Use precise prompt vocabulary (enumerate, constrain, specify, exclude, structure as)
- Be tightly structured (context --> task --> constraints --> output format)
- Eliminate all vague/soft language
- Be realistically usable -- not an academic exercise

### KEY DIFFERENCES Section

For each major improvement, explain:

1. **What changed:** The specific word or phrase swap
2. **Why the change matters:** What precision or control it adds to the prompt
3. **What the original lacked:** Why the vague version would produce weaker LLM output

Focus on VOCABULARY CHOICES. This is a language training tool, not a prompt engineering course. The feedback should make the operator reach for more precise words next time.

---

## Weakness Mapping

PROMPT_CRAFT missions detect weaknesses in the operator's prompt language:

- **utility_words:** Used "good", "nice", "great", etc. in their prompt where specificity was needed
- **hedging:** Used "maybe", "try to", "I think", "sort of" -- uncertainty in instructions
- **vague_nouns:** Used "things", "stuff", "something" instead of naming what they want
- **weak_verbs:** Used "do", "make", "get" instead of precise instruction verbs (enumerate, synthesize, constrain)
- **filler_words:** Used "basically", "just", "really" -- noise in instructions
- **flat_structure:** Prompt is one undifferentiated block with no logical sections

Report in the debrief:

```
WEAKNESSES DETECTED: hedging, vague_nouns
```

---

## Daily Word Bonus

If the operator uses the session's daily word in their prompt, award +5 bonus XP:

```
DAILY WORD BONUS: +5 XP ("enumerate" deployed in prompt)
```

---

## Edge Cases

- **Operator writes an extremely long prompt:** Do not penalize length per se. A well-structured 200-word system prompt can score 100. Penalize only if length comes from redundancy, filler, or disorganization.
- **Operator uses markdown formatting in their prompt:** This is GOOD practice. Reward it under Structure.
- **Operator includes few-shot examples:** Excellent at L4+. Reward under Specificity and Structure.
- **Operator writes a meta-prompt (prompt about prompts):** If the goal calls for it (e.g., "design a system prompt"), this is correct. Evaluate the meta-prompt as a prompt.
- **Operator asks for clarification about the goal:** Respond: "Work with the intel you have, operator. Ambiguity is part of the mission. Make assumptions explicit in your prompt."
