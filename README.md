# FrameShift — Relational Frame Training Game Suite

**Version:** 2.0  
**Author:** Syntopic Systems (AUSPEX build, JONATHAN clinical specs)  
**Date:** February 22, 2026  
**License:** Proprietary — Syntopic Systems LLC

---

## Overview

FrameShift is a suite of 20 therapeutic games implementing Relational Frame Theory (RFT) protocols for children, primarily targeting language and reasoning development in autism spectrum disorder (ASD). Each game trains a specific relational frame through a structured train → test paradigm, where the test phase probes for *derived* relational responding — behavior that was never directly trained.

The suite progresses from concrete translation frames (comparative, coordination) through equivalence relations (identity, cross-modal, analogical) to abstract operations (categorical, interrogative, inductive), then into inference chains (conditional, transitive, metaphorical), flexible problem-solving, social pragmatics, and generative language tasks.

Programs 12, 14, 16, and 18 include **caregiver-scored generation phases** where the child must produce responses spontaneously rather than selecting from options — measuring the clinically critical recognition-to-generation gap.

## Architecture

### Stack
- **Single-file HTML** — each game is one self-contained `.html` file
- **React 18** via CDN (unpkg)
- **Tailwind CSS** via CDN
- **Babel standalone** for JSX transformation
- **Zero build step** — open any file in a browser, it runs
- **Web Audio API** — synthesized sound effects (correct, incorrect, neutral, complete)

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

| File | Program | Clinical Target | Category |
|------|---------|----------------|----------|
| `index.html` | Hub + Tracker | Navigation, progress, achievements | — |
| `p1-more-or-less.html` | More or Less | Comparative relations | Translation |
| `p2-same-and-different.html` | Same & Different | Coordination/distinction | Translation |
| `p3-symbol-bridge.html` | Symbol Bridge | Stimulus equivalence | Equivalence |
| `p4-scent-match.html` | Scent Match | Cross-modal olfactory | Equivalence |
| `p5-taste-test.html` | Taste Test | Cross-modal gustatory + vocal | Equivalence |
| `p6-common-features.html` | Common Features | Analogical reasoning | Equivalence |
| `p7-what-kind-of-story.html` | What Kind of Story? | Genre abstraction | Abstraction |
| `p8-why-detective.html` | The Why Detective | Interrogative frame | Abstraction |
| `p9-what-kind.html` | What Kind? | Descriptive/qualifier frame | Abstraction |
| `p10-what-comes-next.html` | What Comes Next? | Inductive patterns | Abstraction |
| `p11-chain-reaction.html` | Chain Reaction | Conditional inference | Inference |
| `p12-value-chain.html` | Value Chain | Reverse derivation + generation | Inference |
| `p13-trait-bridge.html` | Trait Bridge | Synonym-mediated equivalence | Inference |
| `p14-feeling-metaphors.html` | Feeling Metaphors | Multi-relation emotional metaphor | Inference |
| `p15-creative-tools.html` | Creative Tools | Non-obvious tool selection | Flexibility |
| `p16-what-to-share.html` | What to Share | Social pragmatics + safety | Social |
| `p17-name-that-thing.html` | Name That Thing | Figurative description comprehension | Language |
| `p18-character-namer.html` | Character Namer | Trait-based creative naming | Language |
| `p19-same-or-different.html` | Same or Different | Equivalence class formation | Categorization |
| `p20-pronoun-bridge.html` | Pronoun Bridge | Pronoun families + story application | Language |

## Clinical Design

### Category Structure

| Category | Programs | Frame Types |
|----------|----------|-------------|
| **Translation** | P1–P2 | Comparative, coordination/distinction |
| **Equivalence** | P3–P6 | Identity, cross-modal (olfactory, gustatory), feature-based analogy |
| **Abstraction** | P7–P10 | Categorical, interrogative, descriptive, inductive |
| **Inference** | P11–P14 | Conditional chaining, reverse derivation, synonym mediation, metaphorical networks |
| **Flexibility** | P15 | Creative lateral problem-solving |
| **Social** | P16 | Pragmatic information disclosure, safety awareness |
| **Language** | P17–P18, P20 | Description comprehension, generative naming, pronoun classes |
| **Categorization** | P19 | Equivalence class sorting, odd-one-out |

### Mastery & Gating

Every program follows the same paradigm:
1. **Training phase** — corrective feedback, scaffolding
2. **Test phase** — novel stimuli, no corrective feedback ("Response recorded")
3. **Mastery threshold** — must pass training (typically 75%) to unlock test
4. **Derived responding** — test phase measures behavior never directly trained

The test phase is the clinical signal. Training accuracy is expected; test accuracy demonstrates *generalization* — the hallmark of relational frame formation.

### Generation Phases (P12, P14, P16, P18)

Four programs include a third phase where the child must produce responses without choices:
- **P12 Value Chain** — given a value, produce the action
- **P14 Feeling Metaphors** — given a metaphor, produce the emotion
- **P16 What to Share** — given a social scenario, produce an appropriate response
- **P18 Character Namer** — given character traits, invent a creative name

Caregiver scores responses as ✅ Correct / 🟡 Partial / ❌ Incorrect, with verbatim text logging. The recognition-to-generation gap on identical stimuli (same items appear in both MC and generation tests) is the primary clinical metric.

### Caregiver Orchestration

Programs requiring caregiver participation: P4, P5, P8, P9, P12, P14, P16, P18. These use a consistent UI pattern with a caregiver instruction panel (dashed yellow border, 🧑‍🏫 icon).

## Deployment

### GitHub + Vercel (Production)
- Repository: `github.com/syntopicsystems/frameshift`
- Auto-deploys to Vercel on push
- Live at: `frameshift-tau.vercel.app`

### Minimal (Local)
1. Place all `.html` files in the same directory
2. Open `index.html` in a browser
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
| 🗺️ | Explorer | Try 10 programs |
| 🌍 | Globe Trotter | Try all 20 programs |
| 🔥 | On Fire | 5-day play streak |
| ⭐ | Dedicated | Complete 10 sessions |
| 🥇 | First Mastery | Master any program |
| 🏆 | Five Star | Master 5 programs |
| 🌟 | Ten Star | Master 10 programs |
| 👑 | FrameShift Master | Master all 20 programs |
| 🔗 | Equivalence Pro | Master programs 3–6 |
| 🧠 | Abstract Thinker | Master programs 7–10 |
| ⛓️ | Chain Master | Master programs 11–14 |
| 💎 | Quarter Century | Complete 25 sessions |
| 🔮 | Fifty & Fabulous | Complete 50 sessions |

## Known Limitations

- No server-side persistence — progress is `localStorage` only
- No multi-user support (single learner per browser profile)
- Caregiver scoring is honor-system (no automated speech recognition)
- Emoji rendering varies by platform (most consistent on modern browsers)
- CDN dependency for React, Tailwind, Babel (cache for offline use)

## Future Integration Points

- **Progress Tracker API** — server-side persistence
- **PWA wrapper** — installable app with offline support
- **Cross-program analytics** — frame-type profiling, modality profiling, recognition-generation gap analysis
- **Adaptive difficulty** — within-program tier escalation based on performance
- **LLM-generated stimuli** — infinite novel test items for programs with fixed content

---

*Built by AUSPEX. Clinical design by JONATHAN. For Syntopic Systems LLC.*
