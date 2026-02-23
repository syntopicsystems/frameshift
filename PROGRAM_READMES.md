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

---

# Program 11: Chain Reaction — README

**File:** `p11-chain-reaction.html`  
**Clinical Target:** Conditional/causal inference  
**Frame Type:** If A→B and B→C, derive A→C (transitive conditional)  
**Category:** Inference  
**Caregiver Required:** No

## What It Does

Trains conditional relations (if X then Y) across two links, then tests whether the child derives the transitive chain without direct training. Uses cause-and-effect scenarios with everyday objects and events.

## Phase Structure

1. **Train A→B** — "If it rains, the ground gets wet" (8 trials). Mastery: 6/8.
2. **Train B→C** — "If the ground is wet, we wear boots" (8 trials). Mastery: 6/8.
3. **Test A→C** — "If it rains, what do we do?" → wear boots (derived, no feedback, 8 trials).

## Tracker Integration

Saves: B→C as train, A→C as test. Mastery = test phase reached.

---

# Program 12: Value Chain — README

**File:** `p12-value-chain.html`  
**Clinical Target:** Reverse derivation / mutual entailment  
**Frame Type:** Train A→B, derive B→A  
**Category:** Inference  
**Caregiver Required:** No

## What It Does

Trains one-directional relations (A is more valuable than B), then tests whether the child derives the reverse relation (B is less valuable than A) without training. Tests mutual entailment — the foundation of relational frame theory.

## Phase Structure

1. **Training** — Forward relations with corrective feedback (8 trials). Mastery: 6/8.
2. **Test** — Reverse relations, no feedback (8 trials).

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 13: Trait Bridge — README

**File:** `p13-trait-bridge.html`  
**Clinical Target:** Synonym inference / coordination via shared meaning  
**Frame Type:** A means same as B, B means same as C, derive A=C  
**Category:** Inference  
**Caregiver Required:** No

## What It Does

Trains synonym chains across two links, then tests whether the child derives the transitive synonym relation. Uses age-appropriate vocabulary words with visual supports.

## Phase Structure

1. **Train A=B** — Word-to-synonym matching (9 trials). Mastery: 7/9.
2. **Train B=C** — Synonym-to-synonym matching (9 trials). Mastery: 7/9.
3. **Test A=C** — Derived synonym relation, no feedback (9 trials).

## Tracker Integration

Saves: B=C as train, A=C as test. Mastery = test phase reached.

---

# Program 14: Feeling Metaphors — README

**File:** `p14-feeling-metaphors.html`  
**Clinical Target:** Metaphorical/analogical relational framing  
**Frame Type:** Emotion → physical sensation → metaphor (derive emotion=metaphor)  
**Category:** Inference  
**Caregiver Required:** No

## What It Does

Trains the connection between emotions and physical sensations (angry → hot), then sensations and metaphors (hot → "boiling over"), then tests whether the child derives the emotion-metaphor link without training.

## Phase Structure

1. **Train A→B** — Emotion → sensation (8 trials). Mastery: 6/8.
2. **Train B→C** — Sensation → metaphor (8 trials). Mastery: 6/8.
3. **Test A→C** — Emotion → metaphor (derived, no feedback, 8 trials).

## Tracker Integration

Saves: B→C as train, A→C as test. Mastery = test phase reached.

---

# Program 15: Creative Tools — README

**File:** `p15-creative-tools.html`  
**Clinical Target:** Flexible/creative problem-solving  
**Frame Type:** Novel function derivation — using objects in non-standard ways  
**Category:** Social  
**Caregiver Required:** No

## What It Does

Presents problem scenarios where the standard tool is unavailable. The child must select an unconventional substitute from an array of objects. Tests cognitive flexibility and transformation of stimulus function.

## Phase Structure

1. **Training** — 8 scenarios with scaffolding hints. Mastery: 6/8.
2. **Test** — 8 novel scenarios, no hints, no feedback.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 16: What to Share — README

**File:** `p16-what-to-share.html`  
**Clinical Target:** Pragmatic disclosure / social safety framing  
**Frame Type:** Context → audience → appropriate disclosure level  
**Category:** Social  
**Caregiver Required:** No

## What It Does

Presents social scenarios with varying audiences (friend, stranger, teacher, family) and asks whether specific personal information is appropriate to share. Trains contextual discrimination of disclosure.

## Phase Structure

