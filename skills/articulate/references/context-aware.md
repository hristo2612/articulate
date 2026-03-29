# Context-Aware Sessions

## Purpose

Read the user's current project to generate sessions that use real project nouns, domain terms, and scenarios. Context scanning runs automatically whenever you invoke Articulate in a project directory — no toggle needed.

## First Time in a New Project

When the user invokes `/articulate` in a project directory that has no cached context:

1. Detect the project name from the directory name or manifest file
2. Ask: `"I notice you're working on {project}. Want me to generate sessions based on this? (yes/no)"`
3. If the user says no — skip context for this project, do NOT cache, use generic sessions
4. If the user says yes — proceed with context extraction below

Do not ask again for a project that already has a cached context file.

## What to Read

### Phase 1 — Structure scan (always, fast)

Run these before reading any files:

- List top-level files and directories in the project root
- Build a shallow directory tree (2-3 levels deep) to understand project shape
- Identify key file types (.ts, .py, .go, .rs, .swift, .java, .rb, .php) for tech stack detection

### Phase 2 — Signal files (read in priority order, stop when enough context)

1. **README.md** (or README, README.rst) — first 150 lines max
2. **Manifest files** — extract name, description, and key dependencies from the first match:
   - `package.json`, `Cargo.toml`, `pyproject.toml`, `go.mod`
   - `Gemfile`, `pom.xml`, `build.gradle`, `Package.swift`, `composer.json`
3. **CLAUDE.md** — extract project description sections only (not instructions)
4. **Source entry directories** — list top-level modules in `src/`, `lib/`, or `app/`
5. **Test patterns** — check for `test/`, `tests/`, `spec/`, `__tests__/` and identify the framework
6. **CI config** — `.github/workflows/`, `.gitlab-ci.yml` — extract pipeline stage names
7. **docs/ index** — scan for an index.md or README.md in the docs directory
8. **.env.example** (NOT .env) — read configuration shape without secrets

Stop as soon as you have enough to fill the extraction fields below. Do not read more than necessary.

## What to Extract

Build a summary containing ONLY these fields:

- **name**: Project name
- **description**: One-line description (50 words max)
- **domain**: Industry or domain (e.g., "fitness/health-tech", "developer-tools", "fintech")
- **audience**: Who uses this (e.g., "mobile app developers", "enterprise teams")
- **features**: 3-5 key features as short phrases
- **techStack**: Primary languages/frameworks (e.g., "TypeScript, React, Node.js")
- **projectStructure**: Brief directory layout description (e.g., "monorepo with packages/ and apps/")
- **keyModules**: Top-level modules or packages (e.g., ["api", "core", "cli"])
- **testFramework**: Testing framework if detected (e.g., "Jest", "pytest") or null
- **ciPipeline**: CI system and key stages (e.g., "GitHub Actions: lint, test, deploy") or null
- **dependencies**: Top 5-10 notable dependencies (libraries, not dev tooling)

## What NEVER to Include

These must NEVER appear in context summaries or generated sessions:

- **Source code** — no functions, classes, or code snippets
- **API keys** — never read .env files or any credentials
- **Environment variables** — skip .env, .env.local, .env.production
- **Credentials** — passwords, tokens, secrets, connection strings
- **Internal architecture** — no database schemas, internal APIs, or implementation details
- **Private data** — no user data, customer information, or analytics

If a README contains API keys or secrets inline (bad practice but it happens), skip those sections entirely.

## Cache Format

Save the extracted context to `~/.articulate/contexts/{project-name}.json`:

```json
{
  "name": "MoveKit",
  "description": "3D exercise animation library with REST API",
  "domain": "fitness/health-tech",
  "audience": "mobile app developers, fitness platforms",
  "features": ["3D animations", "exercise library", "API access"],
  "techStack": "Swift, Node.js, Three.js",
  "projectStructure": "monorepo with packages/api and packages/renderer",
  "keyModules": ["api", "renderer", "cli"],
  "testFramework": "Jest",
  "ciPipeline": "GitHub Actions: lint, test, deploy-staging, deploy-prod",
  "dependencies": ["three.js", "express", "prisma", "zod", "bull"],
  "cachedAt": "2026-03-29T10:00:00Z"
}
```

Rules for `{project-name}`:
- Use the project name from the manifest or directory name
- Lowercase, hyphens instead of spaces
- Example: `my-cool-project.json`

## Cache Expiry

- Read `cachedAt` from the context file
- If older than **7 days** — re-scan the project and overwrite the cache
- If the user asks to refresh: re-scan immediately regardless of age

## Session Integration

Pass cached context to mission generation. Every mission should feel connected to the user's actual work.

### Mission Integration

Use project domain terms in challenges:

- **Swap:** Use sentences about the user's domain. "We need to **handle** the checkout flow" instead of generic "handle the task."
- **Trim:** Pull bloated phrases from project-relevant scenarios. "In order to facilitate the process of deploying to staging..."
- **Punch:** Flatten sentences about the user's actual features. "The cart update went well."
- **Snipe:** Prioritize passages from conversations about the current project.
- **Flip:** Use project scenarios for tone flips. Casual dev chat about a deploy → formal incident report.
- **Fill:** Use project-specific sentences. "The _____ of our checkout flow caused cart abandonment."

### 🔥 Roast Integration

Prioritize passages related to the current project:
- Scan conversations about the project for vague descriptions, hedging in decisions, filler in commit messages.
- Project-specific roasts feel more relevant and memorable.
