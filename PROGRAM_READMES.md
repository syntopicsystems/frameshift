# Program 1: More or Less — README

**File:** `p1-more-or-less.html`  
**Clinical Target:** Comparative relational framing  
**Frame Type:** Translation (more/less/same)  
**Category:** Translation  
**Caregiver Required:** No

## What It Does

Presents pairs of objects differing on a single dimension (quantity, size, length, weight) and asks "Which has MORE?" or "Which has LESS?" Uses inline SVG illustrations on a meadow-green gradient background.

## Phase Structure

Single-phase design (12 trials). No separate test phase in v1 — the session mixes comparison types to assess general comparative framing.

- **Mastery threshold:** 8/12 correct
- **Feedback:** Correct → green highlight + ascending chime. Incorrect → gentle wiggle + explanation of the correct comparison.

## Stimuli

4 dimension types, each with multiple exemplar pairs:
- **Quantity:** apples, stars, dots (countable arrays)
- **Size:** animals, objects (visual size comparison)
- **Length:** snakes, pencils, rivers (horizontal extent)
- **Weight:** conceptual (elephant vs. feather, etc.)

Comparison direction (MORE vs. LESS) randomizes per trial.

## Tracker Integration

Saves: `trainScore` = correct count, `trainMax` = 12, no test phase, mastery = score ≥ 8.

## Design Notes

