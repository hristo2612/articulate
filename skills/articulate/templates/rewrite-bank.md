# Rewrite Challenge Bank

> 35 curated REWRITE challenges. Distribution: 12 for L1-2, 12 for L3-4, 11 for L5-7.
> Weakness categories: utility_words, hedging, flat_structure, vague_nouns, weak_verbs, filler_words

---

## Levels 1-2 (Fundamentals)

### R-1
- **Level:** 1
- **Weaknesses:** [utility_words, weak_verbs]
- **Challenge:** "The new feature is **really good** and will **help** users **do things** faster."
- **Gold standard:** "The batch-upload feature cuts CSV import time from 4 minutes to 12 seconds."
- **Notes:** Replaces three vague elements (really good, help, do things) with a single concrete claim. Specificity creates credibility.

### R-2
- **Level:** 1
- **Weaknesses:** [utility_words, vague_nouns]
- **Challenge:** "We need to fix some **stuff** in the codebase because there are **things** that are **bad**."
- **Gold standard:** "We need to resolve three memory leaks in the payment module that spike RAM usage past 2 GB under load."
- **Notes:** "Stuff," "things," and "bad" are the unholy trinity of vague writing. The rewrite names the problem, the location, and the impact.

### R-3
- **Level:** 1
- **Weaknesses:** [utility_words, hedging]
- **Challenge:** "I **think** this PR is **pretty good** and should **probably** be merged soon."
- **Gold standard:** "This PR resolves the race condition in checkout. Tests pass on all three environments — ready to merge."
- **Notes:** Hedging ("think," "pretty," "probably") signals the writer hasn't actually reviewed the code. The rewrite states what was verified.

### R-4
- **Level:** 1
- **Weaknesses:** [filler_words, weak_verbs]
- **Challenge:** "**Basically**, the API **is having** some **issues** and we need to **look into** it."
- **Gold standard:** "The /payments endpoint returns 503 errors for 12% of requests. I'm tracing the root cause to the connection pool."
- **Notes:** "Basically" adds zero meaning. "Look into" is the vaguest possible description of debugging. The rewrite names the endpoint, the error, the rate, and the action.

### R-5
- **Level:** 1
- **Weaknesses:** [utility_words, vague_nouns]
- **Challenge:** "Our **product** is a **solution** that **helps** people with their **problems**."
- **Gold standard:** "Articulate trains developers to write precise English by replacing vague defaults with exact vocabulary."
- **Notes:** Every word in the original could describe literally any product. The rewrite passes the "only one company" test — you can tell what this is.

### R-6
- **Level:** 2
- **Weaknesses:** [hedging, weak_verbs]
- **Challenge:** "I **feel like** the deployment **might** have **caused** some **issues** with the login **flow**."
- **Gold standard:** "The 2:15 PM deploy broke OAuth token refresh — users on sessions older than 1 hour hit a redirect loop."
- **Notes:** "Feel like" in a production incident is dangerous. The rewrite gives the timestamp, the mechanism, the scope, and the symptom.

### R-7
- **Level:** 2
- **Weaknesses:** [flat_structure, utility_words]
- **Challenge:** "The meeting was **good**. We talked about **various things** and **got** some **good** ideas for the roadmap."
- **Gold standard:** "The roadmap review produced three decisions: sunset the legacy API by Q3, double down on the Slack integration, and hire a second backend engineer."
- **Notes:** "Good" appears twice, "various things" conveys nothing. The rewrite extracts the actual signal — what was decided.

### R-8
- **Level:** 2
- **Weaknesses:** [filler_words, hedging]
- **Challenge:** "**Just** wanted to **quickly** check in and **see if** you **maybe** had a chance to **look at** the **thing** I sent over."
- **Gold standard:** "Have you reviewed the pricing proposal? I need your sign-off by Thursday to hit the Q2 launch date."
- **Notes:** Five hedges in one sentence. The writer is apologizing for having a request. The rewrite states the ask, the artifact, and the deadline.

### R-9
- **Level:** 2
- **Weaknesses:** [utility_words, weak_verbs]
- **Challenge:** "This **tool** is **nice** because it **makes** your workflow **better** and **easier**."
- **Gold standard:** "This linter catches undefined variables and unused imports before CI, saving one failed pipeline per pull request on average."
- **Notes:** "Nice," "better," and "easier" are empty calories. The rewrite names the tool's function, its trigger point, and its measurable payoff.

