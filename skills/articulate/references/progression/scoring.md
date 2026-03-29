# Progression — Scoring & XP

## Scoring by Mission Type

### Simple Scoring (Swap & Fill)

Three tiers — no axis bars:

| Tier | Score | XP | Display |
|------|-------|----|---------|
| ✅ Nailed it | 90 | 15 | `✅ **Nailed it.** +15 XP` |
| 🔶 Close | 70 | 10 | `🔶 **Close.** +10 XP` |
| ❌ Missed | 40 | 5 | `❌ **Missed.** +5 XP` |

### Full Scoring (Trim, Punch, Snipe, Flip)

Four axes, 25 points each, 100 total.

**Trim:**
| Axis | What it measures |
|------|-----------------|
| Compression | How much waste was cut |
| Meaning | Core meaning preserved? |
| Naturalness | Reads like a human wrote it |
| Impact | Does it actually land better? |

**Punch:**
| Axis | What it measures |
|------|-----------------|
| Power | Does it hit harder than the original? |
| Specificity | Vague → concrete? |
| Naturalness | Not forced or over-written |
| Brevity | Didn't bloat while punching up |

**Snipe:**
| Axis | What it measures |
|------|-----------------|
| Detection | How many problems found |
| Precision | Fixes are specific, not vague |
| Compression | Waste cut in rewrite |
| Naturalness | Reads like real writing |

**Flip:**
| Axis | What it measures |
|------|-----------------|
| Register | Actually changed register, not just swapped words |
| Naturalness | Sounds natural in target register |
| Information | Core info preserved through the flip |
| Style | Has personality in the new register |

### Display Format

```
**Score: 85/100**
├─ Compression:  22/25 ████████████████████░░░░
├─ Meaning:      21/25 ████████████████████░░░░
├─ Naturalness:  22/25 ████████████████████░░░░
└─ Impact:       20/25 ████████████████░░░░░░░░
```

Bar: 25 chars. `filled = floor((score/25) * 25)`.

---

## XP Formula

| Component | Formula | Range |
|-----------|---------|-------|
| base | 10 | 10 |
| score_bonus | floor(score / 10) | 0-10 |
| streak_bonus | min(streak × 2, 20) | 0-20 |
| **total** | **sum** | **10-40** |

### Display (one line)

```
⚡ +28 XP (base 10 + score 8 + streak 10) | 🔥 5d
```

### Cumulative

```
XP: 342 → 370/600 ████████████████░░░░░░░░░ 62% → 🟧 SPECIALIST
```
