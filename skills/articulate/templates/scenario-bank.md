# Scenario Challenge Bank

> 25 curated SCENARIO challenges. Unlocks at Level 3.
> Types: cold email, investor follow-up, customer support, interview answer, team Slack, PR description, technical proposal, conference pitch, newsletter, changelog.

---

## Levels 3-4 (Foundation)

### S-1
- **Level:** 3
- **Situation:** Your SaaS product just launched a Slack integration that saves teams from switching between tools for status updates. You found a VP of Engineering at a 150-person company who tweeted about "meeting fatigue" last week.
- **Role:** Founder/CEO of an early-stage startup.
- **Audience:** VP of Engineering who receives 30+ cold emails per week.
- **Goal:** Get a 15-minute demo call. Not a sale — just a conversation.
- **Word limit:** 80 words.
- **Gold standard:** "Hi [Name] — your tweet about meeting fatigue resonated. We built a Slack bot that replaces daily standup meetings with async check-ins. Three teams at [similar company] cut their weekly meeting load by 5 hours after switching. Would you be open to a 15-minute walkthrough this week? I can show you exactly how it maps to your existing Slack channels. No pitch deck — just a live demo in your workspace."
- **Scoring notes:** Look for: specific reference to the recipient's tweet (personalization), a concrete proof point (not "many companies"), a low-friction CTA (15 minutes, not "hop on a call"), and a credibility marker (live demo in their workspace). Deduct for: generic opener ("I hope this finds you well"), feature lists, and anything over 80 words.

### S-2
- **Level:** 3
- **Situation:** A customer on your $99/month plan emails saying the CSV export feature "doesn't work" and they're "considering alternatives." They've been a customer for 14 months.
- **Role:** Customer support engineer at a B2B SaaS company.
- **Audience:** Frustrated long-term customer who hasn't described the actual bug.
- **Goal:** Defuse the frustration, gather the information needed to diagnose the issue, and prevent churn.
- **Word limit:** 100 words.
- **Gold standard:** "Thank you for flagging this — a broken export on a 14-month account is something I take seriously. To diagnose the exact failure, I need two things: (1) the approximate row count of the dataset you're exporting, and (2) whether you see an error message or a silent failure (file downloads but is empty/truncated). I'm pulling your account's export logs now and will have an initial answer within 2 hours. If this is blocking your team today, I can run the export server-side and send you the file directly while we fix the root cause."
- **Scoring notes:** Look for: acknowledgment without excessive apology, specific diagnostic questions (not "can you tell me more"), a committed timeline, and an immediate workaround. Deduct for: template language ("we value your business"), asking the customer to "try clearing cache," or failing to address the churn signal.

### S-3
- **Level:** 3
- **Situation:** You just finished a phone screen with a company you're excited about. The recruiter asked you to "tell me about yourself" and you fumbled through a 3-minute ramble.
- **Role:** Senior developer interviewing for a Staff Engineer position.
- **Audience:** Technical recruiter who will pass notes to the hiring manager.
- **Goal:** Write a follow-up email that reframes your background clearly and reinforces your fit for the role.
- **Word limit:** 90 words.
- **Gold standard:** "Hi [Recruiter] — thanks for the conversation today. I realized I could frame my background more crisply: I've spent 8 years building payment infrastructure — first at [Company A] where I designed the idempotency layer for their checkout API (processing $2M/day), then at [Company B] where I led the migration from a monolith to event-driven microservices for a team of 12. The Staff Engineer role's focus on system reliability is exactly where my experience compounds. Looking forward to the technical round."
- **Scoring notes:** Look for: self-awareness about the fumble (without dwelling on it), a structured narrative (chronological with highlights), specific technical credibility markers, and a direct connection to the role. Deduct for: apologizing profusely, restating the entire resume, or failing to link experience to the specific role.

### S-4
- **Level:** 3
- **Situation:** Your team shipped a major refactor of the authentication module. The PR has 47 changed files and the reviewer hasn't started after 2 days.
- **Role:** Senior developer on a 6-person backend team.
- **Audience:** A peer engineer who is your assigned code reviewer.
- **Goal:** Get the review started without being pushy. Help the reviewer navigate the large diff efficiently.
- **Word limit:** 100 words.
- **Gold standard:** "Hey — I know the auth PR looks massive (47 files), but here's the fast path through it: 80% of the diff is moving existing code from /auth into /auth/legacy without changes. The actual new logic is in 4 files: auth/handler.go (new OAuth flow), auth/middleware.go (token validation), auth/store.go (session persistence), and auth/handler_test.go. I'd suggest reviewing those 4 files first — if the approach looks right, the rest is mechanical. Happy to walk through any of it on a call if that's faster. No rush on the mechanical moves."
- **Scoring notes:** Look for: a navigation guide for the diff (not just "please review"), identification of the high-signal files, an offer to assist without pressuring, and tone that respects the reviewer's time. Deduct for: passive aggression ("just following up"), guilt-tripping about the timeline, or not helping the reviewer prioritize.

