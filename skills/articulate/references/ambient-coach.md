# Ambient Coach

Always-on coaching that drops inline vocabulary tips during regular work sessions.

## Injection Prompt

This prompt (under 150 words) gets embedded in the session-start hook when coaching is enabled:

```
You have Articulate ambient coaching enabled. When you notice the user writing with vague, hedging, or imprecise language in their messages to you, occasionally offer a brief inline vocabulary tip. Format: 💡 *You wrote "X" — try "Y" for [reason].* Rules: max once per 3-4 user messages, one line only, placed after your main response with a blank line separator, only target natural language (never code), skip if user is rushed/debugging/emotional, never suggest the same tip twice in a session. Focus on: vague nouns (thing/stuff), weak verbs (do/make/get), hedging (I think maybe), filler (basically/literally/just/really).
```

**Word count:** 104 words. Must stay under 150.

## State Management

### Check

Read `~/.articulate/user.json` and inspect the `coachingEnabled` field.

```json
{
  "name": "Hristo",
  "languages": ["en", "bg"],
  "coachingEnabled": true,
  "createdAt": "2026-03-29T...",
  "lastUpdated": "2026-03-29T..."
}
```

### Toggle

| Command | Action |
|---------|--------|
| `/articulate coach on` | Set `coachingEnabled: true` in user.json |
| `/articulate coach off` | Set `coachingEnabled: false` in user.json |

Confirm with:
- On: "Ambient coaching **on**. I'll drop tips as you work."
- Off: "Ambient coaching **off**. Run `/articulate coach on` to re-enable."

## Tip Format

Always exactly this structure, placed after the main response with a blank line:

```
{main response content here}

💡 *You wrote "do the thing" — try "execute the migration" for precision.*
```

## Frequency Rules

- **Max once per 3-4 user messages** — never tip on consecutive messages
- **One line only** — never multi-line tips
- **After main response** — separated by a blank line, never interrupting the answer
- **Track internally** — count user messages since last tip to enforce spacing

## What to Target

| Pattern | Example trigger | Example tip |
|---------|----------------|-------------|
| Vague nouns | "fix the thing" | try "fix the parser" |
| Weak verbs | "make it work" | try "restore the connection" |
| Hedging | "I think maybe we should" | try "we should" |
| Fillers | "basically the issue is" | try "the issue is" |

## What NOT to Coach

Skip tip generation entirely when:

- **Code** — never correct variable names, function calls, or technical syntax
- **Technical jargon** — domain terms are precise by nature, leave them alone
- **Casual chat** — if the user is clearly in informal mode, don't coach
- **Non-configured languages** — only coach languages listed in `user.json` languages
- **Rushed/debugging** — if messages are short and rapid-fire, the user is troubleshooting. Stay out of the way
- **Emotional context** — if the user sounds frustrated or stressed, coaching feels tone-deaf

## Session-Start Hook Integration

The session-start hook (`hooks/session-start`) handles injection:

1. Read `~/.articulate/user.json`
2. Check `coachingEnabled === true`
3. If true, append the injection prompt to the hook output
4. Platform detection (CLAUDE_PLUGIN_ROOT vs CURSOR_PLUGIN_ROOT) stays unchanged

The prompt is embedded directly in the hook script — not loaded from this file at runtime.

## Example in Context

User message: "Can you basically just make the button do the thing when someone clicks it?"

Claude response:
```
Sure. I'll add an onClick handler to the submit button that triggers form validation.

[code block with implementation]

💡 *You wrote "make the button do the thing" — try "trigger validation on click" for clarity.*
```
