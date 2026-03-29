# Boss Challenge Bank

> 10 curated BOSS challenges. Unlocks at Level 4.
> Each boss combines multiple skills in a multi-part challenge with escalating difficulty.
> These are the hardest challenges in the game — completing one is a genuine accomplishment.

---

### B-1
- **Level:** 4
- **Theme:** Value proposition clarity + cold outreach + audience adaptation.
- **Part 1:**
  - **Challenge:** "Your B2B SaaS product automates invoice reconciliation for e-commerce companies. Write a one-sentence value proposition that would work as a homepage headline. No jargon, no buzzwords, no 'leverage' or 'streamline.'"
  - **Gold standard:** "We match your invoices to your bank transactions automatically — so your finance team closes the books in hours, not days."
  - **Scoring notes:** Must name the specific action (match invoices to transactions), the user (finance team), and the measurable outcome (hours vs. days). Reject anything that could describe a different product.
- **Part 2:**
  - **Challenge:** "Now write an 80-word cold email to the CFO of a 200-person e-commerce company using that value proposition. The CFO cares about accuracy and audit readiness, not speed."
  - **Gold standard:** "Hi [Name] — finance teams at companies your size typically reconcile 2,000-5,000 transactions per month manually. The error rate on manual matching hovers around 3-4%, and each error creates an audit trail gap. We automate the matching with 99.7% accuracy and generate an audit-ready reconciliation report for every closing cycle. Your team at [Company] processes roughly [X] orders/month on Shopify — I can show you exactly what automated reconciliation looks like for that volume. 15 minutes?"
  - **Scoring notes:** Must adapt the value prop to the CFO's priorities (accuracy + audit, not speed). Must include a specific number or benchmark. The company reference should feel researched, not templated. Reject emails that lead with speed when the brief says the CFO cares about accuracy.
- **Part 3:**
  - **Challenge:** "The CFO replies: 'Interesting, but our accountant has a system that works fine. What's the ROI?' Write a 60-word response that answers the objection without being pushy."
  - **Gold standard:** "That's fair — if the current system works, the bar for switching should be high. The ROI question comes down to two things: how many hours per month does reconciliation take, and what does one undetected error cost during an audit? Our customers in your revenue range typically recover 15-20 hours/month and eliminate audit findings entirely. Worth a quick comparison?"
  - **Scoring notes:** Must validate the objection genuinely (not dismissively). Must reframe ROI in terms the CFO measures (hours and audit risk). Must end with a low-pressure CTA. Reject responses that ignore the "our system works fine" objection or attack the accountant's process.

### B-2
- **Level:** 4
- **Theme:** Technical writing precision + audience code-switching.
- **Part 1:**
  - **Challenge:** "Your team just shipped a new feature: real-time collaborative editing in your web app (like Google Docs). Write a 50-word technical explanation of how it works for your engineering blog. Audience: senior engineers."
  - **Gold standard:** "We use CRDTs (Conflict-free Replicated Data Types) for real-time collaboration. Each client maintains a local replica of the document. Edits are encoded as operations with Lamport timestamps and broadcast via WebSocket. CRDTs guarantee convergence — all clients reach the same state regardless of operation order or network delays, with no central coordination."
  - **Scoring notes:** Must name the specific technology (CRDTs), the mechanism (Lamport timestamps, WebSocket), and the key property (convergence without central coordination). Reject vague explanations ("we use real-time sync technology").
- **Part 2:**
  - **Challenge:** "Now rewrite the same feature explanation in 50 words for the product changelog. Audience: non-technical users who just want to know what they can do now."
  - **Gold standard:** "You can now edit documents with your team in real time. Everyone sees changes as they happen — no more emailing versions back and forth or worrying about overwriting someone's work. Just share the link, start typing together, and the document stays in sync automatically."
  - **Scoring notes:** Must describe the same feature with zero technical jargon. Must focus on the user's experience, not the implementation. Must solve a pain point the user recognizes ("emailing versions back and forth"). Reject explanations that mention CRDTs, WebSocket, or any implementation detail.

