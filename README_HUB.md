# FrameShift Hub — README

**File:** `index.html`  
**Purpose:** Navigation hub, progress tracker, and achievement system for the FrameShift RFT Game Suite

## What It Does

Central landing page for the 32-program suite. Displays:
- **Overview stats** — total sessions, programs tried (/32), programs mastered (/32), day streak, achievements earned
- **Category progress bars** — 7 categories in a responsive grid
- **Program grid** — clickable cards with mastery rings, star ratings, session counts (4-column on wide screens)
- **Achievement badges** — 15 unlockable achievements with earned/locked states
- **Session log** — per-program history showing train/test scores by date

## Category Structure

| Category | Programs | Color |
|----------|----------|-------|
| Translation | P1–2 | Green |
| Equivalence | P3–6, 19, 29 | Purple |
| Abstraction | P7–10, 30 | Blue |
| Inference | P11–14, 31 | Red |
| Social | P15–16 | Teal |
| Language | P17–18, 20 | Violet |
| Transformation | P21–28, 32 | Orange |

## Visual Design

- **Dancing lines background** — 7 sine waves with different amplitudes, frequencies, and colors, rendered on an HTML5 canvas at 60fps. Soft indigo/purple/pink/blue palette.
- **Glassmorphism cards** — `backdrop-filter: blur(12px)` with semi-transparent white backgrounds
- **Mastery rings** — conic-gradient progress indicators around each program emoji
- **Star ratings** — 0–3 stars: 0 = untouched, 1 = played, 2 = reached test phase, 3 = mastered
- **Responsive grid** — 1 col mobile, 2 col tablet, 3 col desktop, 4 col wide

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
| `globe_trotter` | 🌍 | Globe Trotter | programs tried ≥ 32 |
| `five_streak` | 🔥 | On Fire | streak.best ≥ 5 |
| `ten_sessions` | ⭐ | Dedicated | totalSessions ≥ 10 |
| `mastery_1` | 🥇 | First Mastery | any program mastered |
| `mastery_5` | 🏆 | Five Star | 5 programs mastered |
| `mastery_10` | 💫 | Ten Strong | 10 programs mastered |
| `mastery_all` | 👑 | FrameShift Master | all 32 mastered |
| `equiv_complete` | 🔗 | Equivalence Pro | P3–6, 19, 29 all mastered |
| `abstraction_complete` | 🧠 | Abstract Thinker | P7–10, 30 all mastered |
| `inference_complete` | 🔮 | Master Deducer | P11–14, 31 all mastered |
| `transform_complete` | 🔄 | Shapeshifter | P21–28, 32 all mastered |
| `twenty_five` | 💎 | Quarter Century | totalSessions ≥ 25 |
| `fifty_sessions` | 🎯 | Fifty Strong | totalSessions ≥ 50 |

Achievements are computed on-the-fly from progress data (no separate storage needed).

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
