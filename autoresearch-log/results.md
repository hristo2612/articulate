# Autoresearch Results Log

## Phase 1 Config (iterations 0-20)
- Goal: Make /articulate fascinating, visually polished, and genuinely educational
- Scope: skills/articulate/**/* + hooks/session-start
- Metric: Fascination (0-25) + Teaching Quality (0-25) + Visual Polish (0-25) = 0-75
- Direction: Higher is better
- Guard: SKILL.md < 400 lines
- Iterations: 20
- Final Score: 73/75

## Phase 1 Results

| # | Change | Fascination | Teaching | Visual | Total | Verdict |
|---|--------|-------------|----------|--------|-------|---------|
| 0 | Baseline | 21 | 19 | 19 | 59 | — |
| 10 | All improvements combined | 25 | 24 | 23 | 72 | Best |
| 20 | Final test | 25 | 25 | 23 | 73 | Final |

---

## Phase 2 Config (iterations 21-30) — RADICAL REBUILD
- Goal: Radically reimagine the skill using science-backed learning methods
- Approach: Replace everything. No sacred cows. Test completely different pedagogies.
- Scope: skills/articulate/**/* + hooks/session-start
- Metric: Active Learning (0-25) + Stickiness (0-25) + Practical Transfer (0-25) + Delight (0-25) = 0-100
- Direction: Higher is better
- Guard: SKILL.md < 400 lines
- Iterations: 10
- Test: Fresh state each run, English only, claude -p simulation

### Science-Backed Methods Being Tested
- **Retrieval practice** — testing > re-reading (Roediger & Karpicke, 2006)
- **Productive failure** — struggle first, instruction after (Kapur, 2008)
- **Elaborative interrogation** — "WHY does this work?" (Pressley et al., 1987)
- **Interleaving** — mixing topics > blocking (Rohrer & Taylor, 2007)
- **Desirable difficulty** — harder encoding = better retention (Bjork, 1994)
- **Contrastive analysis** — comparing examples forces deep processing
- **Generation effect** — self-generated > read (Slamecka & Graf, 1978)

## Phase 2 Results

| # | Approach | Active | Sticky | Transfer | Delight | Total | Verdict |
|---|----------|--------|--------|----------|---------|-------|---------|