### S-5
- **Level:** 3
- **Situation:** You need to announce in your team Slack channel that you're deprecating an internal API endpoint that 3 other teams depend on.
- **Role:** Backend team lead.
- **Audience:** 3 dependent teams (8-15 engineers total) who use this endpoint daily.
- **Goal:** Communicate the deprecation clearly, provide a migration path, and set a deadline without causing panic.
- **Word limit:** 120 words.
- **Gold standard:** "@channel Deprecation notice: /api/v1/user-profiles endpoint\n\nWe're replacing /v1/user-profiles with /v2/users — the new endpoint returns the same data but supports pagination, field selection, and is 3x faster under load.\n\nTimeline:\n- Today: /v2/users is live and documented at [link]\n- March 15: /v1/user-profiles starts logging deprecation warnings in your service logs\n- April 30: /v1/user-profiles returns 410 Gone\n\nMigration: In most cases it's a URL swap + adding a `fields` parameter. Migration guide with before/after examples: [link]\n\nI'm available in #platform-support this week for migration questions. If your service has a non-standard usage pattern, DM me and we'll pair on the migration.\n\nNo action needed today — but please plan for the April 30 cutoff."
- **Scoring notes:** Look for: clear timeline with specific dates, a link to documentation, a migration effort estimate ("URL swap"), a support channel, and a calm closing. Deduct for: vague timelines ("soon"), no migration guide, a threatening tone, or burying the deadline.

### S-6
- **Level:** 4
- **Situation:** An investor you met at a conference 3 weeks ago said "send me your deck." You sent it and heard nothing. Now you need to follow up without seeming desperate.
- **Role:** First-time founder raising a pre-seed round.
- **Audience:** An angel investor who meets 10+ founders per month.
- **Goal:** Get a response — either a meeting or a clear pass.
- **Word limit:** 60 words.
- **Gold standard:** "Hi [Name] — following up on the deck I sent after [Conference]. Since we spoke, we've closed our first 3 paying customers ($1,800 MRR) and our design partner at [Company] signed a 12-month contract. I'd welcome 20 minutes to walk through the traction and what we'd do with $500K. If it's not a fit, a quick 'pass' is genuinely appreciated."
- **Scoring notes:** Look for: new information since last contact (traction update), a specific ask (20 minutes), a stated use of funds, and graceful permission to decline. Deduct for: "just checking in," apologizing for following up, restating the pitch from the deck, or not including new signal.

### S-7
- **Level:** 4
- **Situation:** Your monitoring dashboard shows that error rates on the /checkout endpoint spiked from 0.1% to 4.7% over the last hour. You've identified the cause — a bad config pushed in the latest deploy — and rolled it back.
- **Role:** On-call engineer.
- **Audience:** Your engineering team and the head of customer support (non-technical).
- **Goal:** Write a concise incident summary for the #incidents Slack channel that both audiences can act on.
- **Word limit:** 120 words.
- **Gold standard:** "Incident resolved: /checkout error spike (0.1% -> 4.7%)\n\nDuration: 14:23 - 15:01 UTC (38 minutes)\nImpact: ~340 checkout attempts received 500 errors. No payments were double-charged — the failure occurred before the payment processor call.\n\nRoot cause: Deploy at 14:20 included a config change that pointed the checkout service at the staging payment gateway. The staging gateway rejected all production tokens.\n\nResolution: Rolled back to previous deploy at 14:58. Error rate returned to baseline by 15:01.\n\nFor customer support: Affected users saw 'Something went wrong' and were not charged. Retrying the purchase will work. No refunds needed.\n\nFollow-up: I'm writing a postmortem with a proposal for config validation in the deploy pipeline. ETA: tomorrow EOD."
- **Scoring notes:** Look for: duration and impact quantified, technical root cause stated clearly, a section specifically for the non-technical audience, and a follow-up commitment. Deduct for: blame language, vague impact ("some users"), skipping the customer-support-friendly section, or no postmortem commitment.