1. **Training** — 8 scenarios with corrective feedback. Mastery: 6/8.
2. **Test** — 8 novel scenarios with novel audience/info combinations, no feedback.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 17: Name That Thing — README

**File:** `p17-name-that-thing.html`  
**Clinical Target:** Descriptive language / circumlocution  
**Frame Type:** Object → multi-feature description  
**Category:** Language  
**Caregiver Required:** Yes

## What It Does

Shows an object and asks the child to describe it using multiple features (color, size, function, category) without naming it. The caregiver scores the description quality. Trains the descriptive relational frame.

## Phase Structure

1. **Training** — 8 items with scaffolding prompts ("What color?", "What does it do?"). Mastery: 6/8.
2. **Test** — 8 novel items, no scaffolding, caregiver scores.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 18: Character Namer — README

**File:** `p18-character-namer.html`  
**Clinical Target:** Naming / labeling relational frame  
**Frame Type:** Features → name derivation  
**Category:** Language  
**Caregiver Required:** Yes

## What It Does

Presents novel characters with visible features and asks the child to generate an appropriate name based on those features. Tests productive naming — creating labels from attribute combinations.

## Phase Structure

1. **Training** — 8 characters with example names and feedback. Mastery: 6/8.
2. **Test** — 8 novel characters, caregiver scores name appropriateness.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 19: Same or Different — README

**File:** `p19-same-or-different.html`  
**Clinical Target:** Equivalence class formation  
**Frame Type:** Odd-one-out / class membership  
**Category:** Equivalence  
**Caregiver Required:** No

## What It Does

Presents groups of items and asks which one doesn't belong. Tests equivalence class formation by requiring the child to identify the shared relation among members and detect the non-member.

## Phase Structure

1. **Training** — 8 trials with corrective feedback. Mastery: 6/8.
2. **Test** — 8 novel groupings, no feedback.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 20: Pronoun Bridge — README

**File:** `p20-pronoun-bridge.html`  
**Clinical Target:** Deictic/pronominal relational framing  
**Frame Type:** Name → pronoun substitution (he/she/they)  
**Category:** Language  
**Caregiver Required:** No

## What It Does

Trains pronoun-referent relations — given a character and context, select the correct pronoun. Tests derived pronoun use in novel sentences.

## Phase Structure

1. **Training** — 10 trials with corrective feedback. Mastery: 8/10.
2. **Test** — 8 novel characters/contexts, no feedback.

## Tracker Integration

Saves: train score/10, test score/8. Mastery = test phase reached.

---

# Program 21: Near & Far — README

**File:** `p21-near-and-far.html`  
**Clinical Target:** Spatial relational framing  
**Frame Type:** Train spatial comparisons, test transitive derivation + perspective reversal  
**Category:** Transformation  
**Caregiver Required:** No

## What It Does