### R-10
- **Level:** 2
- **Weaknesses:** [vague_nouns, flat_structure]
- **Challenge:** "We should **improve** the **user experience** of our **application** because **people** are **having trouble** with **it**."
- **Gold standard:** "Our checkout form loses 34% of users at the address step. Replacing the five-field layout with Google Places autocomplete should recover most of those drop-offs."
- **Notes:** "Improve the user experience" is a non-sentence. The rewrite names the page, the metric, the cause hypothesis, and the proposed fix.

### R-11
- **Level:** 2
- **Weaknesses:** [hedging, filler_words]
- **Challenge:** "**So basically** I was **wondering if** it would **perhaps** be possible to **get** access to the staging **environment**."
- **Gold standard:** "I need staging access to reproduce the billing bug in JIRA-4521. Can you add my SSH key by end of day?"
- **Notes:** Three hedges plus "basically" before getting to the point. The rewrite leads with the reason, names the ticket, specifies the mechanism, and sets a deadline.

### R-12
- **Level:** 2
- **Weaknesses:** [utility_words, weak_verbs]
- **Challenge:** "The **changes** are **good** and the code **looks** fine, I don't see any **issues** with **it**."
- **Gold standard:** "The refactor consolidates three redundant DB queries into one join. Execution time drops from 800ms to 120ms. Approved."
- **Notes:** A code review that says "looks fine" provides zero value. The rewrite summarizes what changed, quantifies the improvement, and gives a clear verdict.

---

## Levels 3-4 (Intermediate)

### R-13
- **Level:** 3
- **Weaknesses:** [flat_structure, vague_nouns, hedging]
- **Challenge:** "We've been **working on** some **improvements** to the system and **I think** they will **probably** make **things** **better** for our users."
- **Gold standard:** "We shipped three performance patches this sprint: lazy-loaded the dashboard images (LCP down 40%), paginated the activity feed (eliminated infinite scroll jank), and cached the org-settings query (page load under 200ms). Users on slower connections will feel the difference most."
- **Notes:** The original is 25 words of nothing. The rewrite uses a numbered structure, names each change, and quantifies each impact. Structure turns vagueness into authority.

### R-14
- **Level:** 3
- **Weaknesses:** [weak_verbs, utility_words]
- **Challenge:** "Our team **has** the **ability** to **handle** complex **challenges** and **deliver** **good results** in a timely manner."
- **Gold standard:** "Our four-person team shipped a HIPAA-compliant audit logging system in six weeks, passing the external security review on the first attempt."
- **Notes:** "Has the ability to handle" is four words doing one word's job. "Good results" is unmemorable. The rewrite replaces claims with a specific proof point.

### R-15
- **Level:** 3
- **Weaknesses:** [hedging, filler_words, flat_structure]
- **Challenge:** "**I guess** I **just** wanted to **kind of** explain that **basically** the **issue** is that we **sort of** need more **resources** to **get things done** properly."
- **Gold standard:** "We're two engineers short for the migration timeline. Without additional headcount by April, the legacy system cutover slips from Q3 to Q1 next year."
- **Notes:** Six hedging/filler words in one sentence. The writer is so afraid of the ask that the message drowns. The rewrite states the gap, the deadline, and the consequence.

### R-16
- **Level:** 3
- **Weaknesses:** [utility_words, vague_nouns]
- **Challenge:** "The **thing** about our **approach** is that it's **really** **different** from other **solutions** in the **space**."
- **Gold standard:** "Unlike Datadog and New Relic, we instrument at the application layer — no sidecar containers, no eBPF agents. One npm install and you're collecting traces."
- **Notes:** "Different" is the weakest possible differentiator. The rewrite names competitors, states the architectural difference, and highlights the user-facing consequence.

### R-17
- **Level:** 3
- **Weaknesses:** [weak_verbs, flat_structure]
- **Challenge:** "The customer **said** they **were** unhappy and **wanted** us to **do** something about the **problem** they **had** with our **service**."
- **Gold standard:** "The customer's invoice doubled after our November pricing migration. They've requested a credit for the overcharge and a rate lock through their contract renewal in March."
- **Notes:** Five weak verbs (said, were, wanted, do, had) produce a sentence with no information density. The rewrite tells you what happened, what the customer wants, and the timeline.

### R-18
- **Level:** 4
- **Weaknesses:** [hedging, utility_words, weak_verbs]
- **Challenge:** "I **think** we **should** **probably** **look into** **maybe** using a **different** database because the current one **might** not **be** **good** enough for our **needs**."
- **Gold standard:** "Postgres is hitting write throughput limits at 15k inserts/sec during peak ingestion. I'm benchmarking ScyllaDB and TiDB this week — both handle our access pattern (append-heavy, range-scan reads) and scale horizontally."
- **Notes:** Four hedges around a vague suggestion. The rewrite states the current system, the measured limit, the candidates, the evaluation criteria, and the timeline.