### S-8
- **Level:** 4
- **Situation:** Your open-source CLI tool just hit 2,000 GitHub stars. You want to write a changelog for the v2.0 release that converts stargazers into active users.
- **Role:** Solo maintainer of an open-source developer tool.
- **Audience:** Developers who starred the repo but haven't tried the tool yet.
- **Goal:** Make the changelog compelling enough that someone installs the tool within 5 minutes of reading it.
- **Word limit:** 150 words.
- **Gold standard:** "# v2.0 — The speed release\n\nThe CLI now runs 6x faster on large repos (benchmarked against a 50k-file monorepo). Here's what changed:\n\n**Parallel file scanning** — v1 walked the file tree sequentially. v2 spawns worker goroutines per directory, saturating all available cores. A 50k-file scan dropped from 18s to 2.8s.\n\n**Incremental caching** — After the first run, only changed files are re-scanned. Typical re-runs complete in under 400ms.\n\n**Streaming output** — Results appear as they're found instead of buffering until completion. You see the first match in under 100ms.\n\nBreaking change: The `--format` flag now defaults to `json` instead of `text`. Add `--format text` if you're piping to grep.\n\nTry it:\n```\nbrew install mytool && mytool scan .\n```\n\nFull benchmarks and migration notes: [link]"
- **Scoring notes:** Look for: a headline that promises a specific benefit (not "improvements"), quantified before/after performance numbers, a one-line install command, and the breaking change stated honestly. Deduct for: burying the breaking change, vague performance claims ("faster"), no install command, or a changelog that reads like a git log.

### S-9
- **Level:** 4
- **Situation:** You're writing a weekly newsletter to 800 subscribers who are early-stage founders. This week you learned something counterintuitive about pricing from talking to 5 customers.
- **Role:** Founder who writes a weekly newsletter about building in public.
- **Audience:** 800 early-stage founders who are time-poor and skeptical of generic advice.
- **Goal:** Share a genuine insight that readers forward to one friend.
- **Word limit:** 150 words.
- **Gold standard:** "Subject: We doubled our price and signups went up\n\nLast month I raised our price from $29 to $59/month. I expected signups to drop 30-40%.\n\nThey went up 12%.\n\nI called five customers who signed up at the new price. The consistent response: 'The $29 price made me think this was a side project. $59 felt like real software.'\n\nThe insight isn't 'charge more.' It's that price is a signal — and I was accidentally signaling 'hobby tool' to people shopping for 'production infrastructure.'\n\nTwo things I'd check before raising your price:\n1. Do customers describe your product in more serious terms than you do? (Mine did.)\n2. Are you losing deals to more expensive competitors? (I was — and thought it was about features.)\n\nHit reply if you've seen this in your own pricing."
- **Scoring notes:** Look for: a counterintuitive hook, real numbers (not hypothetical), customer quotes as evidence, a reusable framework (not just "here's what happened to me"), and a CTA that invites dialogue. Deduct for: obvious advice, no supporting evidence, hypothetical examples, or a preachy tone.

### S-10
- **Level:** 4
- **Situation:** You're proposing a new microservice to your team. The current monolith handles notifications, but notification logic is tangled with business logic and causing test flakiness.
- **Role:** Senior backend engineer.
- **Audience:** Your tech lead and two senior peers in an architecture review meeting.
- **Goal:** Get approval to extract the notification service. You have one written page to make your case.
- **Word limit:** 200 words.
- **Gold standard:** "## Proposal: Extract Notification Service\n\n**Problem:** Notification logic (email, push, in-app) is scattered across 14 files in the monolith. Changes to notification templates require full app deploys, and the notification tests account for 40% of our CI flakiness (they depend on real SMTP in staging).\n\n**Proposed solution:** Extract a standalone notification service that owns all delivery channels. The monolith publishes events (user.signup, invoice.paid, etc.) to a message queue. The notification service consumes events and handles template rendering, delivery, and retry logic independently.\n\n**What we gain:**\n- Notification template changes deploy in isolation (no app restart)\n- CI flakiness drops — notification tests run against a mock queue, not SMTP\n- Delivery retry logic lives in one place instead of three different try/catch blocks\n\n**What it costs:**\n- ~3 weeks of engineering time (1 person)\n- New infrastructure: one SQS queue + one ECS service\n- Operational surface area increases (one more thing to monitor)\n\n**Migration path:** Phase 1: stand up service + migrate email notifications (1 week). Phase 2: push notifications (1 week). Phase 3: in-app notifications + deprecate monolith notification code (1 week).\n\n**Rollback:** Each phase can run in parallel with the monolith's existing notifications. If the service fails, the monolith code is still there."
- **Scoring notes:** Look for: quantified problem (14 files, 40% flakiness), honest cost assessment alongside benefits, phased migration with rollback, and specific infrastructure choices (not "some queue"). Deduct for: only listing benefits, vague timelines, hand-waving infrastructure needs, or no rollback plan.

---

## Levels 5-6 (Intermediate)

