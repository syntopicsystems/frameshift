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

Same pattern as P3: saves BC as train, AC as test.

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

## Tracker Integration

Saves: CA = train, CB = test, mastery = CB completed.

---

# Program 7: What Kind of Story? — README

**File:** `p7-what-kind-of-story.html`  
**Clinical Target:** Genre abstraction / categorical relational framing  
**Frame Type:** Extract abstract category rule from exemplars, apply to novel instances  
**Category:** Abstraction  
**Caregiver Required:** No

## What It Does

Presents short stories (4 pages each, with page-turn UI and Web Speech API narration option). After reading, the child classifies the story by genre. Training uses corrective feedback; test uses novel, never-seen stories with no feedback.

## Phase Structure

1. **Training** — 16 stories (4 genres × 4 stories), interleaved order. Mastery: 12/16.
2. **Test** — 16 novel stories (4 genres × 4 new stories). No corrective feedback.

## Content

**32 original stories** across 4 genres: Mystery, Non-Fiction, History, Fantasy.

## Tracker Integration

Saves: train score/16, test score/16. Mastery = test phase reached.

---

# Program 8: The Why Detective — README

**File:** `p8-why-detective.html`  
**Clinical Target:** Interrogative relational frame (why → because → reason → action)  
**Frame Type:** Using "why" questions to access causal information for decision-making  
**Category:** Abstraction  
**Caregiver Required:** Yes (for verbal interactions)

## What It Does

Presents social scenarios. A "❓ Ask WHY" button reveals speech bubbles showing each character's reason. The child must use the revealed causal information to select the correct person.

## Phase Structure

1. **Training** — 8 scenarios. Mastery: 6/8.
2. **Test** — 8 novel scenarios. Tracks whether child asked why before choosing.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 9: What Kind? — README

**File:** `p9-what-kind.html`  
**Clinical Target:** Descriptive/qualifier frame (adjective production)  
**Frame Type:** Object → "What kind of [object]?" → Adjective  
**Category:** Abstraction  
**Caregiver Required:** Optional (for vocal scoring)

## What It Does

Shows a picture. "What KIND of [object]?" → Caregiver scores the adjective response.

## Phase Structure

1. **Training** — 10 items. Mastery: 8/10.
2. **Test** — 8 novel items. No scaffolding, no corrective feedback.

## Tracker Integration

Saves: train score/10, test score/8. Mastery = test phase reached.

---

# Program 10: What Comes Next? — README

**File:** `p10-what-comes-next.html`  
**Clinical Target:** Inductive pattern abstraction  
**Frame Type:** Identify changing feature dimension, extract rule, apply to novel sequence  
**Category:** Abstraction  
**Caregiver Required:** No

## What It Does

Presents sequences of colored shapes on a "conveyor belt" with an empty slot. The child selects the correct next item from a 4-option array.

## Phase Structure

1. **Training (Tier 1)** — 8 patterns. Mastery: 6/8.
2. **Test (Tier 2)** — 8 novel patterns. No scaffolding, no feedback.

## Tracker Integration

Saves: train score/8, test score/8. Mastery = test phase reached.

---

# Program 11: Chain Reaction — README

**File:** `p11-chain-reaction.html`  
**Clinical Target:** Transitive conditional inference (forward chaining)  
**Frame Type:** Train A→B→C, test derived A→C  
**Category:** Inference  
**Caregiver Required:** No

## What It Does

Trains conditional chains: "If A then B" and "If B then C." Tests whether the child derives "If A then C" — the transitive inference that was never directly taught. Uses real-world cause-and-effect chains (e.g., homework not done → bad grade → trouble).

## Phase Structure

1. **Training** — 6 chains, each with 3 questions (A→B check, B→C check, A→C derivation with bridge screen). 18 training questions total. Corrective feedback.
2. **Test** — 4 novel chains, same structure. 12 test questions. Neutral "Response recorded" feedback.

## Stimuli

Training: homework→bad grade→trouble, dam breaks→flooding→evacuate, practice→improve→win, alarm→wake up→school on time, clouds→rain→puddles, seed→plant→flower

Test: no study→fail→summer school, eat too much candy→stomachache→miss party, save money→buy bike→ride to park, forget umbrella→get wet→catch cold