### B-3
- **Level:** 5
- **Theme:** Diagnosis + proposal + stakeholder communication.
- **Part 1:**
  - **Challenge:** "Your SaaS app's dashboard page takes 8 seconds to load. Product is getting complaints. Write a 100-word Slack message to your tech lead diagnosing the problem and proposing three investigation areas."
  - **Gold standard:** "Looked into the dashboard load time. The page makes 23 API calls on mount — 7 of them are sequential (each waits for the previous one to return). Three areas to investigate: (1) Parallelize the 7 sequential calls — at least 4 of them have no data dependency on each other. (2) The /analytics/summary endpoint alone takes 3.2 seconds — it's computing aggregates on every request instead of reading from a materialized view. (3) The frontend renders all 12 dashboard widgets at once — we could lazy-load below-the-fold widgets. I'd start with #2 since it's the single biggest contributor."
  - **Scoring notes:** Must include specific evidence (23 API calls, 7 sequential, 3.2s endpoint), three distinct investigation areas, and a prioritized recommendation. Reject vague diagnoses ("the page has too many requests") or proposals without prioritization.
- **Part 2:**
  - **Challenge:** "Your tech lead approves investigation area #2. Write a 100-word Jira ticket description for the materialized view optimization. Include acceptance criteria."
  - **Gold standard:** "## Optimize /analytics/summary with materialized view\n\nThe /analytics/summary endpoint computes dashboard aggregates (total revenue, active users, event counts) from raw tables on every request. At our current data volume (2.3M events), this takes 3.2 seconds.\n\nProposed fix: Create a materialized view that pre-computes these aggregates. Refresh the view every 5 minutes via pg_cron.\n\nAcceptance criteria:\n- [ ] /analytics/summary responds in <200ms (p95)\n- [ ] Dashboard data is at most 5 minutes stale (document this in the UI with a 'last updated' timestamp)\n- [ ] Materialized view refresh completes in <10 seconds and doesn't lock the source tables"
  - **Scoring notes:** Must include current state with numbers (2.3M events, 3.2s), a specific technical approach (materialized view + pg_cron), and measurable acceptance criteria with thresholds. Reject tickets that say "make it faster" without defining success.
- **Part 3:**
  - **Challenge:** "The fix ships and dashboard load time drops from 8s to 1.4s. Write a 60-word update for the #product Slack channel that the whole company can understand — engineering, sales, support, everyone."
  - **Gold standard:** "Dashboard load time: 8 seconds -> 1.4 seconds. Your customers' dashboards now load 5x faster. The biggest impact is on accounts with high event volumes — they were waiting the longest. If any customer mentions slow dashboards in a support ticket, that's a stale complaint — ask them to try again and the experience should be noticeably different."
  - **Scoring notes:** Must translate the technical achievement into customer impact. Must include actionable information for non-engineering teams (support can redirect stale complaints). Reject updates that only describe the technical change without business context.

### B-4
- **Level:** 5
- **Theme:** Product thinking + concise writing + persuasion.
- **Part 1:**
  - **Challenge:** "You're building a developer tool that generates API documentation from code comments. Write a 40-word product description that would work as the first paragraph on your landing page."
  - **Gold standard:** "Write a code comment. Get a docs page. Our tool scans your codebase, extracts structured comments from your endpoints, and publishes a searchable documentation site — synced to your repo, updated on every push, zero manual formatting."
  - **Scoring notes:** Must open with the simplest possible framing of the user action and the result. Must name the mechanism without jargon. Must include the key differentiator (auto-synced, zero manual work). Reject descriptions that start with "We are a platform that..."
- **Part 2:**
  - **Challenge:** "A developer on Hacker News comments: 'How is this different from Swagger/OpenAPI? Serious question.' Write a 60-word response that takes the question seriously and differentiates without attacking the competitor."
  - **Gold standard:** "Good question. Swagger requires you to maintain a separate spec file (YAML/JSON) alongside your code. Specs drift from implementation unless someone manually keeps them in sync. We generate docs directly from your code comments — the documentation is the code, not a file next to the code. Trade-off: we're less flexible than a full OpenAPI spec. Advantage: your docs are never stale."
  - **Scoring notes:** Must take the question genuinely seriously (no dismissiveness). Must explain the specific architectural difference (inline comments vs. separate spec file). Must acknowledge a trade-off (less flexible). Reject responses that trash Swagger or claim to be "better in every way."
