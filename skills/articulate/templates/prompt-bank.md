# Prompt Craft Challenge Bank

> 25 curated PROMPT_CRAFT challenges. Unlocks at Level 2.
> Goals are realistic LLM tasks a developer/entrepreneur would actually perform.

---

## Levels 2-3 (Foundation)

### P-1
- **Level:** 2
- **Goal:** "Get the LLM to summarize a lengthy technical RFC into a decision-ready brief for your engineering manager."
- **Constraints:** Under 80 words. Must include: the proposal, the trade-offs, and a recommended action. Audience is a non-technical-but-smart engineering manager.
- **Gold standard prompt:** "Summarize this RFC for my engineering manager who approves architecture decisions but doesn't write code. Structure: (1) What we're proposing in one sentence, (2) Two strongest arguments for, (3) Biggest risk and how we'd mitigate it, (4) Your recommended decision in one line. Keep it under 80 words total. Write in plain English — no jargon without a parenthetical definition."
- **Key techniques:** Specifies the audience's knowledge level and decision authority. Provides an explicit numbered structure. Sets a word limit. Defines the jargon rule rather than vaguely saying "keep it simple."

### P-2
- **Level:** 2
- **Goal:** "Get the LLM to write a changelog entry for a new feature release."
- **Constraints:** Under 60 words. Must be user-facing (not developer-facing). Must lead with the benefit, not the mechanism.
- **Gold standard prompt:** "Write a changelog entry for our new batch-export feature. Audience: non-technical SaaS users who read the 'What's New' page. Lead with what they can now do, not how we built it. One sentence for the headline benefit, one sentence for how to access it, one sentence for any limitations. Under 60 words. Tone: helpful, not promotional."
- **Key techniques:** Defines the audience precisely (non-technical SaaS users, not developers). Gives a three-sentence structure. Separates benefit from mechanism. Constrains tone explicitly.

### P-3
- **Level:** 2
- **Goal:** "Get the LLM to review your cold email draft and identify weak spots."
- **Constraints:** Must return specific line-by-line feedback, not generic advice. Must evaluate against cold-email best practices.
- **Gold standard prompt:** "Review this cold email draft. For each sentence, rate it Pass/Rewrite and explain why in under 15 words. Evaluate against these criteria: (1) Does the opening line reference something specific about the recipient? (2) Is the value prop about their problem, not our features? (3) Is the CTA a single low-friction ask? (4) Is total length under 100 words? After the line-by-line, give one overall verdict: Send, Revise, or Scrap."
- **Key techniques:** Forces granular feedback (per-sentence, not per-paragraph). Provides explicit evaluation criteria instead of relying on the model's defaults. Asks for a clear verdict, preventing hedge-heavy responses.

### P-4
- **Level:** 2
- **Goal:** "Get the LLM to generate test cases for a function you describe."
- **Constraints:** Must cover happy path, edge cases, and failure modes. Output must be copy-paste-ready code.
- **Gold standard prompt:** "Generate test cases for this function: [function signature + behavior description]. Organize into three groups: (1) Happy path — standard inputs that should succeed, (2) Edge cases — boundary values, empty inputs, maximum sizes, (3) Failure modes — invalid types, null values, inputs that should throw. Write each test in [language/framework]. Use descriptive test names that state the expected behavior, not 'test1', 'test2'. Include a brief comment above each test explaining WHY this case matters."
- **Key techniques:** Categorizes tests into three explicit groups instead of asking for "comprehensive" tests. Specifies the naming convention. Asks for comments explaining rationale, not just the test code.

### P-5
- **Level:** 3
- **Goal:** "Get the LLM to compare two architectural approaches for a system design decision."
- **Constraints:** Must be structured as a decision matrix. Must include trade-offs, not just pros and cons. Must end with a recommendation.
- **Gold standard prompt:** "Compare these two approaches for [system]: [Approach A] vs [Approach B]. Evaluate across these dimensions: (1) Latency under normal load, (2) Latency under 10x spike, (3) Operational complexity (what can break at 3 AM), (4) Migration cost from our current system, (5) Team skill match (we have 3 Go engineers, 1 Python). For each dimension, declare a winner and explain in one sentence. End with: 'Recommended approach: [X] because [one-sentence reason].' If it's genuinely a coin flip, say so and explain what would be the tiebreaker."
- **Key techniques:** Defines exactly five evaluation dimensions (not "consider the trade-offs"). Grounds the comparison in the team's actual context (stack, team size). Forces a recommendation but permits honest ambiguity with a tiebreaker mechanism.