## Key Design: Derivation Tracking

A→C questions tracked separately from A→B and B→C checks. The A→C derivation accuracy is the primary clinical signal — and the key distractor is B (the intermediate step), which tests whether the child is truly chaining vs. just recalling a single link.

## Tracker Integration

Saves: trainScore/18, testScore/12. Separate derivation accuracy displayed on end screen.

---

# Program 12: Value Chain — README

**File:** `p12-value-chain.html`  
**Clinical Target:** Reverse derivation with recognition-to-generation progression  
**Frame Type:** Train A→B→C (action→outcome→value), test C→A (value→action)  
**Category:** Inference  
**Caregiver Required:** Yes (for generation phase)

## What It Does

Trains forward chains from concrete actions to abstract values (e.g., share toys → fun together → generosity). Tests reverse derivation: given the value, can the child identify or produce the action? Three-phase architecture with a critical generation phase.

## Phase Structure

1. **Training** — 6 triads. Per triad: teach A→B, check A→B, teach B→C, check B→C, bridge screen ("think backwards"), check C→A multiple choice. 18 questions. Corrective feedback.
2. **Test MC** — 4 novel triads, same structure. 12 questions. Neutral feedback.
3. **Test Generation** — Same 4 test triads. Child hears value C, must spontaneously produce action A. Caregiver types response and scores ✅/🟡/❌.

## Clinical Signal: Recognition vs. Generation

The same novel triads appear in both Test MC and Test Generation, allowing direct comparison of recognition (selecting from options) vs. generation (producing from nothing) on identical stimuli.

## Tracker Integration

Saves: trainScore/18, combined test score (MC + generation correct) / 16.

---

# Program 13: Trait Bridge — README

**File:** `p13-trait-bridge.html`  
**Clinical Target:** Cross-modal equivalence via synonymous trait chains  
**Frame Type:** Picture A → Trait B → Synonym C, test C → Picture A  
**Category:** Inference  
**Caregiver Required:** No

## What It Does

Trains two links: a picture matches a trait (race car → "speedy"), and that trait has a synonym ("speedy" ≈ "fast"). Tests the derived relation: given the synonym "fast," can the child select the original picture (race car)?

## Phase Structure

Per item: teach A→B, check A→B, teach B→C (synonym), check B→C, bridge screen, check C→A (picture selection). 6 training items (18 questions), 4 test items (12 questions).

## Stimuli

Training: race car/speedy/fast, rat/gross/dirty, fox/sly/clever, turtle/slow/unhurried, lion/fierce/brave, owl/wise/smart

Test: snake/sneaky/tricky, elephant/enormous/huge, bee/busy/hardworking, eagle/sharp-eyed/watchful

## Tracker Integration

Saves: trainScore/18, testScore/12. Separate derivation (C→A) accuracy tracked.

---

# Program 14: Feeling Metaphors — README

**File:** `p14-feeling-metaphors.html`  
**Clinical Target:** Multi-relation emotional metaphor understanding  
**Frame Type:** Train A-B (emotion→face), C-D (metaphor→picture), B-D (face→metaphor picture), test C→A (metaphor→emotion)  
**Category:** Inference  
**Caregiver Required:** Yes (for generation phase)

## What It Does

The most complex relational network in the suite. Trains three separate relations that share no common element, then tests whether the child can traverse the entire network: "If someone feels like 'rain,' how do they feel?" This requires deriving through face↔metaphor picture↔emotion connections.

## Phase Structure

1. **Training** — 6 emotion sets. Per set: teach A→B (emotion→face), check A→B, teach C→D (metaphor→picture), check C→D, teach B→D (face→metaphor picture), check B→D. 18 training questions.
2. **Test MC** — 4 novel sets. Given metaphor word C + metaphor picture D, select emotion word A. 4 questions.
3. **Test Generation** — Same 4 sets. "Someone feels like [metaphor]. How do they feel?" Caregiver-scored.

## Stimuli

Training: sad/😢/rain/🌧️, angry/😠/fire/🔥, happy/😊/rainbow/🌈, scared/😨/storm/⛈️, calm/😌/still water/🏞️, excited/🤩/fireworks/🎆

