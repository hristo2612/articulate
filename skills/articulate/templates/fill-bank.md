# Fill Precision Challenge Bank

> 35 curated FILL_PRECISION challenges. Distribution: 12 for L1-2, 12 for L3-4, 11 for L5-7.
> Target words are "passive vocabulary" — words users recognize but rarely produce.

---

## Levels 1-2 (Fundamentals)

### F-1
- **Level:** 1
- **Target word:** "concise"
- **Challenge:** "The executive summary should be [___] — no more than three sentences covering the problem, the solution, and the ask."
- **Strong synonyms:** ["succinct", "terse"]
- **Acceptable:** ["brief", "short", "compact"]
- **Etymology:** From Latin *concisus* ("cut short"), past participle of *concidere* ("to cut up"). Good writing cuts away excess.
- **Register:** Professional writing, editorial feedback, style guides. The word signals you care about information density.

### F-2
- **Level:** 1
- **Target word:** "ambiguous"
- **Challenge:** "The error message 'something went wrong' is [___] — the user has no idea whether to retry, refresh, or contact support."
- **Strong synonyms:** ["vague", "equivocal"]
- **Acceptable:** ["unclear", "imprecise", "nebulous"]
- **Etymology:** From Latin *ambiguus* ("having double meaning"), from *ambigere* ("to wander around"). Ambiguous text sends readers wandering.
- **Register:** Technical writing, code reviews, UX copy critique. Essential for anyone designing interfaces or APIs.

### F-3
- **Level:** 1
- **Target word:** "redundant"
- **Challenge:** "The function validates the input twice — the second check is [___] since the middleware already sanitizes the payload."
- **Strong synonyms:** ["superfluous", "duplicative"]
- **Acceptable:** ["unnecessary", "extra", "extraneous"]
- **Etymology:** From Latin *redundantem* ("overflowing"), from *redundare* ("to overflow"). Redundant code is code that spills past what's needed.
- **Register:** Code review, engineering discussions, technical writing. Calling something "redundant" is more precise than "unnecessary" because it implies duplication.

### F-4
- **Level:** 1
- **Target word:** "trivial"
- **Challenge:** "Renaming the variable is a [___] change — it touches one line and carries zero regression risk."
- **Strong synonyms:** ["negligible", "inconsequential"]
- **Acceptable:** ["minor", "small", "simple"]
- **Etymology:** From Latin *trivialis* ("commonplace"), from *trivium* ("crossroads where three roads meet") — a place everyone passes through, hence ordinary.
- **Register:** Engineering, mathematics, code review. In tech, "trivial" has a precise connotation: so simple it barely warrants discussion.

### F-5
- **Level:** 1
- **Target word:** "deprecate"
- **Challenge:** "We plan to [___] the v1 endpoint in March and remove it entirely by June, giving consumers a three-month migration window."
- **Strong synonyms:** ["sunset", "phase out"]
- **Acceptable:** ["retire", "wind down"]
- **Etymology:** From Latin *deprecari* ("to pray against, avert by prayer"). In software, we pray against old APIs by marking them for removal.
- **Register:** Software engineering, API design, changelogs. The word carries a specific lifecycle meaning: still functional but marked for removal.

### F-6
- **Level:** 2
- **Target word:** "idempotent"
- **Challenge:** "The payment webhook handler must be [___] — if Stripe sends the same event twice, we should process it once and ignore the duplicate."
- **Strong synonyms:** ["safely repeatable"]
- **Acceptable:** ["duplicate-safe", "replay-safe"]
- **Etymology:** From Latin *idem* ("same") + *potens* ("powerful"). An idempotent operation has the same power no matter how many times applied.
- **Register:** Backend engineering, API design, distributed systems. One of those words that compresses a paragraph of explanation into five syllables.

### F-7
- **Level:** 2
- **Target word:** "verbose"
- **Challenge:** "The logging is too [___] in production — we're writing 4 GB of debug-level output per hour and drowning out the actual errors."
- **Strong synonyms:** ["prolix", "long-winded"]
- **Acceptable:** ["wordy", "excessive", "noisy"]
- **Etymology:** From Latin *verbosus* ("full of words"), from *verbum* ("word"). The word itself is about words — meta-precision.
- **Register:** Engineering (log levels), writing feedback, code review. Developers know exactly what "verbose" means in logging contexts.