### P-6
- **Level:** 3
- **Goal:** "Get the LLM to draft a Slack message announcing a breaking change to internal teams."
- **Constraints:** Under 100 words. Must include: what changed, who is affected, what they need to do, and by when.
- **Gold standard prompt:** "Draft a Slack message for our #engineering channel announcing a breaking change. Context: [describe the change]. Structure it as: Line 1: emoji + bold one-line summary of what broke/changed. Line 2: Who is affected (which teams/services). Line 3: What they need to do (specific action, not 'update your code'). Line 4: Deadline. Line 5: Where to ask questions (channel or person). Keep it under 100 words. Tone: direct and urgent, not apologetic."
- **Key techniques:** Provides a five-line structure instead of asking for "all the important info." Specifies tone as "direct, not apologetic" — a subtle but important distinction for breaking-change comms. Requires a named escalation path.

### P-7
- **Level:** 3
- **Goal:** "Get the LLM to refactor a block of code for readability without changing behavior."
- **Constraints:** Must preserve exact behavior. Must explain each change. No new dependencies.
- **Gold standard prompt:** "Refactor this code for readability. Rules: (1) Do not change behavior — the same inputs must produce the same outputs, (2) Do not add dependencies or imports, (3) Prioritize: rename unclear variables first, extract named functions for repeated logic second, simplify conditionals third. For each change you make, add an inline comment starting with '// Refactor:' explaining what you changed and why. Show the complete refactored code, not diffs."
- **Key techniques:** Sets a priority order for refactoring steps (not just "make it cleaner"). Requires inline explanations for each change, making the output self-documenting. Explicitly forbids new dependencies to prevent scope creep.

### P-8
- **Level:** 3
- **Goal:** "Get the LLM to extract action items from meeting notes."
- **Constraints:** Must assign owners and deadlines. Must distinguish decisions from action items from open questions.
- **Gold standard prompt:** "Extract structured output from these meeting notes. Categorize everything into three sections: DECISIONS (things we agreed on — state each as a declarative sentence), ACTION ITEMS (things someone must do — format as: '[ ] [Owner]: [Task] by [Date]'), OPEN QUESTIONS (things we discussed but didn't resolve — state each as a question with the person responsible for answering). If no deadline was mentioned for an action item, flag it with '[NO DEADLINE — needs one]'. If no owner was mentioned, flag it with '[UNASSIGNED]'."
- **Key techniques:** Defines three distinct categories with different formatting rules for each. Flags missing information (no deadline, no owner) instead of silently ignoring it. Uses checkbox format for action items making the output directly pasteable into a task tracker.

---

## Levels 4-5 (Intermediate)

### P-9
- **Level:** 4
- **Goal:** "Get the LLM to write a technical blog post introduction that hooks developer readers in the first two sentences."
- **Constraints:** Under 50 words for the intro. Must use a concrete example or number in the first sentence. No "In this post, we'll explore..."
- **Gold standard prompt:** "Write a two-sentence introduction for a technical blog post about [topic]. Sentence 1 must open with a specific, concrete claim — a number, a measurement, or a real-world failure. No abstractions. Sentence 2 must create tension: what most people assume vs. what's actually true, or what should work vs. what breaks. Forbidden phrases: 'In this post,' 'Let's explore,' 'Have you ever wondered,' 'In today's world.' Under 50 words."
- **Key techniques:** Bans the most common AI-generated openers by name. Requires a concrete claim (number/measurement) in sentence one, making vagueness structurally impossible. The "tension" instruction in sentence two creates a reason to keep reading.

### P-10
- **Level:** 4
- **Goal:** "Get the LLM to evaluate a startup pitch deck and identify the weakest slide."
- **Constraints:** Must evaluate each slide separately. Must rank them. Must provide a rewrite suggestion for the weakest one.
- **Gold standard prompt:** "Evaluate this pitch deck slide by slide. For each slide, give: (1) What it communicates in one sentence, (2) Strength score 1-5 where 5 = 'investor would nod, no questions' and 1 = 'investor tunes out,' (3) One specific flaw if score < 4. After evaluating all slides, identify the single weakest slide and provide a complete rewrite. The rewrite must follow the rule: lead with the claim, support with one number, close with the implication. Assume the audience is a seed-stage VC who sees 20 decks per week."
- **Key techniques:** Forces per-slide evaluation (prevents the LLM from giving generic "good deck" feedback). Anchors the scoring rubric with behavioral descriptions. Provides a structural formula for the rewrite. Sets the audience's context and attention level.

