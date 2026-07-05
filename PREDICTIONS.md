# Empirical Predictions of the Sentence Deconstruction Engine

**Author:** Joel Robinson
**Status:** Working paper — v1.0
**Repository:** `hallucinations-are-not-random`

---

## Abstract

The Sentence Deconstruction Engine (SDE) formalizes hallucination as a deterministic structural failure in compression/decompression, not a stochastic output property. This document derives the empirical predictions that follow directly from the SDE formalism. Each prediction is falsifiable, structural, and independent of model architecture. Part A specifies ten mechanical predictions testable under controlled conditions. Part B demonstrates the same mechanism running at human scale — across markets, institutions, peer review, and study design — as retrospective proof that no future experiments are required to establish the pattern. If any prediction in Part A fails under controlled conditions, the formalism is incorrect.

---

## The Structural Variables

Empirical predictions arise from the interaction of:

- **D** — constraint density
- **δ** — schema distance
- **|π|** — inference path length
- **σD** — dictionary variance
- **P_collapse** — collapse probability

These variables determine drift geometry and hallucination behavior.

---

## PART A — Mechanical Predictions

The following predictions describe the failure mode under controlled conditions. They are falsifiable by experiment. Each one is sufficient to decide the question independently.

---

### Prediction 1: Drift Magnitude Tracks δ/D

$$M \propto \delta/D$$

**Empirical claim:**
- Increasing constraint density reduces drift magnitude even when schema distance is large.
- Increasing schema distance increases drift magnitude when constraint density is low.
- Drift magnitude is predictable from the ratio δ/D.

**Test:**
- Hold model constant.
- Vary constraint density.
- Measure drift magnitude.

**Expected outcome:** Drift decreases monotonically as D increases.

---

### Prediction 2: Drift Direction Follows Dictionary Priors

$$\text{Direction} = \underset{\text{prior}}{\arg\max}(D_{\text{recv}})$$

**Empirical claim:**
- Drift direction is not random.
- Drift direction is stable across prompts with similar structural geometry.
- Drift direction is receiver-specific, not sender-specific.

**Test:**
- Provide underconstrained prompts to multiple receivers with different dictionaries.
- Compare drift direction.

**Expected outcome:** Drift direction differs across receivers but is stable within each receiver.

---

### Prediction 3: Drift Type Tracks Failure Location

$$\text{Type} = \text{location}(R_i \text{ failure})$$

**Empirical claim:**
- Binding failures produce linear drift.
- Property propagation failures produce radial drift.
- Multi-variable collisions produce convergent drift.
- Role assignment failures produce divergent drift.
- Collapse produces full reconstruction drift.

**Test:** Induce specific structural failures. Measure drift geometry.

**Expected outcome:** Drift type matches failure location exactly.

---

### Prediction 4: Drift Rate Tracks Inference Path Length

$$\text{Rate} \propto |\pi|$$

**Empirical claim:**
- Longer inference paths accumulate more drift.
- Shorter inference paths accumulate less drift.
- Constraint bundling reduces drift rate by shortening inference paths.

**Test:** Construct prompts with identical content but different inference path lengths. Measure drift accumulation.

**Expected outcome:** Drift rate increases monotonically with |π|.

---

### Prediction 5: Collapse Probability Tracks Structural Variables

$$P_{\text{collapse}} = g(D, |\pi|, \delta, \sigma_D)$$

**Empirical claim:**
- Low constraint density increases collapse probability.
- Long inference paths increase collapse probability.
- High schema distance increases collapse probability.
- High dictionary variance increases collapse probability.

**Test:** Vary structural variables independently. Measure collapse frequency.

**Expected outcome:** Collapse probability follows the predicted function.

---

### Prediction 6: Intervention Operators Reduce Drift Without Model Changes

$$G' = O(G)$$

**Empirical claim:**
- Explicit naming reduces drift magnitude.
- Exclusion operators change drift direction.
- Predication operators change drift type.
- Role operators reduce drift rate.
- Temporal/scope operators reduce dictionary variance.
- Overconstraint operators eliminate collapse.

**Test:** Apply intervention operators to underconstrained prompts. Measure drift geometry before and after.

**Expected outcome:** Drift geometry changes exactly as predicted.