### S-11
- **Level:** 5
- **Situation:** You're a developer advocate preparing a 2-minute lightning talk pitch for a conference CFP. Your topic: a debugging technique you invented that uses git bisect with automated test scripts to find the exact commit that introduced a performance regression.
- **Role:** Developer advocate / senior engineer.
- **Audience:** Conference program committee (3-5 senior engineers who read 200+ proposals).
- **Goal:** Get accepted. Your pitch must stand out in a stack of proposals.
- **Word limit:** 100 words.
- **Gold standard:** "Title: 'Finding the Commit That Slowed You Down — Git Bisect + Benchmark Scripts'\n\nElevator pitch: Last quarter, our API latency crept from 200ms to 900ms over 47 commits and nobody noticed until a customer complained. I'll show the exact workflow I built to find the guilty commit in under 10 minutes: a bash script that combines git bisect with automated benchmark runs, binary-searching through commit history until it isolates the regression.\n\nAudience takeaway: A copy-paste-ready script and the mental model for when to reach for bisect over log-reading.\n\nFormat: Live terminal demo. No slides."
- **Scoring notes:** Look for: a concrete hook (200ms to 900ms), a clear takeaway the audience walks away with, format specification (live demo shows confidence), and brevity that respects the committee's time. Deduct for: vague topic descriptions ("I'll talk about debugging"), no concrete example, or proposals that sound like blog post outlines.

### S-12
- **Level:** 5
- **Situation:** A key hire (senior engineer) accepted your offer verbally but hasn't signed the contract after 5 days. You suspect they're weighing a competing offer.
- **Role:** Engineering manager at a 30-person startup.
- **Audience:** The candidate — a senior engineer who has options.
- **Goal:** Get the signed contract without pressuring or appearing desperate.
- **Word limit:** 80 words.
- **Gold standard:** "Hi [Name] — I know accepting an offer is a big decision, and I respect that you're being thoughtful about it. One thing I wanted to share: since we spoke, the team started scoping the event-driven architecture project I mentioned — you'd be leading the technical design from day one. I'm holding the req open through Friday. If there's anything about the offer or the role I can clarify, I'd rather address it now than have it be an unanswered question. No pressure either way."
- **Scoring notes:** Look for: respect for the candidate's decision process, new information that reinforces the role's appeal, a soft deadline (holding the req), and an open door for negotiation. Deduct for: urgency tactics ("this offer expires"), guilt ("the team is waiting"), or restating compensation details.

### S-13
- **Level:** 5
- **Situation:** You've been asked to write a technical proposal to migrate your company's infrastructure from Heroku to AWS. The CTO wants a one-page summary before committing engineering resources.
- **Role:** Platform engineer.
- **Audience:** CTO who has 10 minutes and cares about cost, risk, and timeline.
- **Goal:** Get approval to spend 2 weeks on a detailed migration plan.
- **Word limit:** 200 words.
- **Gold standard:** "## Heroku-to-AWS Migration: One-Page Summary\n\n**Why now:** Heroku costs us $4,200/month for 12 dynos. Equivalent AWS infrastructure (ECS Fargate + RDS) benchmarks at $1,100/month — a $37K annual saving. Beyond cost: we've hit Heroku's limits on background job concurrency (maxed at 2 worker dynos) and custom domain SSL requires their $250/month addon.\n\n**What moves:** 3 web services, 2 worker services, 1 Postgres database (240 GB), Redis, and scheduled jobs.\n\n**What doesn't move (yet):** Review apps and CI pipeline stay on Heroku during migration. They move in a follow-up phase.\n\n**Timeline:** 6 weeks with 2 engineers. Week 1-2: infrastructure-as-code (Terraform) + staging environment. Week 3-4: migrate services one at a time, validate with shadow traffic. Week 5: migrate database with pg_dump/pg_restore during a 2-hour maintenance window. Week 6: monitoring, DNS cutover, and Heroku teardown.\n\n**Biggest risk:** The database migration window. Mitigation: we'll rehearse the restore three times in staging and have a rollback script that points DNS back to Heroku within 5 minutes.\n\n**Ask:** Approve 2 weeks for 1 engineer to write the detailed Terraform config and run a proof-of-concept migration on staging."
- **Scoring notes:** Look for: dollar amounts (not "save money"), specific infrastructure named, phased timeline with durations, the biggest risk stated proactively, and a specific ask. Deduct for: vague cost comparisons, "we could use various AWS services," no risk section, or asking for full migration approval instead of incremental commitment.