### P-11
- **Level:** 4
- **Goal:** "Get the LLM to generate a SQL query from a natural language business question."
- **Constraints:** Must ask clarifying questions before writing the query. Must explain the query logic. Must include a test case.
- **Gold standard prompt:** "I need a SQL query to answer this business question: [question]. Before writing any SQL: (1) List any assumptions you're making about the schema (table names, column types, relationships), (2) Ask me up to 3 clarifying questions if the business question is ambiguous. Then write the query with: a comment block explaining the logic step by step, the SQL itself (formatted for readability — one clause per line), and a sample test case showing expected input rows and the expected output. Use [Postgres/MySQL] syntax."
- **Key techniques:** Forces the LLM to surface assumptions before committing to a solution. Limits clarifying questions to three (prevents infinite loops). Requires a test case, which catches logic errors the LLM might otherwise gloss over.

### P-12
- **Level:** 4
- **Goal:** "Get the LLM to write a pull request description that a reviewer can act on."
- **Constraints:** Must include context, changes, and testing. Must explain WHY, not just WHAT. Under 150 words.
- **Gold standard prompt:** "Write a PR description for this diff. Structure: '## Why' — one sentence explaining the problem or motivation (link to the issue if I provide one). '## What changed' — bullet list of the key changes, each bullet is one sentence starting with a verb (Added, Removed, Refactored, Fixed). '## How to test' — numbered steps a reviewer can follow to verify the change works. '## Risks' — anything that could break, or 'None identified' if genuinely safe. Keep the total under 150 words. Write for a reviewer who hasn't seen the ticket."
- **Key techniques:** Provides four named sections with explicit formatting rules per section. The verb-first bullet rule for "What changed" prevents passive, vague descriptions. Writing for "a reviewer who hasn't seen the ticket" forces context inclusion.

### P-13
- **Level:** 5
- **Goal:** "Get the LLM to roleplay as a demanding customer to stress-test your support response."
- **Constraints:** The customer must be specific about their frustration. Must escalate if the response is vague. Must have a hidden acceptance criteria.
- **Gold standard prompt:** "Roleplay as a frustrated enterprise customer. Context: You're the CTO of a 200-person company paying us $4,800/month. Your engineering team lost 6 hours of work because our export feature silently dropped rows when the dataset exceeded 100k records. Rules for your character: (1) You are technically sophisticated — vague apologies insult you, (2) You need three things: acknowledgment that data was lost, a technical explanation of why, and a committed timeline for the fix, (3) If the response gives all three, you de-escalate. If any are missing, you escalate to 'I need to speak with your VP of Engineering.' Stay in character. Do not break character to offer tips."
- **Key techniques:** Gives the roleplay character a specific context (company size, spend, exact incident). Defines hidden acceptance criteria (three requirements for de-escalation). Prevents the LLM from breaking character to "help" — which would defeat the exercise.

### P-14
- **Level:** 5
- **Goal:** "Get the LLM to analyze user interview transcripts and extract product insights."
- **Constraints:** Must separate observations from interpretations. Must identify patterns across multiple interviews. Must prioritize findings by frequency.
- **Gold standard prompt:** "Analyze these user interview transcripts. For each interview, extract: OBSERVATIONS (direct quotes or paraphrased statements — what the user actually said, with no interpretation), INTERPRETATIONS (what you infer from the observations — label each as 'High confidence' or 'Speculative'). After analyzing all interviews, create a PATTERNS section: group similar observations across interviews, rank by frequency (how many interviewees mentioned this), and for each pattern state: the pattern, the evidence count, a one-sentence product implication. Flag any contradictions between interviewees. End with the top 3 actionable findings."
- **Key techniques:** Forces the separation of data from interpretation (the most common mistake in qualitative research). Confidence labels prevent the LLM from presenting speculation as fact. Frequency ranking keeps the output prioritized. Contradiction flagging catches conflicting signals.