- SVG illustrations are inline (no external images)
- Meadow gradient background (#ECFDF5 → #D1FAE5 → #A7F3D0)
- Progress shown as dot indicators along bottom

---

# Program 2: Same & Different — README

**File:** `p2-same-and-different.html`  
**Clinical Target:** Coordination and distinction frames  
**Frame Type:** Same/Different classification  
**Category:** Translation  
**Caregiver Required:** No

## What It Does

Presents pairs of objects and asks whether they are the SAME or DIFFERENT. Uses OpenMoji emoji on a cork-board aesthetic. Covers identity (exact match), category (same type, different instance), and feature-based (shared color, shape, etc.) comparisons.

## Phase Structure

Single-phase design (12 trials).

- **Mastery threshold:** 9/12 correct
- **Feedback:** Correct → pop animation + chime. Incorrect → wiggle + explanation.

## Stimuli

Pairs drawn from OpenMoji emoji pool. Three comparison types:
- **Identity:** same emoji vs. same emoji
- **Category:** dog vs. cat (both animals — SAME category; dog vs. car — DIFFERENT)
- **Feature:** red apple vs. red car (SAME color)

## Tracker Integration

Saves: `trainScore` = correct count, `trainMax` = 12, no test phase, mastery = score ≥ 9.

---

# Program 3: Symbol Bridge — README

**File:** `p3-symbol-bridge.html`  
**Clinical Target:** Stimulus equivalence  
**Frame Type:** If A=B and B=C, does A=C emerge?  
**Category:** Equivalence  
**Caregiver Required:** No

## What It Does

Trains arbitrary symbol-symbol relations across two phases (A→B, B→C), then tests whether the derived A→C relation emerges without training. Uses abstract symbols (geometric shapes) on a lavender workspace background to ensure the relations are truly arbitrary (not based on pre-existing knowledge).

## Phase Structure

Three phases, gated by mastery:
1. **Phase AB** — Train A→B relations (3 classes × 3 reps = 9 trials). Mastery: 7/9.
2. **Phase BC** — Train B→C relations (9 trials). Mastery: 7/9.
3. **Phase AC** — Test derived A→C (9 trials). **No corrective feedback.** "Response recorded."

## Stimuli

3 equivalence classes with arbitrary symbols:
- Class 1: A1 → B1 → C1
- Class 2: A2 → B2 → C2
- Class 3: A3 → B3 → C3

Symbols are abstract geometric SVGs to prevent semantic mediation.

## Tracker Integration

Saves: `trainScore` = BC phase score (last training phase), `trainMax` = 9, `testScore` = AC phase score, `testMax` = 9, mastery = AC phase completed.

Handles React async state via `currentPhase` variable to avoid stale `phaseScores` reads.

---

# Program 4: Scent Match — README

**File:** `p4-scent-match.html`  
**Clinical Target:** Cross-modal olfactory equivalence  
**Frame Type:** Visual → Label → Scent (A=B, B=C, test A=C)  
**Category:** Equivalence  
**Caregiver Required:** Yes

## What It Does

Extends stimulus equivalence to the olfactory modality. Training: picture → label (Phase AB), label → scent (Phase BC, caregiver presents physical scent). Test: picture → scent (Phase AC) — derived cross-modal relation.

## Phase Structure

Three phases, caregiver-orchestrated:
1. **Phase AB** — Picture → Label matching (digital, 9 trials)
2. **Phase BC** — Label → Scent matching (caregiver presents scent, confirms response, 9 trials)
3. **Phase AC** — Picture → Scent (derived, no feedback, 9 trials)

## Stimuli

3 scent classes:
- Rose (visual: 🌹, scent: rose/floral)
- Lemon (visual: 🍋, scent: citrus)
- Mint (visual: 🌿, scent: mint/herbal)

Caregiver setup screen lists required physical materials.

## Tracker Integration

Same pattern as P3: saves BC as train, AC as test. Timing-safe via `currentPhase`.

---

# Program 5: Taste Test — README

**File:** `p5-taste-test.html`  
**Clinical Target:** Cross-modal gustatory equivalence + vocal production  
**Frame Type:** Visual → Label → Taste, with expressive vocal scoring  
**Category:** Equivalence  
**Caregiver Required:** Yes

## What It Does

Like P4 but for gustatory modality, with the added requirement of vocal production. The caregiver presents taste samples and scores the child's spoken response using a 3-level vocal scoring UI.

## Phase Structure

1. **Phase AB** — Picture → Label (digital, 9 trials)
2. **Phase BC** — Label → Taste (caregiver presents taste, 3-level vocal scoring, 9 trials)
3. **Phase AC** — Picture → Taste (derived, vocal scoring, no corrective feedback, 9 trials)

## Vocal Scoring UI

Caregiver scores each response as:
- ✅ **Correct** — said the right word
- 🟡 **Partial** — approximation or related word
- ❌ **Incorrect** — wrong word or no response

Plus a text field for the actual utterance.

## Stimuli

3 taste classes: Sweet (honey), Sour (lemon), Salty (pretzel). Pink kitchen aesthetic.

## Tracker Integration

Same as P3/P4. BC = train, AC = test.

---

# Program 6: Common Features — README

**File:** `p6-common-features.html`  
**Clinical Target:** Analogical reasoning via shared features  
**Frame Type:** B→A (what feature?), C→A (what feature?), derive C→B (what animal shares this feature?)  
**Category:** Equivalence  
**Caregiver Required:** No

## What It Does

Trains feature-animal associations, then tests whether the child derives that two animals sharing a feature must be related to each other. This is analogical reasoning — the hardest equivalence relation.

## Phase Structure

1. **Phase BA** — "What does a Tiger have?" → Stripes (9 trials)
2. **Phase CA** — "What does a Zebra have?" → Stripes (9 trials)
3. **Phase CB** — "What animal has something in common with Zebra?" → Tiger (**derived, no feedback**, 9 trials)

## Stimuli — Tier 1

| Feature | Animal B | Animal C |
|---------|----------|----------|
| Stripes | Tiger 🐯 | Zebra 🦓 |
| Spikes | Porcupine (custom SVG) | Hedgehog 🦔 |
| Scales | Snake 🐍 | Fish 🐟 |

Custom inline SVG for Porcupine because OpenMoji uses the same emoji (1F994) for both porcupine and hedgehog.

## Diagnostic Error Tracking

Logs not just correct/incorrect but *which wrong animal* was chosen and what feature class the error maps to. Clinically valuable for profiling analogical reasoning breakdown patterns.

## Tracker Integration

Saves: CA = train, CB = test, mastery = CB completed. Timing-safe via `currentPhase`.

---

# Program 7: What Kind of Story? — README

**File:** `p7-what-kind-of-story.html`  
**Clinical Target:** Genre abstraction / categorical relational framing  
**Frame Type:** Extract abstract category rule from exemplars, apply to novel instances  
**Category:** Abstraction  
**Caregiver Required:** No

## What It Does

Presents short stories (4 pages each, with page-turn UI and Web Speech API narration option). After reading, the child classifies the story by genre. Training uses corrective feedback; test uses novel, never-seen stories with no feedback. This is hierarchical relational framing — relating instances to abstract categories.

## Phase Structure

1. **Training** — 16 stories (4 genres × 4 stories), interleaved order. Mastery: 12/16.
2. **Test** — 16 novel stories (4 genres × 4 new stories). No corrective feedback. "Response recorded."

## Content

**32 original stories** written specifically for this program (no copyrighted material):
- **Mystery** (4+4): Missing Cookie, Strange Footprints, Mr. Whiskers, Vanishing Lunch / Midnight Sound, Garden Thief, Missing Paintbrush, Who Drew on the Wall?
- **Non-Fiction** (4+4): How Bees Make Honey, Why Leaves Change Color, Your Amazing Heart, How Clouds Form / Water Cycle, How Seeds Travel, Why the Sky Is Blue, Amazing Octopuses
- **History** (4+4): Moon Landing, Great Fire of London, First Airplane, Pompeii / Titanic, Egyptian Pyramids, Ice Age, First Olympics
- **Fantasy** (4+4): Dragon's Garden, Talking Fish, Cloud Painter, Boy Who Grew Wings / Invisible Library, Night Market, Girl Made of Glass, Upside-Down Mountain

## Key Features

- **Bookcase component** — fills with color-coded book spines as training progresses
- **Page-turn UI** with Web Speech API narration (🔊 button)
- **Genre-specific colors** — Mystery (purple), Non-Fiction (blue), History (amber), Fantasy (green)
- **Confusion pair logging** — tracks which genre pairs are confused (mystery↔history vs fantasy↔non-fiction)

## Tracker Integration

Saves: train score/16, test score/16. Mastery = test phase reached. Timing-safe.

---

# Program 8: The Why Detective — README

**File:** `p8-why-detective.html`  
**Clinical Target:** Interrogative relational frame (why → because → reason → action)  
**Frame Type:** Using "why" questions to access causal information for decision-making  
**Category:** Abstraction  
**Caregiver Required:** Yes (for verbal interactions)

## What It Does

Presents social scenarios with multiple characters, each with a different REASON for their situation. A big animated "❓ Ask WHY" button reveals speech bubbles showing each character's reason. The child must use the revealed causal information to select the correct person.

## Phase Structure

1. **Training** — 8 scenarios. If child acts WITHOUT asking why → "Hmm, how do you know? Try asking why first!" Mastery: 6/8.
2. **Test** — 8 novel scenarios. No prompting to ask why. **Tracks whether child asked why before choosing** — this is the real clinical signal.

## JONATHAN's Enhancement

Rather than just testing compliance ("did they press the button?"), scenarios are designed so multiple characters have different reasons, and the reason *disambiguates* the correct action. This makes the causal logic explicit rather than incidental.

## Key Clinical Metric

End screen shows:
- Accuracy (correct person chosen)
- **Why-asking rate** (percentage of trials where child asked why before acting)

The why-asking rate in the unprompted test phase is the primary clinical outcome measure.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached. Timing-safe.

---

# Program 9: What Kind? — README

**File:** `p9-what-kind.html`  
**Clinical Target:** Descriptive/qualifier frame (adjective production)  
**Frame Type:** Object → "What kind of [object]?" → Adjective  
**Category:** Abstraction  
**Caregiver Required:** Optional (for vocal scoring)

## What It Does

Shows a picture of an object. Two-step flow:
1. "What is this?" → Caregiver confirms child named the object
2. "What KIND of [object]?" → Caregiver scores the adjective response

Tests whether the child spontaneously produces descriptive qualifiers when prompted.

## Phase Structure

1. **Training** — 10 items across 4 feature dimensions (size, color, texture, quality). Scaffolding hints available. Mastery: 8/10.
2. **Test** — 8 novel items. No scaffolding, no corrective feedback.

## Scoring

Three-level caregiver scoring:
- ✅ **Target adjective** — said the expected word (e.g., "big" for big dog)
- 🟡 **Alternative valid** — different but accurate descriptor (e.g., "fluffy" instead of "big")
- ❌ **No adjective** — repeated noun or no response

Plus text field for actual utterance.

## End Screen Analytics

- **Vocabulary breadth** — unique adjectives used (displayed as tag cloud)
- **Dimension breakdown** — accuracy by feature type (size, color, texture, quality)

## Tracker Integration

Saves: train score/10, test score/8. Mastery = test phase reached. Timing-safe.

---

# Program 10: What Comes Next? — README

**File:** `p10-what-comes-next.html`  
**Clinical Target:** Inductive pattern abstraction  
**Frame Type:** Identify changing feature dimension, extract rule, apply to novel sequence  
**Category:** Abstraction  
**Caregiver Required:** Tier 4 only (not implemented in v1)

## What It Does

Presents sequences of colored shapes on a "conveyor belt" with an empty slot at the end. The child selects the correct next item from a 4-option array. This requires simultaneously identifying which feature is changing (color), extracting the rule (cycling/alternating), and selecting the correct answer while ignoring distractors.

## Phase Structure

1. **Training (Tier 1)** — 8 patterns. Same shape throughout, color changes. Scaffolding: color glow on sequence items, "Look at the COLORS" hint after errors. Scaffolding fades with correct answers. Mastery: 6/8.
2. **Test (Tier 2)** — 8 novel patterns. Shape changes every item, only color pattern holds. No scaffolding, no feedback.

## Distractor Logic

Per JONATHAN's spec, every choice array contains exactly:
- **Correct answer** — continues the pattern on the target dimension
- **Repetition error** — copies the last item (tests whether child is just repeating)
- **Wrong-dimension error** — matches on a non-target feature (e.g., right shape, wrong color)
- **Unrelated** — completely different (catch trial)

## Error Type Tracking

End screen shows error breakdown:
- Repetition errors (copying last item)
- Wrong-dimension errors (attending to wrong feature)
- Random/unrelated errors

Cross-reference with P6: if a child struggles with both feature abstraction (P6) and inductive patterns (P10), that's a convergent signal about analogical reasoning capacity.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached. Timing-safe.