- **Part 3:**
  - **Challenge:** "Write a 50-word response to a different HN comment: 'Nice, but I'll never trust auto-generated docs. They always miss the edge cases and context that matter.' This person isn't wrong."
  - **Gold standard:** "You're right — auto-generated docs without context are API reference masquerading as documentation. That's why we support `@context` tags: inline annotations where you explain the why, the gotchas, and the edge cases in your own words. The tool handles the structure and formatting. You handle the knowledge. Both are required."
  - **Scoring notes:** Must validate the criticism genuinely (the person has a real point). Must explain how the product addresses it without claiming to solve it entirely. The "both are required" framing is key — it's honest and positions the tool as an aid, not a replacement. Reject responses that dismiss the concern or claim AI solves the edge-case problem.

### B-5
- **Level:** 5
- **Theme:** Investor communication + metric storytelling + ask formulation.
- **Part 1:**
  - **Challenge:** "Your startup has $18K MRR, 47 customers, and a 94% monthly retention rate. Write a 40-word traction summary for the opening of a pitch deck slide."
  - **Gold standard:** "$18K MRR across 47 customers. 94% monthly retention — meaning a customer who signs up today has a 48% chance of still paying us two years from now. We've grown 22% month-over-month for the last 4 months with zero paid acquisition."
  - **Scoring notes:** Must present all three numbers. The retention calculation (compounding 94% monthly to show 2-year retention) demonstrates metric fluency. The "zero paid acquisition" detail signals capital efficiency. Reject summaries that just list the numbers without context or implication.
- **Part 2:**
  - **Challenge:** "An investor asks: 'Your retention is great, but 47 customers isn't enough to know if this scales. How do you think about that?' Write a 70-word response."
  - **Gold standard:** "You're right that 47 is a small sample. Two things give me confidence it's signal and not noise: First, our retention is consistent across cohorts — January customers retain at 93%, February at 95%, March at 94%. It's not one sticky cohort masking churn elsewhere. Second, our top 10 customers by usage have expanded their seats 2.3x on average. Retention plus expansion in the same accounts is hard to fake."
  - **Scoring notes:** Must validate the investor's concern (not "47 is plenty"). Must provide cohort-level data, not just the aggregate number. The expansion metric is the clincher — it shows organic growth within accounts. Reject responses that deflect the concern or cite vanity metrics.
- **Part 3:**
  - **Challenge:** "Now write the ask slide: 60 words explaining what you'll do with $1.5M in funding."
  - **Gold standard:** "Raising $1.5M to do three things: (1) Hire 2 engineers to build the self-serve onboarding that our sales-assisted model can't scale past 100 customers ($600K, 12 months). (2) Hire 1 demand-gen marketer to test paid channels now that organic has plateaued ($250K, 12 months). (3) Extend runway to 20 months ($650K reserve). Target: $80K MRR and 200 customers by month 18."
  - **Scoring notes:** Must allocate dollars to specific hires with specific purposes (not "grow the team"). Must include a runway buffer (investors want to know you plan for contingencies). Must state a target outcome tied to a timeline. Reject asks that say "hire great people" without specifying roles or "scale the product" without numbers.

### B-6
- **Level:** 6
- **Theme:** Crisis communication under pressure + audience adaptation.
- **Part 1:**
  - **Challenge:** "Your payment processing is down. It's been 45 minutes. You don't know the root cause yet. Write a 50-word status page update that is honest without causing panic."
  - **Gold standard:** "We're investigating an issue affecting payment processing. Payments initiated in the last 45 minutes may not have completed — no duplicate charges have occurred. Our engineering team is actively diagnosing the root cause. Next update in 30 minutes or sooner if we have a resolution. Status: Investigating."
  - **Scoring notes:** Must state the impact clearly (payments may not have completed), address the customer's biggest fear (duplicate charges), commit to a next-update time, and use a status label. Reject updates that say "experiencing issues" without specifying the impact, or that promise a fix timeline when the root cause is unknown.
- **Part 2:**
  - **Challenge:** "30 minutes later, you've found the root cause: a third-party payment gateway deployed a breaking API change without notice. The fix is to pin to the previous API version. ETA: 20 minutes. Write a 70-word update for the status page."
  - **Gold standard:** "Root cause identified: our payment gateway provider deployed a breaking API change that rejected our transaction format. We're rolling back to the previous API version now. ETA for full recovery: 20 minutes from this update. Impact so far: ~180 transactions are queued and will process automatically once the fix is live. No transactions have been lost or double-charged. Next update in 20 minutes."
  - **Scoring notes:** Must name the root cause specifically (third-party breaking change, not "external dependency issue"), provide an ETA, quantify the impact (180 queued transactions), and reassure on data integrity (no loss, no double charges). Reject updates that blame the third party aggressively or provide a vague ETA.