### P-15
- **Level:** 5
- **Goal:** "Get the LLM to draft a technical proposal for a system migration."
- **Constraints:** Must include current state, target state, migration path, risks, and rollback plan. Must be persuasive to both engineers and executives.
- **Gold standard prompt:** "Draft a technical proposal for migrating [current system] to [target system]. Structure: (1) CURRENT STATE — what we have now, including its specific limitations (not 'it's old,' but what breaks and when), (2) TARGET STATE — what we'll have after, with one measurable improvement per limitation listed above, (3) MIGRATION PATH — numbered phases, each with: duration estimate, what gets migrated, how we verify success before proceeding, (4) RISKS — top 3 things that could go wrong, each with a mitigation and a trigger for aborting, (5) ROLLBACK — how we revert each phase independently. Write the executive summary (3 sentences) assuming the reader has 2 minutes and cares about cost, timeline, and risk. Write the technical sections assuming the reader is a senior engineer who will challenge every assumption."
- **Key techniques:** Dual-audience instruction (executive summary vs. technical sections) forces the LLM to code-switch. Phase-by-phase verification prevents "big bang" migration plans. The rollback section per phase is more useful than a single rollback plan. Specific limitation-to-improvement mapping creates logical coherence.

---

## Levels 6-7 (Advanced)