Trains spatial relations between objects (A is nearer than B, B is nearer than C), then tests the derived transitive relation (A is nearer than C) and perspective reversal (from C's viewpoint, what is far?).

## Phase Structure

1. **Train A-B** — Direct spatial comparisons (8 trials). Mastery: 6/8.
2. **Train B-C** — Extended spatial comparisons (8 trials). Mastery: 6/8.
3. **Test A-C** — Transitive derivation (8 trials, no feedback).
4. **Test Y-Z** — Perspective reversal (8 trials, no feedback).

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.

---

# Program 22: First Things First — README

**File:** `p22-first-things-first.html`  
**Clinical Target:** Temporal relational framing  
**Frame Type:** Train before/after sequences, test transitive temporal derivation  
**Category:** Transformation  
**Caregiver Required:** No

## What It Does

Trains temporal ordering (A happens before B, B before C), then tests derived temporal relations (does A happen before C?) and reverse temporal queries (what happened before C?).

## Phase Structure

1. **Train A-B** — Direct temporal pairs (8 trials). Mastery: 6/8.
2. **Train B-C** — Extended temporal pairs (8 trials). Mastery: 6/8.
3. **Test A-C** — Transitive temporal derivation (8 trials, no feedback).
4. **Test Y-Z** — "What happened before/after?" (8 trials, no feedback).

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.

---

# Program 23: Opposite Day — README

**File:** `p23-opposite-day.html`  
**Clinical Target:** Opposition relational framing  
**Frame Type:** Identify dimension of opposition, derive novel opposites  
**Category:** Transformation  
**Caregiver Required:** Yes

## What It Does

Trains opposition relations across multiple dimensions (size, temperature, speed, emotion, height, weight). Child learns to identify the relevant dimension and produce the opposite. Test phase uses novel exemplars on trained dimensions.

## Phase Structure

1. **Training** — 8 trials across dimensions with corrective feedback. Caregiver scores verbal responses. Mastery: 6/8.
2. **Test** — 8 novel opposites on same dimensions, no feedback.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = 75% test accuracy.

---

# Program 24: Spot the Difference — README

**File:** `p24-spot-the-difference.html`  
**Clinical Target:** Distinction relational framing  
**Frame Type:** Identify and verbalize differences between similar items  
**Category:** Transformation  
**Caregiver Required:** Yes

## What It Does

Presents pairs of similar items and asks child to identify what's different. Trains distinction framing — the ability to specify the dimension and direction of difference. Caregiver scores verbal descriptions.

## Phase Structure

1. **Training** — 8 pairs with scaffolding. Mastery: 6/8.
2. **Test** — 8 novel pairs, no scaffolding, caregiver scores.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = 75% test accuracy.

---

# Program 25: Feeling Flip — README

**File:** `p25-feeling-flip.html`  
**Clinical Target:** Emotional opposition / combinatorial entailment  
**Frame Type:** Emotion → opposite emotion, derive novel emotional opposites  
**Category:** Transformation  
**Caregiver Required:** Yes

## What It Does

Trains emotion-opposite relations (happy↔sad, brave↔scared, calm↔angry). Tests derived emotional opposites and combinatorial entailment — if A is the opposite of B and B is the opposite of C, what is A to C?

## Phase Structure

1. **Training** — 8 emotion-opposite pairs with corrective feedback. Caregiver scores verbal production. Mastery: 6/8.
2. **Test** — 8 novel scenarios requiring derived emotional opposites, no feedback.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = 75% test accuracy.

---

# Program 26: Season Sense — README

**File:** `p26-season-sense.html`  
**Clinical Target:** Deictic/seasonal comparison and reversal  
**Frame Type:** Season → characteristics, derive comparisons and reversals  
**Category:** Transformation  
**Caregiver Required:** No

## What It Does

Trains seasonal characteristics and comparisons (summer is hotter than winter), then tests deictic reversal — from winter's perspective, summer is the hot one; from summer's perspective, winter is the cold one.

## Phase Structure

1. **Train A-B** — Season-characteristic associations (8 trials). Mastery: 6/8.
2. **Train B-C** — Cross-season comparisons (8 trials). Mastery: 6/8.
3. **Test** — Deictic reversal and derived comparisons (8 trials, no feedback).

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.

---

# Program 27: Weather Switch — README

**File:** `p27-weather-switch.html`  
**Clinical Target:** Transformation via transitive derivation  
**Frame Type:** Train A-B (same weather across settings), B-C (weather→opposite), Test A-C (transitive), Y-Z (weather→clothing)  
**Category:** Transformation  
**Caregiver Required:** No

## What It Does

Trains weather-setting associations and weather-opposite relations, then tests transitive derivation (scene A → opposite weather, never directly trained) and functional application (weather scene → clothing for opposite weather).

## Phase Structure

1. **Train A-B** — Same weather across settings (8 trials). Mastery: 6/8.
2. **Train B-C** — Weather → opposite weather (8 trials). Mastery: 6/8.
3. **Test A-C** — Transitive derivation (8 trials, no feedback).
4. **Test Y-Z** — Weather scene → clothing for opposite (8 trials, no feedback).

## Stimuli

6 weather types: sunny/rainy, snowy/hot, windy/calm. Each with 2 scenes and matched clothing items.

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.

---

# Program 28: Family Flip — README

**File:** `p28-family-flip.html`  
**Clinical Target:** Opposition within family role category  
**Frame Type:** Verbal production of opposite relative titles  
**Category:** Transformation  
**Caregiver Required:** Yes

## What It Does

Trains opposite family role relations (Mom↔Dad, Aunt↔Uncle, Grandma↔Grandpa, Sister↔Brother, Niece↔Nephew). Caregiver scores verbal production of opposite titles. Test phase uses MC + verbal formats.

## Phase Structure

1. **Training** — Verbal production: "Say the opposite of [relative title]." Caregiver scored with ✅/🟡/❌. (8 trials). Mastery: 6/8.
2. **Test Y-Z** — MC format + verbal: show family member, pick opposite from array. (8 trials, no feedback).

## Tracker Integration

Saves: train score/8, test score/8. Mastery = 75% test accuracy.

---

# Program 29: Taste Match — README

**File:** `p29-taste-match.html`  
**Clinical Target:** Taste-based equivalence class formation  
**Frame Type:** Match foods by shared taste, derive class membership  
**Category:** Equivalence  
**Caregiver Required:** No

## What It Does

Trains taste-based equivalence classes (salty foods go together, sweet foods go together), then tests class membership via odd-one-out and functional substitution (menu ordering: "you don't feel like X, what else might you try?").

## Phase Structure

1. **Training** — Match foods with same taste (8 trials). Mastery: 6/8.
2. **Test odd-one-out** — Which doesn't taste the same? (8 trials, no feedback).
3. **Test Y-Z** — Menu substitution scenarios (8 trials, no feedback).

## Stimuli

4 taste groups: Salty (pretzel, chips, popcorn, crackers), Sweet (cookie, cake, candy, ice cream), Fruity (apple, grape, orange, strawberry), Sour/Tangy (lemon, pickle, yogurt, grapefruit).

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.

---

# Program 30: What's It Like? — README

**File:** `p30-whats-it-like.html`  
**Clinical Target:** Feature abstraction via circular derivation  
**Frame Type:** A→B (feature→item), B→C (item→name), Test C→A (name→feature, derived)  
**Category:** Abstraction  
**Caregiver Required:** Yes (Y-Z trials)

## What It Does

Trains feature-to-item and item-to-name relations, then tests the derived circular relation (name→feature). Y-Z trials require the child to pick an item and verbally describe its feature, scored by caregiver.

## Phase Structure

1. **Train A-B** — Feature → pick item (8 trials). Mastery: 6/8.
2. **Train B-C** — Item → name (8 trials). Mastery: 6/8.
3. **Test C-A** — Name → feature (derived, 8 trials, no feedback).
4. **Test Y-Z** — Pick item + describe feature (caregiver scored, 4 trials).

## Stimuli

8 items: salty pretzel, sweet cookie, cold ice cream, crunchy carrot, soft teddy, sharp pencil, smooth egg, warm cocoa.

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.

---

# Program 31: Where Would You Go? — README

**File:** `p31-where-would-you-go.html`  
**Clinical Target:** Location-based inference and problem-solving  
**Frame Type:** A→B (location→items), Test B→A (reverse), Y-Z (scenario problem-solving)  
**Category:** Inference  
**Caregiver Required:** No

## What It Does

Trains location-item associations (what you find at each place), then tests reverse derivation (given an item, where would you find it?) and functional application (scenario: "you need to fix your bike — where would you go?").

## Phase Structure

1. **Train A-B** — Location → items found there (8 trials). Mastery: 6/8.
2. **Test B-A** — Item → location (reverse, 8 trials, no feedback).
3. **Test Y-Z** — Problem scenarios → location inference (6 trials, no feedback).

## Stimuli

6 locations: Garage, Kitchen, Library, Beach, Hospital, Park. Each with 3 associated items.

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.

---

# Program 32: Here & There — README

**File:** `p32-here-and-there.html`  
**Clinical Target:** Deictic relational framing (HERE/THERE reversal)  
**Frame Type:** Learn object locations, test perspective reversal when locations swap  
**Category:** Transformation  
**Caregiver Required:** Yes (Y-Z trials)

## What It Does

Trains HERE/THERE location assignments for objects across location pairs, then tests what happens when perspective reverses — if you were THERE instead of HERE, what would be near you? Y-Z trials require verbal prediction of swaps, scored by caregiver.

## Phase Structure

1. **Training** — Learn which objects are HERE vs. THERE (8 trials). Mastery: 6/8.
2. **Test reversal** — If locations swap, what's HERE/THERE now? (8 trials, no feedback).
3. **Test Y-Z** — Pick preferred location, predict swap consequences (caregiver scored, 4 trials).

## Stimuli

6 location pairs: Classroom/Playground, Living Room/Backyard, City/Farm, Mountain/Ocean, Winter/Summer, Morning/Night. Each with 2 objects.

## Tracker Integration

Saves: training as train, test as test. Mastery = 75% test accuracy.