### F-8
- **Level:** 2
- **Target word:** "pragmatic"
- **Challenge:** "We don't need a perfect solution — we need a [___] one that ships this week and handles 90% of the cases."
- **Strong synonyms:** ["practical", "utilitarian"]
- **Acceptable:** ["realistic", "sensible", "workable"]
- **Etymology:** From Greek *pragmatikos* ("fit for business"), from *pragma* ("deed, act"). Pragmatism is philosophy rooted in action, not theory.
- **Register:** Product discussions, engineering trade-offs, business strategy. Signals you value shipping over perfection.

### F-9
- **Level:** 2
- **Target word:** "bottleneck"
- **Challenge:** "The database query is the [___] — the API responds in 12ms, but the single SQL join takes 900ms under load."
- **Strong synonyms:** ["chokepoint", "constraint"]
- **Acceptable:** ["limiting factor", "slowest link"]
- **Etymology:** Literally a bottle's narrow neck — the point where flow is physically restricted. The metaphor maps perfectly to system performance.
- **Register:** Performance engineering, product analytics, process optimization. One of the most useful metaphors in technical communication.

### F-10
- **Level:** 2
- **Target word:** "mitigate"
- **Challenge:** "We can't eliminate the risk of a third-party API outage, but we can [___] it with a 30-second local cache and a graceful fallback UI."
- **Strong synonyms:** ["alleviate", "attenuate"]
- **Acceptable:** ["reduce", "lessen", "cushion"]
- **Etymology:** From Latin *mitigare* ("to soften, make mild"), from *mitis* ("soft"). You soften a blow you can't block entirely.
- **Register:** Risk management, incident response, security. More precise than "reduce" because it implies the threat still exists — you're lessening its impact.

### F-11
- **Level:** 2
- **Target word:** "scope"
- **Challenge:** "We need to define the [___] of this project before writing any code — are we rebuilding the whole dashboard or just the charts component?"
- **Strong synonyms:** ["boundaries", "extent"]
- **Acceptable:** ["parameters", "limits", "range"]
- **Etymology:** From Greek *skopos* ("target, aim"), from *skopein* ("to look at"). Scope is what you're aiming at — and implicitly, what you're not.
- **Register:** Project management, engineering, product. "Scope creep" is the developer's most familiar compound noun.

### F-12
- **Level:** 2
- **Target word:** "iterate"
- **Challenge:** "Ship the basic version now and [___] based on real user feedback — we'll learn more from 50 beta users than from another month of internal debate."
- **Strong synonyms:** ["refine", "evolve"]
- **Acceptable:** ["improve", "adjust", "revise"]
- **Etymology:** From Latin *iterare* ("to do again"), from *iter* ("journey, way"). Each iteration is another pass along the path — not a restart, but a progression.
- **Register:** Product development, agile methodology, design. The word implies incremental improvement, not wholesale replacement.

---

## Levels 3-4 (Intermediate)

### F-13
- **Level:** 3
- **Target word:** "orthogonal"
- **Challenge:** "The billing refactor is [___] to the auth migration — they touch completely different modules, so we can run both workstreams in parallel."
- **Strong synonyms:** ["independent", "unrelated"]
- **Acceptable:** ["separate", "decoupled", "non-overlapping"]
- **Etymology:** From Greek *orthogonios* ("right-angled"). In geometry, orthogonal lines meet at 90 degrees — they go in completely different directions. In engineering, it means "no shared dependencies."
- **Register:** Software architecture, mathematics, engineering planning. Using "orthogonal" in a technical context signals architectural fluency.

### F-14
- **Level:** 3
- **Target word:** "deterministic"
- **Challenge:** "The test must be [___] — if the same input always produces the same output, we can trust the CI pipeline to catch regressions."
- **Strong synonyms:** ["reproducible", "predictable"]
- **Acceptable:** ["consistent", "repeatable"]
- **Etymology:** From Latin *determinare* ("to set bounds, limit"). A deterministic system operates within fixed bounds — no randomness, no surprises.
- **Register:** Computer science, testing, distributed systems. Calling a process "deterministic" is more precise than "predictable" because it implies a mathematical guarantee.

### F-15
- **Level:** 3
- **Target word:** "opinionated"
- **Challenge:** "Rails is an [___] framework — it makes strong default choices about file structure, ORM, and routing so you spend time building features instead of configuring tooling."
- **Strong synonyms:** ["prescriptive", "convention-driven"]
- **Acceptable:** ["structured", "guided", "standardized"]
- **Etymology:** A modern tech coinage. From "opinion" (Latin *opinionem*, "conjecture"). An opinionated tool encodes its creator's beliefs about the right way to build software.
- **Register:** Developer tooling, framework evaluation, architecture discussions. This word saves a paragraph of explanation about defaults vs. configuration.

