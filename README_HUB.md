# FrameShift Hub — README

**File:** `index.html`  
**Purpose:** Navigation hub, progress tracker, and achievement system for the FrameShift RFT Game Suite  
**Version:** 2.0

## What It Does

Central landing page for the 20-program suite. Displays:
- **Overview stats** — total sessions, programs tried (/20), programs mastered (/20), day streak, achievements earned
- **Category progress bars** — 8 categories: Translation (P1–2), Equivalence (P3–6), Abstraction (P7–10), Inference (P11–14), Flexibility (P15), Social (P16), Language (P17–18, P20), Categorization (P19)
- **Program grid** — clickable cards with mastery rings, star ratings, session counts
- **Achievement badges** — 14 unlockable achievements with earned/locked states
- **Session log** — per-program history showing train/test scores by date

## Visual Design

- **Dancing lines background** — 7 sine waves with different amplitudes, frequencies, and colors, rendered on an HTML5 canvas at 60fps. Soft indigo/purple/pink/blue palette.
- **Glassmorphism cards** — `backdrop-filter: blur(12px)` with semi-transparent white backgrounds
- **Mastery rings** — conic-gradient progress indicators around each program emoji
- **Star ratings** — 0–3 stars: 0 = untouched, 1 = played, 2 = reached test phase, 3 = mastered
- **Category grid** — 2×4 grid on mobile, 4×2 on desktop, compact progress bars per category

## Data Schema

Reads `localStorage["frameshift_progress"]`:

```json
{
  "programs": {
    "p1": {
      "sessions": [
        { "date": "2026-02-22T...", "trainScore": 10, "trainMax": 12 }
      ],
      "bestScore": { "train": 10, "test": null },
      "mastery": false,
      "lastPlayed": "2026-02-22T..."
    }
  },
  "totalSessions": 5,
  "streak": { "current": 2, "best": 3, "lastDate": "2026-02-22" },
  "achievements": {}
}
```

Games write to this via `window.FrameShift.saveSession()` (injected into each game file).

## Achievement Definitions

| ID | Emoji | Title | Trigger |
|----|-------|-------|---------|
| `first_steps` | 👣 | First Steps | totalSessions ≥ 1 |
| `explorer` | 🗺️ | Explorer | programs tried ≥ 10 |
| `globe_trotter` | 🌍 | Globe Trotter | programs tried ≥ 20 |
| `five_streak` | 🔥 | On Fire | streak.best ≥ 5 |
| `ten_sessions` | ⭐ | Dedicated | totalSessions ≥ 10 |
| `mastery_1` | 🥇 | First Mastery | any program mastered |
| `mastery_5` | 🏆 | Five Star | 5 programs mastered |
| `mastery_10` | 🌟 | Ten Star | 10 programs mastered |
| `mastery_all` | 👑 | FrameShift Master | all 20 mastered |
| `equiv_complete` | 🔗 | Equivalence Pro | P3–P6 all mastered |
| `abstraction_complete` | 🧠 | Abstract Thinker | P7–P10 all mastered |
| `inference_complete` | ⛓️ | Chain Master | P11–P14 all mastered |
| `twenty_five` | 💎 | Quarter Century | totalSessions ≥ 25 |
| `fifty_sessions` | 🔮 | Fifty & Fabulous | totalSessions ≥ 50 |

Achievements are computed on-the-fly from progress data (no separate storage needed).

## Program Registry

| ID | Title | Category |
|----|-------|----------|
| P1 | More or Less | Translation |
| P2 | Same & Different | Translation |
| P3 | Symbol Bridge | Equivalence |
| P4 | Scent Match | Equivalence |
| P5 | Taste Test | Equivalence |
| P6 | Common Features | Equivalence |
| P7 | What Kind of Story? | Abstraction |
| P8 | The Why Detective | Abstraction |
| P9 | What Kind? | Abstraction |
| P10 | What Comes Next? | Abstraction |
| P11 | Chain Reaction | Inference |
| P12 | Value Chain | Inference |
| P13 | Trait Bridge | Inference |
| P14 | Feeling Metaphors | Inference |
| P15 | Creative Tools | Flexibility |
| P16 | What to Share | Social |
| P17 | Name That Thing | Language |
| P18 | Character Namer | Language |
| P19 | Same or Different | Categorization |
| P20 | Pronoun Bridge | Language |

## Navigation

- Hub → Game: each program card links to its `.html` file
- Game → Hub: floating "← FrameShift" pill (top-left) + "← Back to FrameShift" link on end screen
- Hub refreshes data on `window.focus` event (auto-updates when returning from a game tab)

## Streak Tracking

Day streaks are calculated in `saveSession()`:
- Same calendar day → no change
- Next calendar day → streak increments
- Gap of 2+ days → streak resets to 1
- Best streak preserved separately

## Reset

"Reset Progress" link in footer. Confirmation dialog before clearing `localStorage`.