Test: lonely/😔/desert/🏜️, surprised/😲/lightning/⚡, proud/😤/mountain top/🏔️, confused/😵‍💫/maze/🌀

## Tracker Integration

Saves: trainScore/18, combined MC + generation / 8.

---

# Program 15: Creative Tools — README

**File:** `p15-creative-tools.html`  
**Clinical Target:** Flexible problem-solving / non-obvious tool use  
**Frame Type:** Task + two improper tools → select more suitable one  
**Category:** Flexibility  
**Caregiver Required:** No

## What It Does

NOT "hammer a nail → use a hammer." Instead: "Pound a nail — heavy book or teddy bear?" Encourages creative lateral thinking about tool properties rather than conventional associations.

## Phase Structure

1. **Training** — 8 tasks with corrective feedback + explanations. Mastery: 6/8 (75%).
2. **Test** — 6 novel tasks. Neutral "Response recorded" feedback.

## Stimuli

Training: pound nail (book vs teddy), fan yourself (newspaper vs brick), knock bowling pin (basketball vs folder), carry water (rubber boot vs newspaper), reach high shelf (broom vs mitten), hold door open (thick book vs tissue), draw straight line (ruler vs scarf), scoop sand (large spoon vs toothbrush)

Test: hold marbles (ladle vs open book), prop wobbly table (deck of cards vs feather), cut tape (key vs sponge), dig hole in dirt (metal spoon vs sock), signal far away (mirror vs paper clip), flatten wrinkled shirt (hot pan vs stuffed animal)

## Tracker Integration

Saves: trainScore/8, testScore/6.

---

# Program 16: What to Share — README

**File:** `p16-what-to-share.html`  
**Clinical Target:** Social pragmatics and information safety  
**Frame Type:** Situation → appropriate information disclosure  
**Category:** Social  
**Caregiver Required:** Yes (for generation phase)

## What It Does

Presents social situations where someone asks the child for information. The child must determine what is safe and appropriate to share based on who is asking (trusted adult, acquaintance, stranger, online person).

## Phase Structure

1. **Training MC** — 8 scenarios with corrective feedback + safety explanations. Mastery: 6/8 (75%).
2. **Test MC** — 4 novel scenarios. Neutral feedback.
3. **Test Generation** — 4 novel scenarios. No choices — child produces their own response. Caregiver-scored.

## Safety Levels

Each scenario tagged: safe (family, doctor), acquaintance (bus driver, cashier), unsafe (stranger, online).

## Stimuli

Training includes: Mom asks about school (safe), stranger asks where you live (unsafe), bus driver asks about your day (acquaintance), doctor asks what hurts (safe), new kid asks for phone number (acquaintance), teacher asks why you're late (safe), someone online asks your school (unsafe), grandma asks what you want for birthday (safe).

## Tracker Integration

Saves: trainScore/8, combined MC + generation / 8.

---

# Program 17: Name That Thing — README

**File:** `p17-name-that-thing.html`  
**Clinical Target:** Description comprehension → object identification  
**Frame Type:** Read figurative/indirect description → select matching picture  
**Category:** Language  
**Caregiver Required:** No

## What It Does

Presents a written description using figurative language, analogy, or indirect reference. The child selects which picture matches. Difficulty is scaled for a 10-year-old strong reader — descriptions use metaphor ("nature's skyscraper"), analogy ("an underwater architect"), and indirect reference rather than straightforward definitions.

## Phase Structure

1. **Training** — 8 items (3 Tier 1 easier + 5 Tier 2 harder). Corrective feedback. Mastery: 6/8 (75%).
2. **Test** — 6 items (all Tier 2). Neutral feedback.

## Stimuli Examples

- "A kitchen tool shaped like a small bowl on a long handle" → ladle
- "A flying machine without an engine — it rides invisible rivers of rising warm air" → glider
- "A bird that can't fly but swims like a torpedo and wears a permanent tuxedo" → penguin
- "The world's slowest clock — dripping water builds a stone icicle hanging from a cave ceiling" → stalactite

## Tracker Integration

Saves: trainScore/8, testScore/6.

---

# Program 18: Character Namer — README