- **Part 3:**
  - **Challenge:** "Payments are restored. Write a 60-word internal Slack message to the customer success team so they can handle incoming support tickets. Different audience, different information needs."
  - **Gold standard:** "Payments are back up. Here's what CS needs to know: (1) ~180 transactions were queued during the outage — they've all processed successfully now. (2) No customers were double-charged. (3) If a customer says their payment 'failed,' ask them to check their account — it likely went through during the queue drain. (4) If anyone asks for a root cause: our payment provider pushed a breaking change; we've pinned to a stable version and are working with them to prevent recurrence."
  - **Scoring notes:** Must translate the technical incident into customer-facing talking points. Must anticipate the specific questions CS will receive (double charges, failed payments that actually succeeded). The numbered format is critical for a team that needs to scan quickly during high-ticket-volume situations. Reject messages that give the CS team a technical play-by-play instead of actionable guidance.

### B-7
- **Level:** 6
- **Theme:** Hiring communication + evaluation + decision-making.
- **Part 1:**
  - **Challenge:** "You're hiring a senior frontend engineer. Write a 100-word job description section called 'What you'll actually do' that is specific enough for a candidate to self-select in or out. No generic 'collaborate with cross-functional teams.'"
  - **Gold standard:** "What you'll actually do:\n\nOwn the entire dashboard experience — from the charting library to the data-fetching layer. Our dashboard renders 50+ interactive charts built on D3, pulling from a GraphQL API that returns large datasets (100k+ points). Your first project: rebuild the chart rendering pipeline to support streaming data updates without re-rendering the entire SVG.\n\nYou'll work in TypeScript + React. You'll write your own performance benchmarks. You'll review every frontend PR. The team is 3 frontend engineers and you'd be the most senior — which means you set the patterns everyone follows."
  - **Scoring notes:** Must describe a specific first project (not "work on exciting challenges"). Must name the tech stack precisely. Must indicate scope and seniority clearly. The "self-select" requirement means someone who doesn't enjoy D3 or performance work should read this and say "not for me." Reject descriptions that could apply to any frontend role at any company.
- **Part 2:**
  - **Challenge:** "A strong candidate asks in the interview: 'What's the hardest part of working here that you wouldn't put in the job description?' Write a 70-word honest answer that doesn't scare them off but doesn't sugarcoat either."
  - **Gold standard:** "The hardest part is context-switching. We're 20 people, so you'll sometimes drop a complex rendering problem to debug a customer-reported CSS issue in a browser you've never tested in. There's no dedicated QA team. You'll ship something beautiful on Monday and spend Tuesday hunting a Safari-only flexbox bug. If you need long, uninterrupted focus blocks every day, that's genuinely hard to protect here. We're working on it — but I won't pretend it's solved."
  - **Scoring notes:** Must name a real, specific difficulty (not "we work hard"). Must be honest without being defeatist ("we're working on it — but I won't pretend it's solved" is the right balance). Must be specific to this company, not generic startup problems. Reject answers that are secretly humble-brags ("the hardest part is how fast we ship") or that name a problem and immediately claim it's fixed.
- **Part 3:**
  - **Challenge:** "After the interview loop, the team's feedback is split: the hiring manager says 'strong hire,' one panelist says 'hire,' and one says 'no hire — the system design answers were too theoretical, not enough production experience.' Write a 70-word recommendation to the VP of Engineering."
  - **Gold standard:** "Recommendation: Hire with a scoped 30-day evaluation.\n\nThe theoretical system design concern is valid — her answers were architecturally sound but didn't reference production trade-offs (caching invalidation, monitoring, failure modes). However, her D3 live-coding was the strongest we've seen in 6 months, and her code review exercise caught the performance bug that 3 previous candidates missed.\n\nProposed evaluation: assign the chart streaming project. It requires both her D3 strength and the production-systems thinking we're uncertain about. If the first PR shows monitoring and error handling considerations, the concern is resolved."
  - **Scoring notes:** Must acknowledge the dissenting feedback specifically (not "there were some concerns"). Must cite concrete evidence from the interview (live-coding, code review exercise). Must propose a structured evaluation rather than just "hire" or "don't hire." Reject recommendations that dismiss the no-hire panelist's feedback or recommend hiring without addressing the concern.

