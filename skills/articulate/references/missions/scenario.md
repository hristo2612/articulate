# MISSION: SCENARIO

> Full operational reference. An AI agent reading ONLY this file can generate, present, evaluate, and debrief a SCENARIO mission.

---

## Overview

A real-world professional communication challenge with full context. The operator receives a situation, role, audience, goal, and word limit -- then writes their response. This is precision language under pressure: every word must serve the goal within a tight constraint.

**Unlocks at:** Level 3 (OPERATIVE, 300 XP)

**Principle:** Precision is not academic. It is deployed in emails, Slack messages, pitches, and support replies where word choice directly affects outcomes. This mission trains that deployment.

---

## Generation Rules

### Scenario Components

Every scenario MUST specify all five elements:

| Element | Description |
|---|---|
| **SITUATION** | What happened, what is the context, what is at stake |
| **ROLE** | Who the operator is writing as (founder, engineer, PM, support agent, etc.) |
| **AUDIENCE** | Who will read this (investor, customer, teammate, hiring manager, etc.) |
| **GOAL** | What the writing must accomplish (persuade, inform, defuse, close, etc.) |
| **WORD LIMIT** | Hard cap. Operator must stay within it. Forces conciseness. |

### Scenario Types

Draw from these real professional communication contexts:

| Type | Example |
|---|---|
| Cold email | Reaching out to a potential customer, partner, or investor |
| Investor follow-up | Post-meeting email with next steps and momentum |
| Customer support reply | Handling a complaint, bug report, or feature request |
| Interview answer | Behavioral or situational interview response |
| Team Slack update | Status update, decision announcement, or async discussion |
| PR description | Pull request summary for async code review |
| Technical proposal | Proposing an architectural change or new tool adoption |
| Conference talk pitch | 100-word abstract for a talk submission |
| Newsletter intro | Opening paragraph for a product or company newsletter |
| Product changelog entry | Release notes entry for a shipped feature |
| Escalation email | Raising a blocker or risk to leadership |
| Rejection with grace | Turning down a candidate, vendor, or proposal professionally |
| Cross-cultural message | Adapting tone/register for a different cultural context |

### Context-Aware Generation

If `contextAware: true` and project context is cached, use the operator's actual product/project:

```
SITUATION: A fitness app PM emails asking if {project} supports custom
animation speeds for rehabilitation exercises. They are evaluating you
against two competitors.
```

This makes every scenario immediately applicable to the operator's real work.

### Difficulty Scaling

**L3 (OPERATIVE):** Straightforward professional writing. Clear goal, familiar audience, reasonable word limit.

- Word limits: 60-100 words
- Single audience, clear goal
- Standard professional register
- Scenario types: support reply, Slack update, changelog entry

```
SITUATION: A user reports that your API returns 500 errors intermittently.
ROLE: Solo developer / founder
AUDIENCE: The frustrated user (non-technical)
GOAL: Acknowledge the issue, show you're on it, retain their trust.
WORD LIMIT: 80 words
```

**L4 (SPECIALIST):** Competing priorities. The operator must balance multiple goals or navigate sensitive dynamics.

- Word limits: 60-80 words (tighter constraint forces precision)
- Conflicting goals (be honest AND retain the customer)
- Audience may have specific expectations or power dynamics
- Scenario types: escalation email, investor follow-up, rejection

```
SITUATION: Your startup's biggest customer wants a feature that would
take your two-person team 3 months and derail your roadmap.
ROLE: Co-founder / CTO
AUDIENCE: The customer's VP of Product (long-standing relationship)
GOAL: Decline the feature request without losing the account.
WORD LIMIT: 70 words
```

**L5+ (COMMANDER+):** Persuasion, negotiation, cross-cultural sensitivity. Multi-layered communication where subtext matters.

- Word limits: 50-80 words (extreme constraint)
- Persuasion against resistance
- Cross-cultural considerations
- Multiple stakeholders (write for one, but others will see it)
- Scenario types: negotiation, cross-cultural, conference pitch, investor ask

```
SITUATION: You need to convince your engineering team to adopt a new
testing framework. The tech lead is openly skeptical and influential.
ROLE: Engineering manager
AUDIENCE: Engineering team (8 people, mixed seniority) in a Slack channel
GOAL: Propose the switch, acknowledge the tech lead's concerns, and get
buy-in for a 2-week trial without forcing a decision.
WORD LIMIT: 60 words
```

---

## Presentation Format

```
**MISSION: SCENARIO 🎭**

SITUATION: A potential customer emailed asking if your API supports
           batch processing. They're evaluating you against two competitors.
ROLE: Founder / sole developer
AUDIENCE: Technical PM at a mid-size SaaS company
GOAL: Confirm, differentiate, close toward trial signup.
WORD LIMIT: 80 words

Your response:
```

For L5+ with additional constraints:

```
**MISSION: SCENARIO 🎭**

SITUATION: Your SaaS product had a 4-hour outage affecting ~200 customers.
           Root cause: database migration untested against production volumes.
ROLE: CEO / co-founder
AUDIENCE: All affected customers (email blast)
GOAL: Take accountability, explain briefly, rebuild trust. No over-promising.
WORD LIMIT: 60 words | REGISTER: Transparent, humble, professional.

Your response:
```

---

## Evaluation Rubric

**5 axes. 0-20 each. Total: 0-100.**

### Word Choice (0-20)

Are the words precise, professional, and free of filler? Does every word carry information?

| Score | Criteria |
|---|---|
| 20 | Every word is deliberate and precise -- zero filler, zero utility words |
| 16 | Strong word choices throughout, one soft spot |
| 12 | Mix of precise and generic language |
| 8 | Relies heavily on utility words and generic phrases |
| 4 | Dominated by vague, low-information language |
| 0 | Word choices actively undermine the message |