### R-19
- **Level:** 4
- **Weaknesses:** [flat_structure, vague_nouns, filler_words]
- **Challenge:** "**So** the **situation** is that we have some **issues** with **things** and we need to **figure out** a **way** to **deal with** all the **stuff** that's **going on**."
- **Gold standard:** "Three production incidents in two weeks — all traced to the event bus. The retry logic has no exponential backoff, so a single downstream timeout cascades into a queue backup. I'm proposing we add circuit breakers before Friday's deploy."
- **Notes:** The original is an anxiety sentence — the writer knows something is wrong but can't articulate it. The rewrite demonstrates diagnostic clarity: pattern, root cause, mechanism, and proposed fix.

### R-20
- **Level:** 4
- **Weaknesses:** [utility_words, hedging, weak_verbs]
- **Challenge:** "This **feature** would be **nice** to have and **I think** it could **potentially** **make** a **good** impact on our **numbers**."
- **Gold standard:** "Adding seat-based pricing to the Team plan would increase average contract value by an estimated $2,400/year per account, based on our median team size of 8 and the $25/seat/month price point competitors use."
- **Notes:** "Nice to have" is a death sentence in product prioritization. The rewrite builds a back-of-napkin business case with real numbers.

### R-21
- **Level:** 4
- **Weaknesses:** [weak_verbs, flat_structure, vague_nouns]
- **Challenge:** "The **update** **includes** some **changes** to **several** **areas** of the codebase and **addresses** a few **things** that **were** **reported** by users."
- **Gold standard:** "v2.4.1 patches the CSV export crash on datasets over 50k rows (GH-891), restores dark-mode contrast on the settings page (GH-903), and adds request-ID headers to all API responses for easier support debugging."
- **Notes:** A changelog that says "some changes to several areas" insults the reader's time. The rewrite lists each fix, references the issue, and explains the user-facing effect.

### R-22
- **Level:** 4
- **Weaknesses:** [hedging, filler_words, utility_words]
- **Challenge:** "**Honestly**, **I feel like** the interview went **pretty well** and **I think** the candidate was **quite good** and would **probably** be a **nice** addition to the team."
- **Gold standard:** "Strong hire. She traced the system design problem to a cache invalidation issue in under two minutes, wrote clean Go with tests unprompted, and asked pointed questions about our on-call rotation. One concern: she hasn't worked with event-driven architectures, which is 40% of our stack."
- **Notes:** "Pretty well" and "quite good" give a hiring committee nothing to act on. The rewrite provides specific evidence for the recommendation and flags the one risk.

### R-23
- **Level:** 4
- **Weaknesses:** [utility_words, vague_nouns, weak_verbs]
- **Challenge:** "We need to **make** sure our **thing** **has** all the **right** **stuff** so **people** can **use** it **well** and **get** **value** from it."
- **Gold standard:** "The SDK must ship with TypeScript types, a quickstart guide under 50 lines, and error messages that link to the relevant docs page. Developers should go from install to first API call in under 3 minutes."
- **Notes:** "Thing," "stuff," "people," "value" — pure abstraction. The rewrite names the artifact (SDK), three concrete requirements, and a measurable success threshold.

### R-24
- **Level:** 4
- **Weaknesses:** [flat_structure, hedging]
- **Challenge:** "The customer **might** churn **I think**, they **seem** kind of frustrated with **some things** and **maybe** we should **try** to **reach out** or **something**."
- **Gold standard:** "Acme Corp hasn't logged in since Feb 12 and their support tickets mention slow exports three times. I'm scheduling a call with their engineering lead this week to demo the new batch-export endpoint that ships Thursday."
- **Notes:** "Might churn I think" is uncertainty squared. The rewrite cites behavioral evidence (no login, ticket pattern), names the account, and describes a concrete save play.

---

## Levels 5-7 (Advanced)

### R-25
- **Level:** 5
- **Weaknesses:** [flat_structure, weak_verbs, hedging]
- **Challenge:** "We've **been** **working** on this for a while and **I think** we're **making** **progress** but there **are** still some **things** that **need** to **be** addressed before we can **move forward** with the launch."
- **Gold standard:** "Authentication and billing are production-ready. Two blockers remain: the webhook retry logic fails silently after three attempts (needs dead-letter queue), and the rate limiter doesn't share state across pods (needs Redis backend). Both are scoped — estimated 4 dev-days total. Launch target: March 18."
- **Notes:** The original reads like a status update from someone who hasn't checked the board. The rewrite categorizes work (done vs. blocked), names each blocker with technical specificity, estimates effort, and commits to a date.