### B-8
- **Level:** 6
- **Theme:** Strategic writing + metric framing + executive communication.
- **Part 1:**
  - **Challenge:** "Your freemium SaaS product has 12,000 free users and 340 paying customers ($49/month plan). The CEO asks: 'Is freemium working?' Write a 60-word answer that uses data, not opinion."
  - **Gold standard:** "Freemium is working as acquisition, not as conversion. 78% of our paying customers started on free — so it's our best top-of-funnel channel. But the free-to-paid conversion rate is 2.8%, and the median time-to-convert is 67 days. For context, best-in-class freemium SaaS converts at 5-7%. We're acquiring well but leaving conversion on the table."
  - **Scoring notes:** Must answer the question with a nuanced position (not just "yes" or "no"). Must cite specific metrics (conversion rate, time-to-convert). Must provide a benchmark for context. Reject answers that are purely positive ("yes, 12,000 users!") or purely negative ("only 2.8% convert").
- **Part 2:**
  - **Challenge:** "The CEO replies: 'OK, what would you change?' Write a 80-word recommendation with a specific experiment you'd run to improve free-to-paid conversion."
  - **Gold standard:** "The 67-day median time-to-convert tells me free users aren't hitting the value ceiling fast enough — they can do everything they need on the free plan for two months before feeling constrained. I'd run one experiment: lower the free plan's project limit from 10 to 3. This forces users to hit the upgrade wall in their first week instead of their third month. We measure: (1) conversion rate change, (2) free-user activation rate (to make sure we're not killing top-of-funnel), (3) time-to-convert. Run it for 6 weeks on 50% of new signups."
  - **Scoring notes:** Must diagnose why conversion is low (value ceiling too far away), propose a specific experiment (not "improve onboarding"), define success metrics, and include a safeguard metric (activation rate). Reject recommendations that are generic ("add more premium features") or that don't include a measurement plan.
- **Part 3:**
  - **Challenge:** "Write a 50-word Slack message to the product team announcing this experiment without it sounding like a mandate from the CEO."
  - **Gold standard:** "Team — I want to test a hypothesis: our free plan is too generous, and that's why free-to-paid conversion sits at 2.8%. Proposed experiment: reduce the project limit from 10 to 3 for 50% of new signups over 6 weeks. Goal: find the constraint that makes free users discover the paid value sooner. I'd love input on the experiment design before we ship it — anything I'm not seeing?"
  - **Scoring notes:** Must frame it as a hypothesis to test (not a decision made). Must invite input genuinely (not "let me know if you have concerns," which is a fake invitation). Must include enough context that the team understands the reasoning. Reject messages that sound like orders or that don't share the underlying data.