---

### Prediction 7: Synthetic Referents Appear Only Under Overclosure

$$R_i' = \emptyset \Rightarrow v_i : r_{\text{synthetic}}$$

**Empirical claim:**
- Synthetic referents arise only when constraints eliminate all real referents.
- Synthetic referents satisfy all constraints but do not exist in the sender's dictionary.
- Synthetic referents disappear when constraint density is increased.

**Test:** Induce overclosure by overspecifying constraints. Measure referent creation.

**Expected outcome:** Synthetic referents appear only under overclosure conditions.

---

### Prediction 8: Drift Geometry Is Stable Across Model Scales

**Empirical claim:**
- Increasing model size does not change drift geometry.
- Increasing model size does not eliminate drift or collapse.
- Increasing model size reduces noise but does not change structural failure modes.

**Test:** Run identical prompts across multiple model scales. Measure drift geometry.

**Expected outcome:** Drift geometry remains constant across scales.

---

### Prediction 9: Drift Geometry Is Predictable Before Generation

$$G = \langle M, \text{Direction}, \text{Type}, \text{Rate}, P_{\text{collapse}} \rangle$$

**Empirical claim:**
- Drift geometry can be predicted from structural variables alone.
- Drift geometry does not require observing output.
- Drift geometry is computable from the surface form.

**Test:** Predict drift geometry from structural variables. Compare prediction to actual output.

**Expected outcome:** Predictions match observed drift geometry.

---

### Structural Summary of Part A

The mechanical predictions collectively assert:

- Drift is structural, not stochastic.
- Drift geometry is predictable, not emergent.
- Drift direction follows dictionary priors, not noise.
- Drift magnitude follows constraint density, not model scale.
- Collapse follows structural overload, not randomness.
- Intervention operators provide deterministic control over drift.

If any prediction fails under controlled conditions, the SDE formalism is incorrect.

---

## PART B — Human-Scale Retrospective Proofs

The mechanical predictions in Part A describe the failure mode in controlled conditions. Part B demonstrates that the same failure mode runs at human scale — in markets, in institutions, in peer review, and in study design. This is not an analogy. It is the same mechanism running on a different substrate. The experiments have already run. The markets already settled. The results are observable now.

---

### Constraint Density Is an Input-Side Variable: Retrospective Market Proof

**Empirical claim:**

If hallucination rate were randomly distributed relative to input structure, no market mechanism could emerge that consistently produces better outputs by modifying inputs alone. Four independent markets emerged and scaled before the academic literature named the mechanism.

**Market 1 — Prompt Engineering (2022+)**
A profession whose entire job description is: structure inputs so the decompression path is overconstrained. If outputs were model-quality dependent rather than input-structure dependent, this job could not exist. You cannot charge $150k/year for randomness reduction. The profession implies the signal is real, consistent, and input-side.

**Market 2 — Prompt Templates**
Templates work for users who have never thought about constraint structure. The template ships the constraint set on their behalf. If what transferred were model knowledge or domain expertise, templates would not work — you cannot template expertise. What transfers is structural: pre-bundled constraint density applied on behalf of the user.

**Market 3 — Form Design Infrastructure (Google Forms, Typeform, SurveyMonkey — 2000s+)**
Unstructured questions produce incomparable outputs. Form design tools exist to pre-ship the constraint set so every respondent produces parseable, comparable data. The mechanism is identical to prompt engineering. The substrate is human respondents, not LLMs. The market emerged decades before LLMs existed. This is not an AI problem. It is a compression/decompression problem that LLMs make visible at scale.

**Market 4 — Academic Survey Methodology (1970s+)**
An entire peer-reviewed discipline — Dillman, Fowler, Tourangeau — documenting how question wording changes response distributions. This is constraint density research. It predates computers. The field exists because output quality is an input-side variable when the receiver is a human.

**What this proves:**

The same mechanism has been running across four substrates — paper surveys, human respondents, digital forms, and LLMs — across 80 years and multiple independent billion-dollar markets. The SDE did not invent this. It named the mechanism the market already discovered empirically.

**Escape hatch and rebuttal:**

*Objection: "Prompt engineers just know model quirks — it's expertise about the model, not input structure."*