### R-26
- **Level:** 5
- **Weaknesses:** [utility_words, vague_nouns, flat_structure]
- **Challenge:** "Our **product** is a **platform** that **provides** **various** **tools** and **resources** to **help** **businesses** **improve** their **operations** and **achieve** **better** **outcomes**."
- **Gold standard:** "We build real-time inventory sync for Shopify merchants with multiple warehouses. When a customer buys the last unit in Dallas, the Austin and Portland listings update in under 2 seconds — eliminating oversells that cost mid-market merchants an average of $4,200/month in refunds and re-shipping."
- **Notes:** The original is a platitude machine — it could describe 10,000 companies. The rewrite names the platform (Shopify), the user (multi-warehouse merchants), the mechanism (real-time sync), the edge case (last-unit race), and the dollar impact.

### R-27
- **Level:** 5
- **Weaknesses:** [hedging, filler_words, weak_verbs]
- **Challenge:** "**So basically**, **I guess** what I'm **trying to say** is that **perhaps** we **should** **consider** **looking into** the **possibility** of **exploring** **alternative** approaches to **handling** this **kind of** **situation**."
- **Gold standard:** "The current retry-and-alert approach isn't working — we've had three false pages this week. I propose we switch to a circuit-breaker pattern: trip after 5 consecutive failures, half-open after 30 seconds, and alert only on trip state changes."
- **Notes:** Twelve hedging words before reaching a point that never arrives. The rewrite names the current approach, states why it's failing (with evidence), and proposes a specific alternative with parameters.

### R-28
- **Level:** 5
- **Weaknesses:** [flat_structure, utility_words, vague_nouns]
- **Challenge:** "The **results** of our **efforts** have been **good** and we're seeing **positive** **trends** across **various** **metrics** which is **encouraging** for the **future** of the **company**."
- **Gold standard:** "Since the September redesign, trial-to-paid conversion is up from 8% to 14%, median time-to-first-value dropped from 22 minutes to 6, and NPS climbed 18 points to +47. The bottleneck is now activation — 60% of signups never create a second project."
- **Notes:** "Positive trends across various metrics" is a sentence designed to survive any possible outcome. The rewrite names the intervention, cites three metrics with before/after values, and identifies the next constraint.

### R-29
- **Level:** 6
- **Weaknesses:** [weak_verbs, hedging, utility_words, flat_structure]
- **Challenge:** "I **think** the **thing** we **need** to **do** is **get** everyone **together** to **have** a **discussion** about the **direction** we **want** to **go** with this **project** and **make** sure we're all on the same page about **what** we're **trying** to **achieve** and **how** we're going to **get** there."
- **Gold standard:** "I'm calling a 30-minute architecture review Thursday at 2 PM. Agenda: (1) choose between the monorepo migration and the API gateway approach — I'll present the trade-off matrix, (2) assign ownership for the three unowned services, (3) lock the Q3 milestone scope. Pre-read in the shared doc."
- **Notes:** The original is 50 words of process anxiety. The rewrite converts it into a meeting invite with time, duration, three numbered agenda items, preparation instructions, and implied decision authority.

### R-30
- **Level:** 6
- **Weaknesses:** [vague_nouns, utility_words, flat_structure, hedging]
- **Challenge:** "**So** we've been **thinking** about **things** and the **general** **feeling** is that we **probably** need to **make** some **changes** to our **approach** to **handling** **certain** **aspects** of the **product** to **better** **serve** our **customers** and **improve** **overall** **satisfaction**."
- **Gold standard:** "Three patterns in this month's churn interviews: (1) onboarding takes too long — the median user spends 25 minutes before reaching their first dashboard, (2) the Slack integration breaks silently when workspaces exceed 500 members, and (3) annual billing customers can't self-serve downgrades, forcing them to email support and wait 48 hours. I'm drafting fixes for all three, prioritized by churn-risk impact."
- **Notes:** The original is 40 words of corporate vapor. The rewrite demonstrates evidence-based product thinking: data source (churn interviews), three specific findings with supporting detail, and a commitment to action.