**File:** `p18-character-namer.html`  
**Clinical Target:** Trait-based creative naming (feature→label generation)  
**Frame Type:** See character traits → select then produce characteristic name  
**Category:** Language  
**Caregiver Required:** Yes (for generation phase)

## What It Does

Presents a cartoon character (emoji) with described traits. In training, the child selects the best fitting name from options. In the generation test, the child invents their own name — the key clinical signal.

## Phase Structure

1. **Training MC** — 8 characters with corrective feedback. Mastery: 6/8 (75%).
2. **Test MC** — 4 novel characters. Neutral feedback.
3. **Test Generation** — 4 novel characters. Child invents a name. Caregiver scores: ✅ Creative (connects to traits) / 🟡 Okay (weak connection) / ❌ Random (no connection).

## Stimuli

Training: teddy bear→Mr. Fluffums (soft/fluffy), rabbit→Hoppy (bouncy), elephant→Snouty (big trunk), lion→Furrocious (furry/fierce), turtle→Shelldon (slow/steady), owl→Professor Hoot (wise), frog→Ribbit Ron (green/jumpy), fox→Trixie (clever/sneaky)

Test MC: octopus→Twisty, flamingo→Pinky Ballerina, snail→Homey Slowsworth, parrot→Chatty Rainbow

Test Gen: snake (slithery/hissy), shark (big teeth/fast), bee (buzzes/honey), crab (pinchy/sideways)

## Tracker Integration

Saves: trainScore/8, combined MC + generation / 8.

---

# Program 19: Same or Different (Equivalence Classes) — README

**File:** `p19-same-or-different.html`  
**Clinical Target:** Equivalence class formation through same/different judgments  
**Frame Type:** Train A-B same, A-C different → derive untrained D-B/C + odd-one-out  
**Category:** Categorization  
**Caregiver Required:** No

## What It Does

Establishes equivalence classes through explicit same/different training, then tests whether the child can make derived judgments about novel pairings and identify intruders in groups. This is the formal equivalence class paradigm.

## Phase Structure

1. **Training** — 4 sets. Per set: A-B same, A-C different, C-D same, C-A different. 16 trials. Corrective feedback. Mastery: 12/16 (75%).
2. **Test Same/Different** — 3 novel sets. Tests D-B different and D-C same — pairings never seen together. Neutral feedback.
3. **Test Odd-One-Out** — Same 3 sets. Shows {A, B, D} where D is the intruder, and {C, D, B} where B is the intruder. Neutral feedback.

## Stimuli

Training: chicken/cow vs scissors/paper, car/bus vs chair/couch, apple/banana vs shirt/pants, guitar/piano vs soccer ball/basketball

Test: fish/octopus vs cloud/airplane, fire/sun vs snowflake/ice cube, pencil/pen vs frying pan/spoon

## Tracker Integration

Saves: trainScore/16, combined testSd + testOdd scores.

---

# Program 20: Pronoun Bridge — README

**File:** `p20-pronoun-bridge.html`  
**Clinical Target:** Pronoun class equivalence and contextual application  
**Frame Type:** Train pronoun→same-class pronoun (A→B), pronoun→picture (B→C), test: fill pronouns in stories  
**Category:** Language  
**Caregiver Required:** No

## What It Does

Trains pronoun family membership (he/him/his go together, she/her/her go together, etc.) and pronoun-to-referent mapping. Tests application in real written sentences with blanks.

## Phase Structure

1. **Training** — 12 trials across 4 pronoun families (he, she, they, I). Two relation types: pronoun→same-family pronoun (A→B), pronoun→picture (B→C). Corrective feedback. Mastery: 9/12 (75%).
2. **Test — Story Fill-In** — 6 stories with 2-3 blanks each (~14 blanks total). Real narrative sentences where the child selects the correct pronoun from 3 options per blank. Sentences render live as blanks are filled.

## Pronoun Families

| Subject | Object | Possessive | Picture |
|---------|--------|------------|---------|
| he | him | his | 👦 |
| she | her | her | 👧 |
| they | them | their | 👫 |
| I | me | my | 🙋 |

## Tracker Integration

Saves: trainScore/12, testScore/(total blanks). Mastery = test phase reached.
