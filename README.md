# FrameShift — Relational Frame Training Game Suite

**Version:** 1.0  
**Author:** Syntopic Systems (AUSPEX build, JONATHAN clinical specs)  
**Date:** February 17, 2026  
**License:** Proprietary — Syntopic Systems LLC

---

## Overview

FrameShift is a suite of 10 therapeutic games implementing Relational Frame Theory (RFT) protocols for children, primarily targeting language and reasoning development in autism spectrum disorder (ASD). Each game trains a specific relational frame through a structured train → test paradigm, where the test phase probes for *derived* relational responding — behavior that was never directly trained.

The suite progresses from concrete translation frames (comparative, coordination) through equivalence relations (identity, cross-modal, analogical) to abstract operations (categorical, interrogative, descriptive, inductive).

## Architecture

### Stack
- **Single-file HTML** — each game is one self-contained `.html` file
- **React 18** via CDN (unpkg)
- **Tailwind CSS** via CDN
- **Babel standalone** for JSX transformation
- **Zero build step** — open any file in a browser, it runs
- **OpenMoji** emoji via CDN (CC BY-SA 4.0) for consistent cross-platform visuals

### Data Flow
```
Game completes session
    ↓
window.FrameShift.saveSession(programId, trainScore, trainMax, testScore, testMax, mastery)
    ↓
localStorage["frameshift_progress"]
    ↓
FrameShift Hub reads on load/focus
    ↓
Stats, achievements, session log update
```

### Progress Schema
```json
{
  "programs": {
    "p1": {
      "sessions": [
        { "date": "ISO", "trainScore": 10, "trainMax": 12, "testScore": null, "testMax": null }
      ],
      "bestScore": { "train": 10, "test": null },
      "mastery": false,
      "lastPlayed": "ISO"
    }
  },
  "achievements": {},
  "totalSessions": 5,
  "streak": { "current": 2, "best": 3, "lastDate": "2026-02-17" }
}
```

## File Inventory

| File | Size | Program | Clinical Target |
|------|------|---------|----------------|
| `frameshift-hub.html` | 28KB | Hub + Tracker | Navigation, progress dashboard, achievements |
| `p1-more-or-less.html` | 30KB | More or Less | Comparative relations |
| `p2-same-and-different.html` | 29KB | Same & Different | Coordination/distinction |
| `p3-symbol-bridge.html` | 29KB | Symbol Bridge | Stimulus equivalence |
| `p4-scent-match.html` | 35KB | Scent Match | Cross-modal olfactory equivalence |
| `p5-taste-test.html` | 39KB | Taste Test | Cross-modal gustatory + vocal production |
| `p6-common-features.html` | 31KB | Common Features | Analogical reasoning |
| `p7-what-kind-of-story.html` | 54KB | What Kind of Story? | Genre abstraction / categorical |
| `p8-why-detective.html` | 35KB | The Why Detective | Interrogative frame (why → because) |
| `p9-what-kind.html` | 31KB | What Kind? | Descriptive/qualifier frame |
| `p10-what-comes-next.html` | 41KB | What Comes Next? | Inductive pattern abstraction |

**Total:** ~382KB for the complete suite. No external dependencies beyond CDN links.

## Clinical Design

### Category Structure

| Category | Programs | Frame Types |
|----------|----------|-------------|
| **Translation** | P1–P2 | Comparative, coordination/distinction |
| **Equivalence** | P3–P6 | Identity, cross-modal (olfactory, gustatory), feature-based analogy |
| **Abstraction** | P7–P10 | Categorical, interrogative, descriptive, inductive |

### Mastery & Gating

Every program follows the same paradigm:
1. **Training phase** — corrective feedback, scaffolding
2. **Test phase** — novel stimuli, no corrective feedback ("Response recorded")
3. **Mastery threshold** — must pass training to unlock test
4. **Derived responding** — test phase measures behavior never directly trained

The test phase is the clinical signal. Training accuracy is expected; test accuracy demonstrates *generalization* — the hallmark of relational frame formation.

### Caregiver Orchestration

Programs 4, 5, 8, and 9 require a caregiver/clinician to mediate physical stimuli or score vocal responses. These use a consistent UI pattern:
- Setup screen (caregiver prepares materials)
- Present prompt (app instructs caregiver what to show/do)
- Caregiver confirms child's response
- Score screen (3-level: correct / partial / incorrect, with text field)

### Data Logging

Every program logs trial-level data including:
- Stimulus presented, response given, correct answer
- Response latency (where applicable)
- Error classification (program-specific diagnostic codes)
- Phase, trial number, timestamp

This data is preserved in the trial log within each game session and summarized to the tracker on completion.

## Deployment

### Minimal (Local)
1. Place all 11 `.html` files in the same directory
2. Open `frameshift-hub.html` in a browser
3. Click any program to launch it
4. Progress persists via `localStorage`

### Notes
- Works offline once CDN resources are cached
- All files must be in the same directory (relative links)
- `localStorage` is per-origin — progress is scoped to the serving domain
- Reset progress from the hub footer

## Achievements

| Badge | Title | Requirement |
|-------|-------|-------------|
| 👣 | First Steps | Complete 1 session |
| 🗺️ | Explorer | Try all 10 programs |
| 🔥 | On Fire | 5-day play streak |
| ⭐ | Dedicated | Complete 10 sessions |
| 🥇 | First Mastery | Master any program |
| 🏆 | Five Star | Master 5 programs |
| 👑 | FrameShift Master | Master all 10 programs |
| 🔗 | Equivalence Pro | Master programs 3–6 |
| 🧠 | Abstract Thinker | Master programs 7–10 |
| 💎 | Quarter Century | Complete 25 sessions |

## Known Limitations

- No server-side persistence — progress is `localStorage` only
- No multi-user support (single learner per browser profile)
- Caregiver scoring is honor-system (no automated speech recognition)
- Stories in P7 are fixed content (future: LLM-generated novel stimuli)
- P10 implements Tiers 1–2 only (Tiers 3–4 with category/multisensory patterns planned)
- CDN dependency for React, Tailwind, Babel, OpenMoji (cache for offline use)

## Future Integration Points

- **Echo Proxy** — voice-activated game launching via Alexa
- **Progress Tracker API** — server-side persistence (SQLite/DuckDB)
- **PWA wrapper** — installable app with offline support
- **LLM story generation** — infinite novel test stimuli for P7
- **Cross-program analytics** — frame-type profiling, modality profiling, abstraction gradient mapping

---

*Built by AUSPEX. Clinical design by JONATHAN. For Syntopic Systems LLC.*
