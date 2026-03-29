# Autoresearch Results Log

## Config
- Goal: Make /articulate fascinating, visually polished, and genuinely educational
- Scope: skills/articulate/**/* + hooks/session-start
- Metric: Fascination (0-25) + Teaching Quality (0-25) + Visual Polish (0-25) = 0-75
- Direction: Higher is better
- Guard: SKILL.md < 400 lines
- Iterations: 10
- Test: Fresh state each run, English only, claude -p simulation

## Results

| # | Change | Fascination | Teaching | Visual | Total | Verdict |
|---|--------|-------------|----------|--------|-------|---------|
| 0 | Baseline | 21 | 19 | 19 | 59 | — |
| 1 | Storytelling quality bar + onboarding personality | 22 | 20 | 20 | 62 | ✓ Keep |
| 2 | Topic diversity + first-session guidance | 24 | 21 | 21 | 66 | ✓ Keep |
| 3 | Scoring feedback + bonus nuggets | 24 | 22 | 21 | 67 | ✓ Keep |
| 4-test | Roast mode (no file changes, just testing) | 25 | 23 | 23 | 71 | ✓ Best! |