### R-31
- **Level:** 6
- **Weaknesses:** [hedging, flat_structure, filler_words]
- **Challenge:** "**Just** to **sort of** circle back on this — **I think** what **happened** was **basically** **kind of** a miscommunication **thing** and **honestly** **I feel like** we **should** **maybe** **try** to be **better** about **this kind of stuff** **going forward**."
- **Gold standard:** "The deploy collision on Tuesday happened because we don't have a deploy lock. I've added a #deploy-queue channel and a simple bot that enforces one deploy at a time. If the queue backs up, we'll revisit with a proper CI/CD gate."
- **Notes:** Seven hedging/filler words and zero information. The rewrite names the incident (deploy collision), the date, the root cause (no lock), the immediate fix (bot), and the escalation path.

### R-32
- **Level:** 6
- **Weaknesses:** [utility_words, weak_verbs, vague_nouns]
- **Challenge:** "**Getting** more **people** to **use** our **product** is **important** and we need to **find** **ways** to **make** our **offering** more **appealing** to **potential** customers in order to **grow** the **business**."
- **Gold standard:** "Our top-of-funnel bottleneck is the pricing page — 68% of visitors bounce without clicking a plan. I'm testing two variants this week: one that leads with a 'calculate your savings' widget, and one that replaces the feature matrix with three customer stories segmented by company size."
- **Notes:** The original could be a fortune cookie from a business school. The rewrite identifies the exact funnel stage, cites the metric, and describes two concrete experiments.

### R-33
- **Level:** 7
- **Weaknesses:** [hedging, utility_words, flat_structure, vague_nouns, weak_verbs]
- **Challenge:** "I **think** what we **should** **probably** **do** is **try** to **figure out** a **good** **way** to **sort of** **leverage** our **existing** **stuff** to **kind of** **build** out **some** **new** **things** that could **potentially** **be** **really** **nice** for our users and **help** us **get** to **where** we **want** to **be** as a **company**."
- **Gold standard:** "Our 12,000-company dataset of onboarding flows is an untapped asset. I propose we productize it as a benchmarking tool: show new customers how their activation metrics compare to anonymized peers in their vertical. It costs us one engineer for two weeks, it gives Sales a demo-closer ('see where you rank'), and it turns raw data we already have into a retention feature."
- **Notes:** The original is 50 words of pure verbal fog. The rewrite identifies the specific asset, proposes a specific product, estimates the cost, and articulates three distinct value angles (engineering effort, sales utility, retention impact).

### R-34
- **Level:** 7
- **Weaknesses:** [flat_structure, hedging, filler_words, utility_words, weak_verbs]
- **Challenge:** "**Honestly**, **so basically**, the **whole** **situation** with the **thing** is that we've **kind of** been **going** back and forth on **it** for a while and **I guess** at the end of the day we **just** need to **make** a **decision** about **what** **direction** to **go** and **just** commit to **something** because **I think** **everyone** is **getting** **pretty** frustrated with the lack of **progress** on this **stuff**."
- **Gold standard:** "We've spent three sprints debating the auth architecture without converging. Here's my forcing function: I'm posting two RFC documents in Notion today — one for the embedded JWT approach, one for the OAuth proxy approach. Each covers latency, security surface, and migration cost. Team votes by Friday. Whoever loses buys coffee. We ship the winner in Sprint 14."
- **Notes:** The original is 60 words of existential frustration with zero action. The rewrite acknowledges the stall (three sprints), proposes a decision mechanism (competing RFCs), sets evaluation criteria, imposes a deadline, adds levity, and commits to an execution sprint.

### R-35
- **Level:** 7
- **Weaknesses:** [vague_nouns, utility_words, weak_verbs, flat_structure, hedging]
- **Challenge:** "We need to **think** about **how** to **make** our **approach** to **onboarding** **better** because **I think** the current **experience** **might** not **be** **giving** **people** the **right** **impression** and could **potentially** **be** **causing** **some** **issues** with **retention** and **stuff** **like** **that**."
- **Gold standard:** "Our onboarding is leaking users at two specific points: 62% drop off during the GitHub OAuth step (our permission scope list scares them — we request repo write access we don't need), and 45% of those who connect never complete the 'create first monitor' wizard (the form has 11 required fields). Fix #1: reduce OAuth scopes to read-only. Fix #2: replace the wizard with a one-click template that creates a pre-configured monitor. Estimated impact: recovering even half those drop-offs adds 300 activated users per month."
- **Notes:** The original is 40 words of anxiety. The rewrite is a mini product brief: two diagnosed drop-off points with percentages, root cause analysis for each, two concrete fixes, and a projected outcome. This is Level 7 writing — it doesn't just replace weak words, it demonstrates an entirely different mode of thinking.
