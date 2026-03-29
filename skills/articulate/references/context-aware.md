# Context-Aware Missions

## Purpose

Read the user's current project to generate missions that use real project nouns, domain terms, and scenarios. This makes missions feel relevant rather than generic.

## Opt-In Check

Before any context gathering:

1. Read `~/.articulate/user.json`
2. Check the `contextAware` field
3. If `false` — skip everything in this file. Use generic challenges only.
4. If `true` — proceed with context gathering

## First Time in a New Project

When the user invokes `/articulate` in a project directory that has no cached context:

1. Detect the project name from the directory name or manifest file
2. Ask: `"I notice you're working on {project}. Want me to generate missions based on this? (yes/no)"`
3. If the user says no — skip context for this project, do NOT cache, use generic missions
4. If the user says yes — proceed with context extraction below

Do not ask again for a project that already has a cached context file.

## What to Read

Scan the current working directory for these files, in priority order. Stop once you have enough to build a project summary. Do not read more than necessary.

1. **README.md** (or README) — primary source. Read the first 100 lines max.
2. **package.json** — extract `name`, `description`, `keywords`
3. **Cargo.toml** — extract `[package]` name and description
4. **pyproject.toml** — extract `[project]` name and description
5. **go.mod** — extract module name
6. **CLAUDE.md** — extract project description sections only (not instructions)
7. **docs/ index** — scan for an index.md or README.md in the docs directory

## What to Extract

Build a summary containing ONLY these fields:

- **name**: Project name
- **description**: One-line description (50 words max)
- **domain**: Industry or domain (e.g., "fitness/health-tech", "developer-tools", "fintech")
- **audience**: Who uses this (e.g., "mobile app developers", "enterprise teams")
- **features**: 3-5 key features as short phrases
- **techStack**: Primary languages/frameworks (e.g., "TypeScript, React, Node.js")

## What NEVER to Include

These must NEVER appear in context summaries or generated missions:

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

## Mission Integration

When generating missions, pass the cached context so the mission generator can weave in project-specific terms.

### REWRITE Integration

Use project nouns and domain in the weak sentence:

- Generic: `"The thing we built is really good and helps people do stuff faster."`
- Context-aware: `"The MoveKit API is a good thing that helps developers do exercise stuff in their apps."`

The weak words remain weak — but the nouns and domain match the user's project.

### SCENARIO Integration

Use the project as the setting for professional communication challenges:

- Generic: `"A potential customer asks about your product's batch processing..."`
- Context-aware: `"A fitness app PM asks if MoveKit supports custom animation speeds and wants to see a demo before committing to your API plan."`

### PROMPT_CRAFT Integration

Use the project domain as the subject of prompt-writing challenges:

- Generic: `"Write a prompt that generates API documentation for a REST endpoint."`
- Context-aware: `"Write a prompt that generates API documentation for MoveKit's animation endpoints, targeting mobile developers who use Swift."`

### FILL_PRECISION Integration

Use project context in the surrounding sentence:

- Generic: `"The system's response time was [___], often exceeding 3 seconds."`
- Context-aware: `"MoveKit's animation rendering pipeline was [___], dropping frames on older devices."`

### REVIEW Integration

When reviewing past missions, if the original was context-aware, use the same project context for the review challenge.