### F-16
- **Level:** 3
- **Target word:** "egregious"
- **Challenge:** "The most [___] performance issue is the N+1 query on the users page — it fires 200 separate DB calls to render a single table."
- **Strong synonyms:** ["flagrant", "glaring"]
- **Acceptable:** ["severe", "blatant", "outrageous"]
- **Etymology:** From Latin *egregius* ("distinguished, eminent"), from *e grege* ("out of the flock"). Originally positive — so outstanding it stood apart. Ironic reversal to mean "outstandingly bad."
- **Register:** Code review, incident reports, quality assessment. Stronger than "bad" — it carries moral weight, implying the problem should have been caught.

### F-17
- **Level:** 3
- **Target word:** "canonical"
- **Challenge:** "The API documentation is the [___] source for endpoint behavior — if the Swagger spec and the README disagree, trust the Swagger spec."
- **Strong synonyms:** ["authoritative", "definitive"]
- **Acceptable:** ["official", "primary", "standard"]
- **Etymology:** From Greek *kanonikos* ("according to rule"), from *kanon* ("measuring rod, rule"). The canon is the standard everything else is measured against.
- **Register:** Engineering, documentation, data modeling. "Canonical URL," "canonical form" — the word appears constantly in technical contexts.

### F-18
- **Level:** 4
- **Target word:** "pernicious"
- **Challenge:** "Technical debt is [___] because it compounds silently — each shortcut makes the next shortcut more tempting until the codebase resists every change."
- **Strong synonyms:** ["insidious", "corrosive"]
- **Acceptable:** ["harmful", "destructive", "damaging"]
- **Etymology:** From Latin *perniciosus* ("destructive"), from *pernicies* ("ruin, death"), from *per-* ("completely") + *nex* ("violent death"). Not just harmful — harm that ruins completely.
- **Register:** Technical writing, product strategy, risk analysis. Stronger than "harmful" — implies gradual, hard-to-detect destruction.

### F-19
- **Level:** 4
- **Target word:** "spurious"
- **Challenge:** "The test failure is [___] — it passes locally but fails in CI because the container's clock drifts by a few milliseconds during timezone conversion."
- **Strong synonyms:** ["bogus", "erroneous"]
- **Acceptable:** ["false", "misleading", "phantom"]
- **Etymology:** From Latin *spurius* ("illegitimate, false"). A spurious result looks real but isn't — it has the appearance of legitimacy without the substance.
- **Register:** Testing, data analysis, debugging. More precise than "false" because it implies the result mimics a real one.

### F-20
- **Level:** 4
- **Target word:** "conflate"
- **Challenge:** "Don't [___] authentication with authorization — verifying who someone is and deciding what they can access are separate concerns that belong in separate modules."
- **Strong synonyms:** ["confuse", "merge"]
- **Acceptable:** ["mix up", "blend", "combine"]
- **Etymology:** From Latin *conflare* ("to blow together, fuse"), from *con-* ("together") + *flare* ("to blow"). Two distinct things blown into one indistinct mass.
- **Register:** Technical discussion, architecture review, philosophical argument. More precise than "confuse" because it implies the two things were actively merged, not merely misidentified.

### F-21
- **Level:** 4
- **Target word:** "preclude"
- **Challenge:** "Choosing a NoSQL database doesn't [___] relational queries — DynamoDB's new PartiQL support lets you write SQL-style queries against document data."
- **Strong synonyms:** ["prevent", "prohibit"]
- **Acceptable:** ["exclude", "rule out", "block"]
- **Etymology:** From Latin *praecludere* ("to shut off, close"), from *prae-* ("before") + *claudere* ("to close"). To preclude is to close a door before someone reaches it.
- **Register:** Technical writing, legal, product decisions. Stronger than "prevent" — it implies a categorical impossibility, not just difficulty.

### F-22
- **Level:** 4
- **Target word:** "extraneous"
- **Challenge:** "Strip all [___] fields from the API response — the client only needs user ID, name, and email, not the full database row with internal timestamps and soft-delete flags."
- **Strong synonyms:** ["superfluous", "irrelevant"]
- **Acceptable:** ["unnecessary", "extra", "unneeded"]
- **Etymology:** From Latin *extraneus* ("external, foreign"), from *extra* ("outside"). Extraneous data is data from outside the boundary of what's needed.
- **Register:** API design, data modeling, writing. More precise than "extra" because it implies the data doesn't belong here — it's foreign to this context.

