# FrameShift — Relational Frame Training Game Suite

**Version:** 2.0  
**Author:** Syntopic Systems (AUSPEX build, JONATHAN clinical specs)  
**Date:** February 22, 2026  
**License:** Proprietary — Syntopic Systems LLC

---

## Overview

FrameShift is a suite of 32 therapeutic games implementing Relational Frame Theory (RFT) protocols for children, primarily targeting language and reasoning development in autism spectrum disorder (ASD). Each game trains a specific relational frame through a structured train → test paradigm, where the test phase probes for *derived* relational responding — behavior that was never directly trained.

The suite progresses from concrete translation frames (comparative, coordination) through equivalence relations (identity, cross-modal, analogical) to abstract operations (categorical, interrogative, descriptive, inductive), inferential reasoning (conditional, reverse, metaphor), social/pragmatic skills, language production, and transformation frames (spatial, temporal, opposition, deictic, emotional).

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
  "streak": { "current": 2, "best": 3, "lastDate": "2026-02-22" }
}
```

## File Inventory

| File | Program | Category | Clinical Target |
|------|---------|----------|----------------|
| `index.html` | Hub + Tracker | — | Navigation, progress dashboard, achievements |
| `p1-more-or-less.html` | More or Less | Translation | Comparative relations |
| `p2-same-and-different.html` | Same & Different | Translation | Coordination/distinction |
| `p3-symbol-bridge.html` | Symbol Bridge | Equivalence | Stimulus equivalence |
| `p4-scent-match.html` | Scent Match | Equivalence | Cross-modal olfactory equivalence |
| `p5-taste-test.html` | Taste Test | Equivalence | Cross-modal gustatory + vocal production |
| `p6-common-features.html` | Common Features | Equivalence | Analogical reasoning |
| `p7-what-kind-of-story.html` | What Kind of Story? | Abstraction | Genre abstraction / categorical |
| `p8-why-detective.html` | The Why Detective | Abstraction | Interrogative frame (why → because) |
| `p9-what-kind.html` | What Kind? | Abstraction | Descriptive/qualifier frame |
| `p10-what-comes-next.html` | What Comes Next? | Abstraction | Inductive pattern abstraction |
| `p11-chain-reaction.html` | Chain Reaction | Inference | Conditional inference |
| `p12-value-chain.html` | Value Chain | Inference | Reverse derivation |
| `p13-trait-bridge.html` | Trait Bridge | Inference | Synonym inference |
| `p14-feeling-metaphors.html` | Feeling Metaphors | Inference | Metaphor |
| `p15-creative-tools.html` | Creative Tools | Social | Creative problem-solving |
| `p16-what-to-share.html` | What to Share | Social | Pragmatic disclosure |
| `p17-name-that-thing.html` | Name That Thing | Language | Description |
| `p18-character-namer.html` | Character Namer | Language | Naming |
| `p19-same-or-different.html` | Same or Different | Equivalence | Equivalence class |
| `p20-pronoun-bridge.html` | Pronoun Bridge | Language | Pronouns |
| `p21-near-and-far.html` | Near & Far | Transformation | Spatial comparison / reversal |
| `p22-first-things-first.html` | First Things First | Transformation | Temporal sequencing / transitive derivation |
| `p23-opposite-day.html` | Opposite Day | Transformation | Opposition / dimension extraction |
| `p24-spot-the-difference.html` | Spot the Difference | Transformation | Distinction / difference matching |
| `p25-feeling-flip.html` | Feeling Flip | Transformation | Emotional opposites / combinatorial entailment |
| `p26-season-sense.html` | Season Sense | Transformation | Deictic comparison / reversal |
| `p27-weather-switch.html` | Weather Switch | Transformation | Weather same→opposite→clothing (transitive) |
| `p28-family-flip.html` | Family Flip | Transformation | Opposite relative titles |
| `p29-taste-match.html` | Taste Match | Equivalence | Taste equivalence class / menu substitution |
| `p30-whats-it-like.html` | What's It Like? | Abstraction | Feature→item→name circular derivation |
| `p31-where-would-you-go.html` | Where Would You Go? | Inference | Location→items / scenario problem-solving |
| `p32-here-and-there.html` | Here & There | Transformation | Deictic HERE/THERE reversal |

**Total:** 33 HTML files (1 hub + 32 programs). No external dependencies beyond CDN links.

## Clinical Design

### Category Structure

| Category | Programs | Frame Types |
|----------|----------|-------------|
| **Translation** | P1–2 | Comparative, coordination/distinction |
| **Equivalence** | P3–6, 19, 29 | Identity, cross-modal (olfactory, gustatory), feature-based analogy, equivalence class, taste |
| **Abstraction** | P7–10, 30 | Categorical, interrogative, descriptive, inductive, feature derivation |
| **Inference** | P11–14, 31 | Conditional, reverse, synonym, metaphor, location |
| **Social** | P15–16 | Creative problem-solving, pragmatic disclosure |
| **Language** | P17–18, 20 | Description, naming, pronouns |
| **Transformation** | P21–28, 32 | Spatial, temporal, opposition, distinction, emotional, deictic, weather, family |

### Mastery & Gating

Every program follows the same paradigm:
1. **Training phase** — corrective feedback, scaffolding
2. **Test phase** — novel stimuli, no corrective feedback ("Response recorded")
3. **Mastery threshold** — must pass training (typically 75%) to unlock test
4. **Derived responding** — test phase measures behavior never directly trained

The test phase is the clinical signal. Training accuracy is expected; test accuracy demonstrates *generalization* — the hallmark of relational frame formation.

### Caregiver Orchestration

Programs requiring a caregiver/clinician to mediate physical stimuli or score vocal responses: P4, P5, P8, P9, P23, P24, P25, P28, P30, P32. These use a consistent UI pattern:
- Dashed yellow border caregiver panel
- Present prompt (app instructs caregiver what to say/do)
- 3-level scoring buttons: ✅ Correct / 🟡 Close / ❌ Incorrect
- Optional text field for actual utterance
- Expected answer hint (training only)

### Data Logging

Every program logs trial-level data including:
- Stimulus presented, response given, correct answer
- Response latency (where applicable)
- Error classification (program-specific diagnostic codes)
- Phase, trial number, timestamp

This data is preserved in the trial log within each game session and summarized to the tracker on completion.

## Deployment

### Minimal (Local)
1. Place all 33 `.html` files in the same directory
2. Open `index.html` in a browser
3. Click any program to launch it
4. Progress persists via `localStorage`

### GitHub Pages
Repository: `https://github.com/syntopicsystems/frameshift`
- Push all files to `main` branch
- Enable Pages from Settings → Pages → Deploy from branch
- Access at `https://syntopicsystems.github.io/frameshift/`

### Notes
- Works offline once CDN resources are cached
- All files must be in the same directory (relative links)
- `localStorage` is per-origin — progress is scoped to the serving domain
- Reset progress from the hub footer

## Achievements

| Badge | Title | Requirement |
|-------|-------|-------------|
| 👣 | First Steps | Complete 1 session |
| 🗺️ | Explorer | Try 10 different programs |
| 🌍 | Globe Trotter | Try all 32 programs |
| 🔥 | On Fire | 5-day play streak |
| ⭐ | Dedicated | Complete 10 sessions |
| 🥇 | First Mastery | Master any program |
| 🏆 | Five Star | Master 5 programs |
| 💫 | Ten Strong | Master 10 programs |
| 👑 | FrameShift Master | Master all 32 programs |
| 🔗 | Equivalence Pro | Master all equivalence programs |
| 🧠 | Abstract Thinker | Master all abstraction programs |
| 🔮 | Master Deducer | Master all inference programs |
| 🔄 | Shapeshifter | Master all transformation programs |
| 💎 | Quarter Century | Complete 25 sessions |
| 🎯 | Fifty Strong | Complete 50 sessions |

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