### Register (0-20)

Is the tone and vocabulary appropriate for the audience, role, and context?

| Score | Criteria |
|---|---|
| 20 | Perfect register -- the audience would find this exactly right |
| 16 | Appropriate with minor register slip (slightly too formal/informal) |
| 12 | Generally okay but noticeable mismatch in places |
| 8 | Register mismatch that would affect reception |
| 4 | Significantly wrong for the audience (too casual for investor, too stiff for Slack) |
| 0 | Completely wrong register |

### Goal Achievement (0-20)

Does the response accomplish the stated goal? Would it produce the desired outcome?

| Score | Criteria |
|---|---|
| 20 | Goal fully achieved -- the response would produce the desired outcome in real life |
| 16 | Goal substantially achieved with minor gaps |
| 12 | Partially achieves the goal but misses key elements |
| 8 | Attempts the goal but execution is weak |
| 4 | Barely addresses the goal |
| 0 | Fails to address the goal or works against it |

### Conciseness (0-20)

Is the response within the word limit? Does every word earn its place?

| Score | Criteria |
|---|---|
| 20 | Within word limit AND every word earns its place -- nothing to cut |
| 16 | Within word limit, one phrase could be tighter |
| 12 | Within word limit but contains filler or redundancy |
| 8 | Slightly over word limit OR significantly padded |
| 4 | Significantly over word limit OR mostly filler |
| 0 | Grossly over word limit or entirely padded |

**Word limit enforcement:** Count words in the operator's response. If over the limit:
- 1-5 words over: note it, dock 2-4 points from Conciseness
- 6-15 words over: dock 8-12 points from Conciseness
- 16+ words over: dock full 20 points from Conciseness

### Persuasiveness (0-20)

Does the response move the audience toward the desired action? Is it compelling?

| Score | Criteria |
|---|---|
| 20 | Highly persuasive -- the audience would act on this |
| 16 | Convincing with minor missed opportunities |
| 12 | Reasonably persuasive but could be stronger |
| 8 | Attempts persuasion but lacks force |
| 4 | Fails to persuade or feels manipulative |
| 0 | Counter-persuasive -- audience would disengage |

---

## Feedback Format

```
**DEBRIEF**

**Score:** 76/100
├─ Word Choice:      16/20  ████████████████░░░░
├─ Register:         18/20  ██████████████████░░
├─ Goal Achievement: 14/20  ██████████████░░░░░░
├─ Conciseness:      16/20  ████████████████░░░░
└─ Persuasiveness:   12/20  ████████████░░░░░░░░

WORD COUNT: 74/80 -- within limit

**Gold standard:**
> "Hi [Name] -- yes, our batch endpoint processes up to 10k records
>  per call with sub-second latency. Unlike [Competitor A]'s queue
>  model, ours returns results synchronously -- no polling. I've
>  attached a code sample in Python. Want to test it? I can set up
>  a sandbox with 50k free API calls this week."

**Why:** "batch endpoint" names the feature precisely; "10k records per call with sub-second latency" replaces "fast" with a metric; "synchronously -- no polling" differentiates in one phrase; "sandbox with 50k free API calls this week" makes the CTA concrete.

**Wins:** [specific strong word choices and WHY they work]
**Sharper:** [specific improvements with alternatives]

WEAKNESSES DETECTED: utility_words, weak_verbs
```

### Gold Standard

ALWAYS provide a gold standard response. It must hit every element of the goal, stay within the word limit, use precise high-information language, match the register, and serve as a model.

### Why / Wins / Sharper

**Why:** Analyze 3-5 specific word choices from the gold standard -- name the word, explain what it accomplishes, contrast with a weaker version.

**Wins / Sharper:** Same format as REWRITE missions. Acknowledge strong choices, then suggest specific improvements.

---

## Weakness Mapping

SCENARIO missions detect all 6 weakness categories in the operator's response:

- **utility_words:** "good", "nice", "great", "important" where precision was needed
- **hedging:** "I think", "maybe", "we could possibly" -- uncertainty in professional communication
- **flat_structure:** All sentences same length and rhythm, no emphasis or contrast
- **vague_nouns:** "things", "stuff", "aspects" instead of naming specifics
- **weak_verbs:** "do", "make", "get", "have" instead of decisive action verbs
- **filler_words:** "basically", "just", "really" -- noise in tight word-limited writing

Only count weaknesses the operator **used**, not weaknesses in the scenario description.

```
WEAKNESSES DETECTED: hedging, filler_words
```

---

## Daily Word Bonus

If the operator deploys the session's daily word in their scenario response:

```
DAILY WORD BONUS: +5 XP ("articulate" deployed in the field)
```

---

## Edge Cases

- **Operator exceeds word limit:** Score and provide feedback, but dock Conciseness points per the enforcement rules above. Note the count: "Your response: 94 words. Limit: 80. Over by 14."
- **Operator writes in a different format than expected:** (e.g., writes bullet points when an email was expected) Dock Register points if the format is inappropriate for the scenario. A Slack update in bullets is fine; an investor email in bullets may lose register points.
- **Operator changes the scenario:** (e.g., invents facts not in the briefing) Minor additions for realism are fine. Major departures (inventing a product feature not mentioned, changing the audience) should be noted but not heavily penalized -- the goal is word choice, not scenario compliance.
- **Operator asks clarifying questions about the scenario:** Respond: "Deploy with available intel, operator. Real communication rarely comes with complete context. Make reasonable assumptions."
- **Operator writes in the wrong language:** If the scenario implies English but they write in Bulgarian (or vice versa), note it. Score the quality of the writing in whatever language they used, but dock Register for language mismatch.