### B-9
- **Level:** 7
- **Theme:** Full product launch — from positioning to execution.
- **Part 1:**
  - **Challenge:** "You're launching a new product: an AI assistant that helps developers write better commit messages. Write a 30-word positioning statement that you'd put above the fold on the landing page."
  - **Gold standard:** "Stop writing commit messages that say 'fix stuff.' Our AI reads your diff and drafts a message that explains what changed and why — in your team's style."
  - **Scoring notes:** Must open with a pain point the reader recognizes ("fix stuff"). Must explain the mechanism in one sentence (reads your diff). Must include the differentiator (adapts to the team's style). Reject positioning that uses generic AI language ("AI-powered," "intelligent") or that doesn't reference a specific user pain.
- **Part 2:**
  - **Challenge:** "Write the launch tweet (under 280 characters) that a developer would retweet."
  - **Gold standard:** "We built an AI that writes your commit messages by reading your diffs. It learned from 1M+ open-source commits. It knows the difference between 'refactor' and 'rewrite.' It matches your team's style. Free for public repos. [link]"
  - **Scoring notes:** Must be concise and specific. The "refactor vs. rewrite" detail demonstrates the product actually understands code semantics. "Free for public repos" is the growth mechanic. Reject tweets that are generic ("Excited to announce...") or that don't include a concrete detail that demonstrates the product's intelligence.
- **Part 3:**
  - **Challenge:** "A skeptical developer replies to your tweet: 'Cool demo but I'll bet it writes generic messages for any non-trivial diff. What happens when I rename a function across 40 files?' Write a 50-word reply."
  - **Gold standard:** "Fair challenge. For a rename-across-40-files diff, it generates something like: 'Rename calculateTax -> computeSalesTax across 40 files. Updates all call sites, test fixtures, and doc references. No logic changes.' It detects the pattern (rename) and doesn't describe each file change individually. Try it on a real refactor PR — genuinely curious if it holds up."
  - **Scoring notes:** Must give a concrete example of the generated message (not "it handles it well"). Must show the product understands diff patterns (rename detection). Must invite testing without being defensive ("genuinely curious if it holds up" shows confidence without arrogance). Reject replies that dodge the question or say "great feedback, we're working on it."

### B-10
- **Level:** 7
- **Theme:** Complete strategy pivot communication — from diagnosis to execution to team alignment.
- **Part 1:**
  - **Challenge:** "Your B2B SaaS product has been targeting enterprise companies (1000+ employees) for 18 months. Sales cycles average 6 months, you've closed 4 deals, and your runway is 9 months. You've noticed that 30 self-serve signups from small teams (5-20 people) are paying $79/month with zero sales involvement. Write a 100-word memo to your co-founder arguing that you should pivot to SMB."
  - **Gold standard:** "We need to talk about pivoting downmarket. The numbers: enterprise has produced 4 deals in 18 months at a 6-month sales cycle. At our current close rate, we'll add 3 more before runway ends. That's not enough. Meanwhile, 30 SMB teams found us organically, signed up without a demo, and are paying $79/month — $2,370 MRR we didn't spend a dollar acquiring. The math: if we redirect the enterprise sales budget into self-serve growth and convert 20 SMBs/month at $79, we hit $30K MRR in 12 months. Enterprise ceiling with our resources: maybe $15K MRR in the same period. I'm not saying abandon enterprise forever. I'm saying our 9-month runway demands the path with the fastest feedback loop."
  - **Scoring notes:** Must compare both paths quantitatively (enterprise ceiling vs. SMB projection). Must acknowledge the runway constraint as the forcing function. Must be honest about what you're not saying ("not abandon enterprise forever"). Reject memos that are purely emotional or that don't include concrete projections for both paths.
- **Part 2:**
  - **Challenge:** "Your co-founder agrees. Now write a 100-word Slack message to your 8-person team explaining the pivot. Two of them were hired specifically for enterprise sales."
  - **Gold standard:** "Team — we're making a strategic shift and I want to be direct about what it means. We're moving our primary focus from enterprise to SMB self-serve. The short version: 30 SMB customers found us on their own and are paying without sales calls. With 9 months of runway, we need the growth path with the fastest signal, and that's self-serve. What this means practically: engineering priorities shift to self-serve onboarding, billing, and the features SMBs are requesting. For [Enterprise Sales 1] and [Enterprise Sales 2] — this affects your roles directly, and I want to talk with each of you individually today to discuss what the path forward looks like. You've built relationships that matter and I want to figure out together how your skills fit the new model. Team meeting tomorrow at 10 AM to walk through the roadmap."
  - **Scoring notes:** Must be direct about the change and its rationale. Must specifically address the people whose roles are most affected (by name or role). Must not be falsely cheerful or pretend the change doesn't have hard consequences. Must set concrete next steps (individual conversations, team meeting). Reject messages that are vague about the impact on the team or that don't directly address the enterprise sales team members.
- **Part 3:**
  - **Challenge:** "Write a 60-word email to your 4 enterprise prospects explaining the shift without burning the relationships. These are people you've been talking to for months."
  - **Gold standard:** "Hi [Name] — I want to be upfront about a shift in our business. We're focusing our near-term roadmap on self-serve capabilities for smaller teams, which means the enterprise-specific features we discussed (SSO, custom SLAs, dedicated support) are moving to a later timeline. I don't want to keep you waiting on commitments we can't make right now. If your timeline allows, I'd welcome continuing the conversation in Q3 when those features ship. Either way, I'm grateful for the time you've invested — your feedback shaped our product in ways that will last."
  - **Scoring notes:** Must be honest about the timeline change without saying "we're pivoting away from enterprise." Must name the specific features that are delayed. Must not burn the bridge (leave the door open for Q3). Must thank them genuinely. Reject emails that are vague ("we're making some changes"), that over-promise a return timeline, or that feel like a form letter.