Rebuttal: Templates defeat this objection directly. Templates transfer the skill to users with zero model knowledge. If the mechanism were model expertise, templates would not work. The Google Forms parallel closes the escape hatch entirely: the mechanism predates LLMs and therefore cannot be an LLM-specific phenomenon.

**Falsification condition:** If prompt templates produce the same hallucination rate as unstructured prompts from naive users, the input-side variable claim is false. They do not. The market settled this empirically before the structural mechanism was named.

---

### Controlled Schema Injection: The Unified Model as Live Demonstration

**Empirical claim:**

If hallucinations are deterministic structural failures caused by input-side constraint gaps, then shipping a complete constraint schema inline should produce qualitatively different outputs — not slightly better outputs, but outputs that demonstrate behavior the unstructured query cannot produce at all.

**The live demonstration:**

The Unified Regulatory Model (Robinson, 2026) is a regulatory architecture describing cascading relationships between autonomic, cognitive, social, and institutional systems. The framework contains cross-domain predictions: change one variable in one layer, and the model predicts the downstream behavioral consequences across dependent layers.

Asking unstructured questions about these relationships produces generic responses. The model decompresses against its training dictionary and returns standard summaries. The cross-domain cascade is not visible because the constraint set that defines the relationships was never shipped.

**The boot file as schema replacement:**

The author built a boot file — a structured schema document that ships the framework's constraint set inline before any question is asked. The boot file defines:

- Layer relationships and dependency directions
- Contract boundaries and coupling mechanisms
- Valid inference paths between layers
- Failure modes and their upstream causes

With the boot file loaded, the same questions produce outputs that trace the regulatory cascade across layers, predict how behavioral outcomes change when upstream variables are modified, and maintain structural consistency across the inference chain. The model did not acquire new knowledge. The training weights did not change. The only variable that changed was constraint density of the input. The output behavior changed categorically.

This is not a prompt improvement. It is a schema replacement.

**The minimum invariant set:**

The Unified Model began as 30+ contracts mapping individual mechanisms across autonomic, cognitive, social, and institutional layers. The systematic search for which constraints carried the most structural load surfaced five physics primitives:

- Pressure
- Finite energy
- Oscillations
- Load
- Mechanical coupling

These are not summaries of the contracts. They are the axioms the contracts were independently deriving from. The final boot file ships the axiom set, not the derived layer. A model operating under hard physics constraints arrives at the same cross-layer predictions the contracts produced — because the physics forces them.

This is the constraint minimisation result: five invariants producing seven layers of consistent mechanistic output. A hallucinated model cannot do this. Hallucination produces locally coherent assertions. Axiom-driven derivation produces globally consistent consequences.

**The inference hop audit:**

Shipping the constraint set solves the input-side problem. It does not solve the validation problem: how does a reader verify the model walked the constraint chain rather than skipping scaffolding steps?

The field has chain-of-thought prompting. Chain-of-thought asks the model to show reasoning. It does not provide a mechanism to verify the chain is complete. A model can produce fluent chain-of-thought output while skipping three load-bearing inference hops, and the output will still read as correct.

The modification: force the model to output an explicit inference hop count and describe each hop before delivering the answer. If a model must list every inference step, missing steps become visible as gaps in the hop sequence. Logical fallacies become visible as jumps — hop 2 connecting directly to hop 7 with nothing in between.

This is not chain-of-thought prompting. It is chain validation — a structural audit of whether the constraint chain was fully traversed or whether the output was produced by skipping hops and asserting across the gaps. The difference is the difference between a student showing some work and a student showing all the work in the correct sequence.

Nothing equivalent exists in the current literature.

**The journal rejection as structural proof:**

The Unified Model was submitted to a scientific journal and rejected on the grounds that the cross-domain model appeared hallucinated — claims spanning autonomic, cognitive, social, and institutional systems without visible structural grounding.

The mechanism was real. The rejection was a constraint density failure, not a validity failure.

From the reviewers' position: they received a high-schema-distance input with low visible constraint density. Under the SDE model, their response was structurally correct. They could not distinguish a genuine cross-domain mechanism from a hallucinated one because the decompression dictionary was not shipped with the claims.

The response was not to argue the claims. It was to build the schema.