### P-16
- **Level:** 6
- **Goal:** "Get the LLM to critique your writing style and identify three specific patterns you should break."
- **Constraints:** Must use examples from the provided text. Must suggest concrete replacements, not abstract advice. Must rank patterns by frequency.
- **Gold standard prompt:** "Analyze my writing style across these samples. Identify my three most frequent weakness patterns — not grammar errors, but vocabulary and structure habits that make my writing less precise or less persuasive. For each pattern: (1) Name it in 3-5 words (e.g., 'hedge-stacking before assertions'), (2) Show 3 exact quotes from my text where this pattern appears, (3) Rewrite each quote to demonstrate the fix, (4) Explain in one sentence what the pattern costs me (clarity? credibility? reader attention?). Rank the three patterns by frequency. Be blunt — I want to improve, not feel good."
- **Key techniques:** Requests patterns, not individual errors (systemic improvement). Requires exact quotes as evidence (prevents generic advice). Asks for rewrites (shows, doesn't just tell). The "be blunt" instruction overrides the LLM's politeness default.

### P-17
- **Level:** 6
- **Goal:** "Get the LLM to generate a competitive analysis from a set of landing pages."
- **Constraints:** Must extract positioning, pricing model, target audience, and key differentiator for each competitor. Must identify gaps no competitor fills.
- **Gold standard prompt:** "Analyze these competitor landing pages: [URLs or pasted content]. For each competitor, extract into a table: Company | One-line positioning | Target customer (be specific — not 'businesses') | Pricing model | Primary differentiator (the one thing they'd put on a billboard) | Biggest weakness visible from their landing page. After the table: (1) Identify the positioning cluster — what do most competitors claim? (2) Identify the gap — what customer need or positioning angle is no one claiming? (3) Draft a one-sentence positioning statement for us that occupies that gap. Be skeptical — if a competitor's landing page says 'AI-powered,' note whether they explain how or if it's buzzword dressing."
- **Key techniques:** The table format forces structured extraction (prevents narrative rambling). "What they'd put on a billboard" forces single-claim distillation. The skepticism instruction prevents the LLM from taking marketing claims at face value. The gap identification is the real output — the competitive table is just scaffolding.

### P-18
- **Level:** 6
- **Goal:** "Get the LLM to help you think through a pricing decision by modeling scenarios."
- **Constraints:** Must model at least three scenarios. Must include revenue projections. Must identify the key assumption that determines which scenario wins.
- **Gold standard prompt:** "Help me think through pricing for [product]. Current state: [current pricing, current customers, current revenue]. I'm considering: (A) [Option A], (B) [Option B], (C) [Option C]. For each option, model: projected monthly revenue at current customer count, projected revenue if we grow 20% in 6 months, likely churn impact (estimate based on the pricing change magnitude and typical SaaS elasticity), and one qualitative risk I might not be thinking about. Present as a table, then identify: which single assumption, if wrong, would flip your recommendation. End with: 'My recommendation is [X] because [one sentence]. The bet you're making is [the key assumption].'"
- **Key techniques:** Forces three explicit options (prevents the LLM from picking one and arguing for it). Requires quantitative modeling, not just pros/cons. The "key assumption" question is the highest-value output — it tells you what to validate before committing. The "bet you're making" framing acknowledges uncertainty honestly.

### P-19
- **Level:** 7
- **Goal:** "Get the LLM to generate a complete onboarding email sequence that reduces time-to-value."
- **Constraints:** Must be a 5-email sequence over 14 days. Each email must have one CTA. Must use behavioral triggers, not just time delays.
- **Gold standard prompt:** "Design a 5-email onboarding sequence for [product]. User persona: [description]. The goal is to get them from signup to [key activation metric] within 14 days. For each email: (1) Trigger — what event or non-event sends this email (e.g., 'signed up but hasn't connected a data source after 24 hours'), (2) Subject line — under 8 words, no exclamation marks, (3) Body — under 100 words, one CTA button with exact text, (4) What success looks like — the specific action we want them to take, (5) What happens if they don't take the action (does the sequence branch?). Include one re-engagement email for users who go silent after email 2. The sequence must feel like a person helping, not a system nudging. No 'Hey [first_name]!' — find a less generic opener for each."
- **Key techniques:** Behavioral triggers instead of time delays makes the sequence responsive, not robotic. Word limits on subject and body prevent bloated emails. The branching question forces the LLM to think about the sequence as a flow, not a list. Banning "Hey [first_name]!" kills the most common fake-personalization pattern.

### P-20
- **Level:** 7
- **Goal:** "Get the LLM to act as a red-team adversary for your product's security model."
- **Constraints:** Must identify at least 5 attack vectors. Must rate severity and exploitability. Must suggest mitigations.
- **Gold standard prompt:** "Red-team this system's security model. Context: [describe authentication, authorization, data flow, and deployment]. Your goal is to find ways to: (1) access data belonging to another tenant, (2) escalate privileges from a regular user to admin, (3) exfiltrate data through the API, (4) abuse rate limits or resource allocation, (5) exploit the authentication flow. For each attack vector you find: describe the attack in 2-3 sentences (enough for an engineer to understand and reproduce), rate Severity (Critical/High/Medium/Low) and Exploitability (Trivial/Moderate/Expert), suggest a mitigation. Think like an attacker, not a consultant — I want 'here's how I'd break this' not 'you should consider implementing best practices.' If something looks secure, say so — don't invent fake vulnerabilities to fill the list."
- **Key techniques:** Five specific attack categories prevent generic "consider XSS" advice. The dual rating (severity + exploitability) is how real security teams prioritize. "Think like an attacker, not a consultant" shifts the LLM's posture from diplomatic to adversarial. Permission to say "this looks secure" prevents padding.

### P-21
- **Level:** 7
- **Goal:** "Get the LLM to help you prepare for a difficult conversation with a direct report about underperformance."
- **Constraints:** Must generate a conversation script, anticipated responses, and follow-up actions. Must be specific, not HR-template generic.
- **Gold standard prompt:** "Help me prepare for a performance conversation with a direct report. Context: [specific situation — what's not meeting expectations, how long, what's been tried]. Generate: (1) OPENING — first 2 sentences that are direct without being harsh. Name the specific behavior, not character traits, (2) EVIDENCE — 3 specific examples I should reference (based on the context I gave — don't invent ones), (3) ANTICIPATED RESPONSES — the 3 most likely things they'll say (defensive, deflecting, emotional) and a one-sentence response to each that acknowledges their point without abandoning mine, (4) THE ASK — what specific, measurable change I'm requesting and by when, (5) FOLLOW-UP — what I commit to do to support them. The script should sound like me talking to a human I respect, not an HR template. No phrases like 'I want to have an open dialogue about...' or 'I value your contributions.'"
- **Key techniques:** Forces behavior-specific feedback (not "you need to improve"). Anticipates defensive responses with prepared redirects. Requires mutual commitment (the manager's follow-up, not just the report's improvement). Bans HR-speak phrases by name, forcing genuine language.

### P-22
- **Level:** 7
- **Goal:** "Chain multiple LLM calls to build a research brief from a single question."
- **Constraints:** Must design a 3-step prompt chain where each step's output feeds the next. Must include validation between steps.
- **Gold standard prompt:** "Design a 3-step prompt chain that turns a broad research question into a structured brief. Step 1 (DECOMPOSE): Take the question '[broad question]' and break it into 5 specific sub-questions. For each sub-question, state what type of evidence would answer it (quantitative data, expert opinion, case study, etc.). Step 2 (RESEARCH): For each sub-question from Step 1, find or generate the best available answer. Rate your confidence (High/Medium/Low) for each. Flag any sub-question where your answer is based on training data that might be outdated. Step 3 (SYNTHESIZE): Combine the sub-answers into a 200-word brief structured as: Key finding, Supporting evidence (reference the strongest sub-answers), Confidence level (aggregate), and Recommended next step (what a human should verify). Between Step 1 and Step 2, validate: are the sub-questions actually answerable, or should any be reframed? Between Step 2 and Step 3, validate: are any sub-answers contradictory?"
- **Key techniques:** This is a meta-prompt — it teaches prompt chaining, not just single-shot prompting. Validation gates between steps prevent error propagation. Confidence rating and staleness flags teach the user to treat LLM output as evidence with uncertainty, not as facts.

### P-23
- **Level:** 6
- **Goal:** "Get the LLM to draft an investor update email that conveys bad news without losing confidence."
- **Constraints:** Under 300 words. Must include metrics (even bad ones). Must end with a clear ask or forward-looking plan.
- **Gold standard prompt:** "Draft a monthly investor update email. Context: [metrics — include the bad numbers]. Structure: (1) HEADLINE — one sentence, the single most important thing this month (do not hide the bad news below a buried paragraph), (2) METRICS TABLE — MRR, burn rate, runway, and 2 product metrics. Show month-over-month change with arrows. Do not omit a metric because it went down, (3) WINS — 2-3 specific accomplishments, each in one sentence, (4) CHALLENGES — the main problem, stated directly, followed by what you're doing about it (not 'we're exploring options'), (5) ASK — one specific thing you need from investors (intro, advice, hiring referral). Under 300 words total. Tone: confident but honest. The test: would you send this if the investor forwarded it to another investor?"
- **Key techniques:** "Do not hide the bad news" overrides the LLM's tendency to bury negatives. The "forwarding test" is a brilliant tone calibrator — it forces writing that survives reputational scrutiny. The metrics table with directional arrows makes bad numbers less scary by presenting them systematically.

### P-24
- **Level:** 5
- **Goal:** "Get the LLM to generate API documentation for an endpoint from its implementation code."
- **Constraints:** Must include request/response examples. Must document error cases. Must be developer-friendly, not auto-generated-feeling.
- **Gold standard prompt:** "Generate API documentation for this endpoint: [paste code]. Format: '## [HTTP METHOD] [path]' as heading. DESCRIPTION — one sentence explaining what this endpoint does in terms of the user's goal (not 'This endpoint handles...' but 'Create a new...'). AUTHENTICATION — what's required. REQUEST — show a realistic example with curl (not placeholder values like 'string123' — use values that make sense for the domain). RESPONSE — show the success response with all fields documented inline (field: type — description). ERRORS — list every error this endpoint can return, with the HTTP status code, error body, and a one-sentence explanation of when it happens. Include a common mistake section: 'Gotchas — things that trip up first-time callers.'"
- **Key techniques:** Realistic examples instead of placeholder values makes the docs immediately usable. Inline field documentation prevents the reader from scrolling between example and reference. The "Gotchas" section captures tribal knowledge that formal docs usually miss.

### P-25
- **Level:** 7
- **Goal:** "Get the LLM to help you make a hire/no-hire decision from interview notes."
- **Constraints:** Must weigh evidence, not impressions. Must identify the strongest signal and the biggest unknown. Must produce a clear recommendation.
- **Gold standard prompt:** "Help me make a hire/no-hire decision. Role: [title and key requirements]. Interview notes: [paste notes from all interviewers]. For each interviewer's notes: extract the single strongest positive signal and the single strongest concern. Ignore vibes — only count specific observed behaviors (what the candidate said or did, not how they 'seemed'). Then synthesize: (1) STRENGTHS — rank the top 3 by relevance to the role's key requirements, (2) RISKS — rank the top 3 concerns by how hard they are to coach (a skill gap is fixable; a values misalignment is not), (3) BIGGEST UNKNOWN — the one thing we still don't know that could change the decision, and how we'd find out, (4) RECOMMENDATION — Hire, No-hire, or 'Hire if [specific condition].' End with: 'The bar for this role is [restate from the requirements]. This candidate [meets/doesn't meet] it because [one sentence].'"
- **Key techniques:** "Ignore vibes" forces evidence-based evaluation. The coachability filter for risks is how the best hiring managers think. The "biggest unknown" prevents premature certainty. The final sentence forces a one-line justification that can't hide behind ambiguity.