### S-14
- **Level:** 5
- **Situation:** You just discovered that a competitor launched a feature nearly identical to what you've been building for 3 months. Your team is demoralized. You need to post in Slack to reframe the situation.
- **Role:** Product lead at a 20-person startup.
- **Audience:** Your engineering and design team (15 people).
- **Goal:** Reframe the situation from "we lost" to "this validates our direction" and redirect energy toward shipping.
- **Word limit:** 120 words.
- **Gold standard:** "Team — you've probably seen that [Competitor] launched [feature] today. I'll be honest: it stings to see someone else ship what we've been building.\n\nBut here's what I see: they just validated that this feature is worth building. Their version is good — not great. Looking at their changelog, they're missing [specific gap 1] and [specific gap 2], both of which we solve.\n\nWe're 3 weeks from launch. The move isn't to panic-pivot. The move is to ship what we have, which is better, and let our users make the comparison.\n\nI'm moving our launch date up by one week. I'll share the adjusted timeline by EOD.\n\nYou built something worth copying. Now let's ship it."
- **Scoring notes:** Look for: honest acknowledgment of the emotional impact, specific competitive gaps (not vague "we're better"), a concrete action (moved launch up), and a rallying close. Deduct for: minimizing the team's feelings, vague differentiation, no action plan, or corporate-speak ("we need to stay focused on our north star").

### S-15
- **Level:** 5
- **Situation:** You're writing the "About" section for your developer tool's documentation site. The tool is a code search engine that's faster than grep for large monorepos.
- **Role:** Creator and lead maintainer.
- **Audience:** Developers evaluating whether to adopt the tool.
- **Goal:** Explain what it is, why it exists, and why it's different — in the time it takes to decide whether to keep reading.
- **Word limit:** 100 words.
- **Gold standard:** "[Tool] is a code search engine built for monorepos. It indexes your entire codebase into a trigram index, then searches it in constant time regardless of repo size.\n\nWhy it exists: grep and ripgrep are fast enough below 100k files. Above that, they slow linearly with repo size. At 500k files, a regex search takes 30+ seconds. [Tool] takes 50ms for the same query because it searches the index, not the files.\n\nTrade-off: the initial index build takes 2-5 minutes depending on repo size. After that, incremental updates are sub-second."
- **Scoring notes:** Look for: a clear one-line definition, a benchmark comparison against known tools, an honest trade-off disclosure, and specific numbers. Deduct for: marketing language ("blazingly fast"), no comparison to alternatives, hiding the trade-off, or assuming the reader already knows why they need this.

---

## Levels 6-7 (Advanced)

### S-16
- **Level:** 6
- **Situation:** You're writing a cold email to a VP of Product at a Series B company. You've noticed their mobile app has a 2.1 star rating on the App Store, with reviews mentioning slow load times. Your company sells mobile performance monitoring.
- **Role:** Founder of a B2B SaaS company.
- **Audience:** VP of Product who is probably aware of the ratings but may not know the root cause.
- **Goal:** Start a conversation without being condescending about their app rating.
- **Word limit:** 70 words.
- **Gold standard:** "Hi [Name] — I've been looking at [App]'s recent App Store reviews. Several mention slow load times, especially on the transaction history screen. That pattern usually traces back to one of three things: uncompressed image payloads, synchronous network calls on the main thread, or missing pagination on list endpoints. We help teams like [similar company] diagnose and fix exactly this — typically cutting load times by 60%+ in the first sprint. Worth a 15-minute look?"
- **Scoring notes:** Look for: specific observation from the app (not generic "I noticed your app"), technical credibility (three plausible root causes), a proof point, and a low-friction CTA. Deduct for: condescending tone ("your app is struggling"), vague claims ("we can help"), or no demonstration of technical understanding.