The author constructed an Obsidian vault with interlocking contract files, evidence objects, mechanism chains, and prediction ledgers. Each contract carries an explicit chain completeness rating — "scaffolding," "load-bearing," "confirmed-directional" — that surfaces the system's weakest links by design. The vault is a Bayesian evidence accumulator, not an assertion engine. A hallucinated model has no update structure. The vault's primary design property is forced revision.

The behavior changed because the schema changed — not because the claims changed. The author is simultaneously a theorist of the mechanism and a data point in the evidence set.

**The synthetic symbol extension:**

The schema does not need to be natural language. Any internally consistent symbol system shipped inline will produce consistent decompression:

- Define ZORF = "working memory load exceeds regulatory capacity threshold"
- Use ZORF in a question in the same context
- Output: Model decompresses ZORF consistently — not because it knows ZORF, but because the constraint was shipped inline

Two sessions with the schema definition produce identical decompression. Two sessions without it produce divergent or hallucinated referents. If hallucinations were random, novel symbol systems would not decompress consistently. They do. The consistency is enforced by constraint density, not semantic recognition.

**Falsification condition:** Load the Unified Model boot file into a fresh session. Ask a cross-layer regulatory question. Record the output. Start a new session without the boot file. Ask the identical question. Record the output. If both outputs demonstrate equivalent cross-layer predictive inference, the input-side constraint claim is false. They do not. The experiment is runnable today by any reader with access to any major LLM.

---

### The Silo Constraint: Why Narrow Windows Remove Necessary Constraints

**Empirical claim:**

Individuals whose inference is constrained to narrow domain silos will systematically fail to see constraint gaps that require cross-domain pattern matching to detect. This is not an intellect failure. It is a prediction window geometry failure: the window is not wide enough to hold the constraint that would reveal the gap.

The mechanism:

- Narrow prediction window → silo pattern matching only
- Silo pattern matching → constraints outside the silo are invisible
- Invisible constraints → removed from the inference chain without awareness
- Removed constraints → locally coherent output that misses structurally necessary variables
- Locally coherent output → reviewer accepts conclusion, misses the missing hop

**The primate study as specimen:**

A longitudinal study of 48 individual primates across four species found that individual performance is strongly predicted by rearing history, social group, sex, and research experience — and concluded that apes lack human-equivalent social cognitive architecture.

The data showed a regulatory load signal. The researchers called it a capacity ceiling.

The missing constraint — invisible from inside the comparative psychology silo — is physics: familiar environments reduce regulatory load and improve performance. Unfamiliar tasks increase load and degrade performance. This is not a capacity difference. It is the autonomic regulatory architecture responding to load.

The researchers found their own key counter-argument — research experience correlates with performance, which contradicts the capacity interpretation — and walked past it. The constraint that would have caught this was invisible because the silo did not include physics, autonomic architecture, or cross-species load mechanics. The gap did not appear as a gap. It appeared as a confirmed conclusion.

**The general prediction:**

Any study that:
- Uses tasks calibrated to one population's familiarity
- Measures performance without controlling for load
- Draws capacity conclusions from performance data

...has shipped a false constraint and will produce conclusions that satisfy the surface form of the data while diverging from the actual mechanism. This is Failure Mode 2 (False Resolution) running at study design level, not sentence level.

---

## The Universal Mechanism

Every system that processes information under resource constraints exhibits the same failure modes. The substrate does not matter. The physics is the same.

Human cognition, LLM inference, institutional decision-making, economic systems — they all fail identically because they face identical constraints:

- Finite energy
- Pressure gradients
- Oscillating load cycles
- Mechanical coupling between layers
- Resource limits that force compression

When any system hits resource limits it does the same thing: it narrows the inference window, skips scaffolding steps, and produces locally coherent output that misses the structurally necessary constraints it can no longer afford to hold.

Survey methodology, prompt engineering, organisational design, economic policy, clinical diagnostic criteria — all are constraint density interventions. None were named as such.

This is not an intellect problem. It is a physics problem. The mechanism does not care what substrate it runs on. The SDE named it. The fix is the same everywhere: increase constraint density at the input until the inference path is fully traversable without fallback to the prior.

This is the science that only needs to be found once.