### F-23
- **Level:** 4
- **Target word:** "salient"
- **Challenge:** "The most [___] finding from the user interviews is that 80% of churned customers never discovered the keyboard shortcuts — our power feature is invisible."
- **Strong synonyms:** ["prominent", "notable"]
- **Acceptable:** ["important", "key", "striking"]
- **Etymology:** From Latin *salientem* ("leaping"), present participle of *salire* ("to leap"). A salient point leaps out at you from the background noise.
- **Register:** Research presentations, executive summaries, product reviews. More vivid than "important" — it implies the finding demands attention.

### F-24
- **Level:** 4
- **Target word:** "attrition"
- **Challenge:** "User [___] accelerates after month three — if someone hasn't integrated with at least two data sources by day 90, their probability of churning doubles."
- **Strong synonyms:** ["erosion", "depletion"]
- **Acceptable:** ["loss", "churn", "decline"]
- **Etymology:** From Latin *attritionem* ("a rubbing against"), from *atterere* ("to wear away"). Attrition is loss through friction — gradual, persistent, and relentless.
- **Register:** Business analytics, HR, military strategy. More evocative than "churn" because it implies the wearing-down process, not just the departure.

---

## Levels 5-7 (Advanced)

### F-25
- **Level:** 5
- **Target word:** "ephemeral"
- **Challenge:** "The container's filesystem is [___] — any data written to disk vanishes when the pod restarts, so persistent state must go to the mounted volume."
- **Strong synonyms:** ["transient", "fleeting"]
- **Acceptable:** ["temporary", "short-lived", "volatile"]
- **Etymology:** From Greek *ephemeros* ("lasting only a day"), from *epi* ("on") + *hemera* ("day"). Originally described insects that live for a single day. In infrastructure, it describes resources designed to disappear.
- **Register:** Cloud infrastructure, Kubernetes, systems design. "Ephemeral" carries a philosophical weight that "temporary" doesn't — it implies the impermanence is by design, not accident.

### F-26
- **Level:** 5
- **Target word:** "byzantine"
- **Challenge:** "The permission system has become [___] — there are six overlapping role hierarchies, three legacy ACL tables, and a set of hardcoded exceptions that nobody fully understands."
- **Strong synonyms:** ["labyrinthine", "convoluted"]
- **Acceptable:** ["complex", "complicated", "tangled"]
- **Etymology:** From the Byzantine Empire, whose politics were legendarily intricate, full of hidden alliances and opaque power structures. The adjective preserves the sense of needless complexity masquerading as sophistication.
- **Register:** Architecture critiques, code review, organizational analysis. Carries a negative judgment that "complex" doesn't — it implies the complexity is unnecessary.