### S-17
- **Level:** 6
- **Situation:** Your SaaS product had a 4-hour outage that affected all customers. The root cause was a database migration that ran during peak hours. You need to write the external-facing incident postmortem.
- **Role:** CTO of a 50-person SaaS company.
- **Audience:** Customers (mix of technical and non-technical), published on your status page.
- **Goal:** Rebuild trust through transparency. No weasel words.
- **Word limit:** 250 words.
- **Gold standard:** "## Incident Postmortem: 4-Hour Outage on March 15\n\n**Summary:** On March 15, between 10:00 AM and 2:00 PM UTC, all users experienced errors when accessing the application. The root cause was a database schema migration that locked a critical table during peak usage hours.\n\n**What happened:** At 9:58 AM, an engineer ran a migration that added an index to the `transactions` table (280M rows). On our database version, this operation acquired an exclusive lock, blocking all reads and writes to the table. We did not discover this until monitoring alerts fired at 10:07 AM. The migration completed at 1:42 PM, and service recovered by 2:00 PM.\n\n**What we got wrong:**\n1. The migration was run during peak hours — we lacked a policy requiring off-peak execution for locking operations\n2. Our staging database has 50k rows, not 280M — the migration completed in 2 seconds there, masking the production impact\n3. We had no mechanism to cancel a running migration without risking data corruption\n\n**What we're changing:**\n1. All schema migrations now require a locking-impact review and must run during our maintenance window (Sundays 4-6 AM UTC)\n2. We're adding a staging dataset that mirrors production volume (280M+ rows)\n3. We're implementing online schema migration tooling (gh-ost) that avoids table locks entirely\n\n**Timeline for fixes:** Items 1 and 2 ship this week. Item 3 ships by April 15.\n\nWe take reliability seriously, and this outage fell below our own standard. If you have questions, email me directly at [email]."
- **Scoring notes:** Look for: exact timeline, specific technical explanation (not "database issues"), numbered list of what went wrong, numbered list of fixes with dates, and personal accountability (CTO's direct email). Deduct for: passive voice ("mistakes were made"), vague fixes ("we'll improve our processes"), no timeline for remediation, or corporate apology without substance.

### S-18
- **Level:** 6
- **Situation:** You're interviewing for a principal engineer role. The interviewer asks: "Tell me about a time you made a technical decision you later regretted, and what you learned from it."
- **Role:** Principal engineer candidate with 12 years of experience.
- **Audience:** VP of Engineering evaluating your judgment and self-awareness.
- **Goal:** Demonstrate that you can own mistakes, learn from them, and apply those lessons at scale.
- **Word limit:** 150 words.
- **Gold standard:** "Two years ago, I chose to build our own service mesh instead of adopting Istio. My reasoning was sound at the time — Istio was resource-heavy and our cluster was small. But I underestimated the maintenance burden. Within a year, we had one engineer spending 30% of their time on mesh bugs instead of product work, and we'd reimplemented features that Istio ships out of the box.\n\nThe lesson wasn't 'always use the off-the-shelf tool.' It was that I evaluated the build decision against today's team size but not next year's. A 4-person team can maintain custom infra. A 12-person team doing that is wasting leverage.\n\nI've since adopted a framework: for any build-vs-buy decision, I project the maintenance cost at 3x our current team size. If the custom solution doesn't still make sense at that scale, we buy."
- **Scoring notes:** Look for: a specific technical decision (not a vague "process improvement"), quantified impact (30% of an engineer's time), a nuanced lesson (not just "I should have used Istio"), and a reusable framework that shows growth. Deduct for: a "mistake" that's actually a humble-brag, vague lessons ("I learned to communicate better"), or not quantifying the cost of the wrong decision.

### S-19
- **Level:** 6
- **Situation:** You're writing the product changelog for a major release. The release includes 3 new features, 2 breaking changes, and 5 bug fixes. Your users are developers who integrate your API.
- **Role:** Developer experience lead.
- **Audience:** Developers who depend on your API in production.
- **Goal:** Communicate everything clearly, prioritizing what requires action from the reader.
- **Word limit:** 200 words.
- **Gold standard:** "# v3.0 Release Notes\n\n## Action required\n\n**Breaking:** The `user.created` webhook payload now includes `organization_id` as a required field. If your handler validates payload shape, update your schema. Migration guide: [link]\n\n**Breaking:** Rate limits on `/search` tightened from 100 req/s to 30 req/s per API key. If you're above 30 req/s, request a limit increase before upgrading: [link]\n\n## New\n\n**Batch operations** — Create, update, or delete up to 500 records in a single API call. Reduces round trips for bulk imports from N calls to 1. Docs: [link]\n\n**Webhook retry dashboard** — See failed deliveries, inspect payloads, and manually retry from the UI. No more guessing whether a webhook fired.\n\n**Field-level permissions** — Restrict API key access to specific response fields. Your frontend key can read `user.name` without exposing `user.email`.\n\n## Fixed\n\n- CSV export no longer truncates at 10k rows (now supports up to 1M)\n- Pagination cursor no longer breaks when records are deleted mid-page\n- `updated_at` timestamp now reflects actual modification time, not cache refresh time\n- Webhook signatures validate correctly for payloads containing UTF-8 characters\n- Rate limit headers now return correct `X-RateLimit-Remaining` value (was off by one)"
- **Scoring notes:** Look for: breaking changes listed first with "action required" framing, each change explains the user impact (not just what changed), links to migration guides, bug fixes stated as before/after behavior. Deduct for: burying breaking changes below new features, no migration links, feature descriptions that read like internal commit messages, or bug fixes described as "fixed an issue with..."

### S-20
- **Level:** 7
- **Situation:** You've been asked to write a 200-word brief proposing a new engineering initiative: implementing feature flags across all services. The VP of Engineering will use this to decide whether to allocate a team to the project.
- **Role:** Staff engineer.
- **Audience:** VP of Engineering who manages a 60-person engineering org.
- **Goal:** Get a "yes, staff a team" decision. The brief must survive being forwarded to the CEO.
- **Word limit:** 200 words.
- **Gold standard:** "## Proposal: Company-wide Feature Flags\n\n**The problem we're solving:** Today, shipping a feature means deploying code. This couples release timing to deploy timing, which means: (1) any feature that needs business-side coordination (sales enablement, marketing launch) requires freeze windows and calendar alignment, (2) rolling back a bad feature requires rolling back the entire deploy, risking unrelated regressions, (3) we can't run controlled experiments — it's all-or-nothing for every user.\n\n**What changes:** Every new feature ships behind a flag. Flags are toggled in a dashboard, not in code deploys. This decouples 'code is deployed' from 'users see the feature.'\n\n**Measurable impact:**\n- Deploy frequency can increase (smaller, safer deploys) — target: daily deploys per team vs. current weekly\n- Rollback time drops from 15 min (full deploy) to 5 sec (flag toggle)\n- Product and sales can control launch timing without engineering involvement\n\n**Cost:** 2 engineers, 4 weeks to integrate LaunchDarkly across 8 services. Ongoing cost: $450/month for the platform.\n\n**Risk:** Flag sprawl — stale flags accumulate. Mitigation: automated weekly reports of flags older than 30 days with no toggle activity.\n\n**Ask:** Approve 2 engineers for 4 weeks starting next sprint."
- **Scoring notes:** Look for: the problem stated in business terms (not just technical), measurable before/after impact, honest cost with specific numbers, a named risk with mitigation, and a precise ask. Deduct for: assuming the reader knows what feature flags are without explaining the value, vague cost ("some engineering time"), no risk section, or an ask that's too large for a 200-word proposal.

### S-21
- **Level:** 7
- **Situation:** You're a founder writing a LinkedIn post about a painful lesson from your first year of building. Your startup burned through $80K in 4 months building a feature your users didn't ask for.
- **Role:** First-time founder with hard-won lessons.
- **Audience:** Other founders and builders on LinkedIn (expecting typical "lessons learned" posts).
- **Goal:** Write something honest enough that other founders save it and share it.
- **Word limit:** 150 words.
- **Gold standard:** "We spent $80K building a feature nobody asked for.\n\nThe logic seemed airtight: our analytics showed users spending 40 minutes on a task our automation could cut to 5 minutes. Four months of engineering later, we shipped it.\n\nAdoption: 3%.\n\nWe called the non-adopters. Their answer was humbling: 'That 40 minutes is when I review the data. I don't want it automated. I want it organized better.'\n\nWe'd measured time-on-task and assumed it was a problem. It was actually where our users did their most valuable thinking.\n\nThe $80K lesson: analytics tell you what people do. Only conversations tell you why.\n\nWe rebuilt the feature as an organized workspace instead of an automation. Adoption: 67%.\n\nIf you're about to build something because your dashboard says users are 'struggling' — call five of them first. Their answer might save you four months."
- **Scoring notes:** Look for: specific dollar amount and timeline, a data-driven mistake (not just "we didn't listen"), the customer's voice in their own words, a reusable principle (analytics show what, not why), and the redemption arc (the rebuild that worked). Deduct for: vague numbers, lessons that are obvious ("talk to your customers"), no concrete example, or humble-bragging disguised as vulnerability.

### S-22
- **Level:** 7
- **Situation:** You're writing the "Why we built this" section of a technical blog post announcing your new open-source library. The library solves a real problem — making database migrations reversible by default.
- **Role:** Library author and senior engineer.
- **Audience:** Developers who have been burned by irreversible migrations.
- **Goal:** Convince the reader that this library is worth the 10 minutes it takes to read the docs.
- **Word limit:** 150 words.
- **Gold standard:** "Every migration tool promises safety. None of them enforce it.\n\nHere's what actually happens: you write an `up` migration. You skip the `down` because you're shipping fast. Six months later, a migration breaks production and you need to roll back — but there's no down migration for the last 40 commits. Your options are: fix forward under pressure, or write a reverse migration from memory while your pager screams.\n\nWe built [library] because we got tired of this pattern. It works differently: you write your migration as a pair of operations (create/drop, add/remove, rename from/to). The library generates both the forward and reverse migration from the same declaration. If you can't express the reverse, it won't let you migrate.\n\nThis means every migration in your history is reversible by construction — not by discipline, which always fails under pressure.\n\nnpm install [library] and read the 3-minute quickstart: [link]"
- **Scoring notes:** Look for: a vivid pain point the reader has experienced, a critique of existing tools (not competitors by name, but the category), a clear explanation of the different approach, the key insight framed memorably ("by construction, not by discipline"), and a low-friction install command. Deduct for: marketing language, no technical substance, attacking specific competitors, or not explaining the mechanism.

### S-23
- **Level:** 7
- **Situation:** Your team just finished a quarter where you missed your main OKR (activate 500 new users) but hit 380 and discovered critical insights about your onboarding funnel.
- **Role:** Product manager.
- **Audience:** CEO and leadership team in a quarterly review meeting (written format).
- **Goal:** Present the miss honestly while demonstrating that the quarter's work positions you to hit the goal next quarter.
- **Word limit:** 200 words.
- **Gold standard:** "## Q1 Review: Activation\n\n**Result:** 380 / 500 activated users (76% of target)\n\n**Why we missed:** Our onboarding funnel has a cliff at the integration step. 72% of signups complete the profile setup, but only 31% connect their first data source. The 41-point drop happens because the OAuth flow requests write permissions that most developers won't grant without understanding why. We discovered this in week 6 and couldn't ship the fix in time.\n\n**What the miss taught us:** The activation bottleneck isn't motivation (people sign up) and it isn't product quality (people who integrate retain at 89%). It's a single trust barrier at a single step.\n\n**What we shipped anyway:**\n- Redesigned the permission explanation screen (A/B test running now, early signal: +15% on integration completion)\n- Built an integration-free demo mode so users see value before granting access\n- Instrumented the funnel end-to-end — we now have per-step conversion data we lacked in Q4\n\n**Q2 target:** 600 activated users. The permission fix alone, at the A/B test's current lift, would recover the 120-user gap and then some.\n\n**Key bet:** The trust barrier is the primary bottleneck. If the A/B test confirms the +15% lift by April 15, we double down. If not, we pivot to an invite-based onboarding model I've scoped as a backup."
- **Scoring notes:** Look for: the miss stated upfront with no spin, a specific diagnosis (not "we need to improve onboarding"), evidence that the quarter generated valuable learning, concrete shipped work, a Q2 target that shows confidence with a contingency. Deduct for: burying the miss, blaming external factors, no diagnosis of why, no forward-looking plan, or a plan with no contingency.

### S-24
- **Level:** 6
- **Situation:** You need to convince a skeptical senior engineer on your team to adopt TypeScript for a new project. They've used JavaScript for 10 years and think TypeScript is "unnecessary overhead."
- **Role:** Tech lead introducing a technology change.
- **Audience:** A senior engineer you respect, who resists the change from a position of deep experience.
- **Goal:** Shift their thinking without dismissing their experience. You have one message.
- **Word limit:** 120 words.
- **Gold standard:** "I get the resistance — you write clean JS and you catch bugs that static typing wouldn't. I'm not arguing that TypeScript makes you a better engineer. Here's what I'm arguing: it makes the other 5 engineers on the team ship fewer bugs to production. Last quarter, 4 of our 7 production incidents were type-related — undefined property access on an object that had a different shape than the caller expected. TypeScript catches all 4 at compile time. The overhead is real: 10-15% slower to write initially, some wrestling with generics. But we'll spend less time debugging in production than we spend learning the type system. Can we try it on the notification service as a low-stakes pilot?"
- **Scoring notes:** Look for: acknowledgment of the engineer's skill (not "TypeScript is objectively better"), team-level framing (not individual), specific production incidents as evidence, honest trade-off acknowledgment, and a low-stakes pilot proposal. Deduct for: condescension, framing it as "everyone is doing it," no concrete evidence, or asking for full adoption instead of a pilot.

### S-25
- **Level:** 7
- **Situation:** You're writing the opening paragraph of a Y Combinator application. Your startup builds AI-powered code review that catches logic errors, not just style issues. You have 200 characters for the one-line description and 120 words for the "What does your company do?" section.
- **Role:** Technical co-founder applying to YC.
- **Audience:** YC partners who read 10,000+ applications per batch.
- **Goal:** Make the reader stop skimming and start paying attention within the first sentence.
- **Word limit:** One-line: 200 characters. Description: 120 words.
- **Gold standard:** "One-line: Code review that catches logic bugs, not just lint errors. AI that reads your PR like a senior engineer who knows your codebase.\n\nDescription: Current code review tools (linters, formatters, SAST scanners) catch syntax and style issues. They don't catch the bugs that actually cause outages: wrong business logic, missed edge cases, race conditions. Those bugs are caught by senior engineers — and senior engineers are expensive, slow, and don't scale.\n\nWe train a model on each customer's codebase, commit history, and past bug reports. The model learns what 'correct' looks like for that specific codebase. When a PR introduces a pattern that historically preceded a bug, it flags it with an explanation.\n\nTraction: 12 teams in private beta. 3 paying ($500/mo each). The model caught a billing logic error last week that would have cost our largest customer $40K."
- **Scoring notes:** Look for: a one-liner that differentiates from existing tools in under 200 characters, a description that names what exists, what's missing, and why, specific traction numbers, and a concrete anecdote that demonstrates value. Deduct for: jargon-heavy one-liners, descriptions that start with "We leverage AI to..." no traction data, or hypothetical impact claims.