### F-27
- **Level:** 5
- **Target word:** "fungible"
- **Challenge:** "Backend engineers on this team are not [___] — swapping someone off the billing service mid-sprint costs two weeks of context transfer, not two days."
- **Strong synonyms:** ["interchangeable", "substitutable"]
- **Acceptable:** ["replaceable", "exchangeable"]
- **Etymology:** From Latin *fungi* ("to perform, enjoy"), related to *functio* ("execution"). In economics, fungible goods can substitute for each other (one dollar bill = any other dollar bill). People, it turns out, are not.
- **Register:** Economics, team management, resource planning. Using "fungible" about people (usually to argue they aren't) is a powerful rhetorical move in staffing discussions.

### F-28
- **Level:** 5
- **Target word:** "obviate"
- **Challenge:** "Adding a message queue between the services would [___] the need for the complex retry logic — if processing fails, the message stays in the queue automatically."
- **Strong synonyms:** ["eliminate", "preclude"]
- **Acceptable:** ["remove", "avoid", "prevent"]
- **Etymology:** From Latin *obviare* ("to act against, prevent"), from *ob* ("against") + *via* ("way"). To obviate is to stand in the way of a problem before it forms.
- **Register:** Technical proposals, architecture decisions, process improvement. More elegant than "eliminate the need for" — it implies the solution makes the problem structurally impossible.

### F-29
- **Level:** 6
- **Target word:** "ossified"
- **Challenge:** "The deployment process has [___] around manual steps that made sense five years ago — we still SSH into production to flip feature flags because nobody has automated it."
- **Strong synonyms:** ["calcified", "petrified"]
- **Acceptable:** ["stagnated", "rigidified", "fossilized"]
- **Etymology:** From Latin *os* ("bone") + *facere* ("to make"). Literally "turned to bone." Living tissue that was once flexible has hardened into something rigid and brittle.
- **Register:** Organizational critique, technical retrospectives, process analysis. The metaphor is visceral — it implies the process was once alive and adaptive but has hardened past the point of useful change.

### F-30
- **Level:** 6
- **Target word:** "parsimonious"
- **Challenge:** "The API design should be [___] — expose only the fields the client actually consumes, not the entire domain model."
- **Strong synonyms:** ["minimal", "lean"]
- **Acceptable:** ["economical", "spare", "frugal"]
- **Etymology:** From Latin *parsimonia* ("thrift, frugality"), from *parcere* ("to spare"). Parsimony is disciplined restraint — using only what is necessary.
- **Register:** API design, scientific methodology (Occam's razor), architecture reviews. In science, "parsimony" means preferring the simplest explanation. In engineering, it means preferring the smallest interface.

### F-31
- **Level:** 6
- **Target word:** "vacuous"
- **Challenge:** "The product vision slide is [___] — 'We empower businesses to unlock potential through innovative solutions' could describe any company in existence."
- **Strong synonyms:** ["hollow", "vapid"]
- **Acceptable:** ["empty", "meaningless", "inane"]
- **Etymology:** From Latin *vacuus* ("empty"), from *vacare* ("to be empty"). A vacuous statement has the grammatical form of meaning but the semantic content of nothing.
- **Register:** Writing critique, pitch feedback, editorial review. Stronger than "vague" — it implies the emptiness is total, not partial.

### F-32
- **Level:** 6
- **Target word:** "intractable"
- **Challenge:** "The problem seemed [___] until we reframed it — instead of trying to predict user intent, we let users tag their own sessions and built the analytics around those tags."
- **Strong synonyms:** ["unsolvable", "insurmountable"]
- **Acceptable:** ["impossible", "unmanageable", "hopeless"]
- **Etymology:** From Latin *intractabilis* ("not to be handled"), from *in-* ("not") + *tractare* ("to handle, manage"). An intractable problem resists every attempt to get a grip on it.
- **Register:** Research, engineering, product strategy. More precise than "hard" — it implies the problem resists solution in its current framing. Often the fix is reframing, not pushing harder.

### F-33
- **Level:** 7
- **Target word:** "apocryphal"
- **Challenge:** "The claim that 'users don't read documentation' is [___] — our analytics show 73% of new users visit the quickstart guide within their first session."
- **Strong synonyms:** ["unsubstantiated", "spurious"]
- **Acceptable:** ["dubious", "unverified", "mythical"]
- **Etymology:** From Greek *apokryphos* ("hidden, obscure"), from *apokryptein* ("to hide away"). Originally described religious texts of doubtful authenticity. Now means any widely-believed claim that lacks evidence.
- **Register:** Research discussions, product debates, technical writing. The word does double duty: it challenges the claim and implies the speaker has actual evidence to counter it.

### F-34
- **Level:** 7
- **Target word:** "recalcitrant"
- **Challenge:** "The legacy service is [___] — every attempt to add observability bounces off its custom logging framework, which silently swallows structured fields."
- **Strong synonyms:** ["obstinate", "resistant"]
- **Acceptable:** ["stubborn", "uncooperative", "defiant"]
- **Etymology:** From Latin *recalcitrantem* ("kicking back"), from *re-* ("back") + *calcitrare* ("to kick"), from *calx* ("heel"). A recalcitrant system kicks back when you try to change it.
- **Register:** Engineering retrospectives, system migration planning, technical proposals. Personifying a system as "recalcitrant" is more vivid and precise than "hard to change."

### F-35
- **Level:** 7
- **Target word:** "panacea"
- **Challenge:** "Microservices are not a [___] — they solve scaling and team-autonomy problems but introduce distributed tracing, network latency, and deployment orchestration challenges that monoliths don't have."
- **Strong synonyms:** ["cure-all", "silver bullet"]
- **Acceptable:** ["magic solution", "universal fix"]
- **Etymology:** From Greek *panakeia* ("universal remedy"), from *pan* ("all") + *akos* ("cure"). Panacea was the Greek goddess of universal healing — the daughter of Asclepius, god of medicine.
- **Register:** Architecture discussions, product strategy, technology evaluation. The word efficiently debunks hype — calling something "not a panacea" acknowledges its value while bounding its scope.
