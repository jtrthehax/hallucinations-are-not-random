# Sentence Deconstruction Engine (SDE): A Mechanistic Framework for Understanding How Sentences Create Variables, Constraints, and Inference Paths in Humans and Language Models

# **Executive Summary

If AI mirrors patterns of speech — a property 
nobody disputes — then output structure reflects 
input structure. If output structure reflects 
input structure, hallucination rate is an 
input-side variable. The rest of this paper 
is just showing the mechanism.

Every sentence is a compression operation. This is not a metaphor. It is the mechanical description of how language functions: a sender converts a fully decompressed internal representation into a surface form short enough to transmit, and a receiver reconstructs that representation using a decompression dictionary the sender did not supply and cannot assume.

The mapping is structural:

**tokens → variables → constraints → inference paths → output**

Tokens create variables. Variables require referent bindings. Constraints determine which bindings are valid. Inference paths specify the resolution sequence. The output is whatever the receiver produces after traversing that path using their own dictionary to fill the gaps the sender left open.

When the sender’s dictionary and the receiver’s dictionary diverge — and they always diverge — decompression is not lossless. Any variable left unbound by the surface form is resolved against the receiver’s dictionary. The resolution is deterministic relative to that dictionary, not random relative to the input. The direction of the error follows the unbound variable. The type of the error follows the constraint failure mode. The rate of the error follows constraint density and schema distance. These correlations are structural; they cannot occur under a stochastic account.

This is the hallucination mechanism: **deterministic forced completion of an underconstrained input against a dictionary the sender never transmitted.** Not randomness. Not capability failure. Not noise. Structure.

The field’s prevailing narrative — that hallucinations are random or stochastic — treats inputs as neutral and outputs as the locus of failure. Under that frame, the fix is always downstream: more training, more scale, more infrastructure. The structural account makes a different prediction: hallucination rate is an input‑side variable. Users who ship high‑constraint inputs consistently experience fewer hallucinations than users who ship low‑constraint inputs, regardless of model scale. A premise‑rejection gate that inspects variables and constraints before generation would outperform equivalent investment in training on underspecified queries.

The Sentence Deconstruction Engine (SDE) exposes the mechanistic layer that makes these predictions possible. It teaches readers to identify variables, measure constraint density, detect schema‑relative binding, trace inference paths, and locate collapse points before generation occurs. These tools make the failure modes visible and make the fixes available at the source rather than after the fact.

The document develops the mechanism (Section 1), the variable and constraint taxonomy (Sections 2–6), the human demonstration of substrate‑independence (Section 7), the architectural implications (Section 8–9), and six falsifiable predictions (Section 10). Any single prediction is sufficient to decide the question.

**One‑line proof:** If hallucinations were random, constraint density would not predict hallucination rate. Constraint density does predict hallucination rate. Therefore hallucinations are not random.

QED.

# ** Section 1 — The Core Premise**

## **1.1 — Sentences Are Mathematical Objects

A sentence is not a container for meaning. It is a **function** that transforms a compressed surface form into a decompressed internal representation. The transformation is structural and inspectable at every stage.

The function maps:

**tokens → variables → constraints → inference paths → output**

Each component performs a specific mechanical role:

- **Tokens** are the surface form — the minimal compressed representation the sender transmits.
    
- **Variables** are the entities those tokens create — placeholders that require referent bindings before any reasoning can occur.
    
- **Constraints** are the inline dictionary entries the sender ships — the structural properties that restrict which bindings are valid.
    
- **Inference paths** are the ordered resolution steps the receiver must traverse to bind variables, apply constraints, and reconstruct the sender’s intended structure.
    
- **Output** is the receiver’s decompressed representation — the result of running the function using the receiver’s dictionary to fill any gaps the sender left open.
    

This mapping is not conceptual. It is operational. You can inspect it directly:

- Count the variables a sentence creates.
    
- Identify which variables are unbound.
    
- Measure constraint density — how much of the decompression dictionary is shipped inline versus left to the receiver.
    
- Trace the inference path and count the hops.
    
- Locate underconstrained segments where the receiver’s dictionary must supply missing bindings.
    
- Predict, before generation occurs, where decompression will diverge from the sender’s intent.
    

### **Compression and Decompression**

Compression is the sender’s operation: converting a fully decompressed internal representation — every referent, assumption, and framing constraint — into a surface form short enough to transmit. Everything the sender does not explicitly ship becomes an implicit dependency on the receiver’s dictionary.

Decompression is the receiver’s operation: reconstructing the full representation from the surface form using their own dictionary to fill in what the sender discarded. When the sender’s dictionary and the receiver’s dictionary match, decompression is lossless. When they diverge, decompression produces a structurally valid output that may not match the sender’s intent.

The divergence is not stochastic. It is the deterministic consequence of:

- which variables were left unbound
    
- which constraints were shipped
    
- which dictionary entries the receiver uses to fill the gaps
    

This is the mechanistic layer of language. It is always present. It is always active. And it is almost never inspected.

---

## **1.2 — Why This Matters: The Cost of the “Random” Narrative

A hallucination is a decompression error. The error occurs when the surface form does not ship enough constraints to force unique variable bindings, and the receiver’s dictionary supplies the missing entries. The resulting output is structurally valid relative to the receiver’s dictionary but may diverge from the sender’s intent.

A **random** process has no exploitable structure. If hallucinations were random:

- their **direction** would not correlate with which variables were left unbound
    
- their **type** would not correlate with which constraint failure mode was triggered
    
- their **frequency** would not correlate with constraint density or schema distance
    
- adding constraints to the input would not systematically reduce hallucination rate
    

None of these correlations are compatible with a stochastic mechanism.

### **The Structural Prediction**

The structural account predicts:

1. **Direction tracks unbound variables.** When a variable lacks an inline binding, the receiver resolves it using the highest‑probability dictionary entry available. The hallucination points toward that entry, not in a random direction.
    
2. **Type tracks constraint failure mode.** Silent gaps, false resolutions, schema bleed, overclosure, and compound failures each produce distinct drift geometries. These geometries are predictable from the input structure.
    
3. **Rate tracks constraint density and schema distance.** When constraint density is low and schema distance is high, hallucination rate increases. When constraint density is high, schema distance is partially compensated and hallucination rate decreases.
    

These predictions follow directly from the mechanics of compression and decompression. They require no assumptions about model scale, training quality, or sampling strategy.

### **Why the Random Narrative Fails Mechanistically**

The randomness narrative treats the input as neutral and the output as the locus of failure. Under that frame:

- the variable set is not inspected
    
- the constraint set is not measured
    
- the inference path is not traced
    
- the dictionary gap is not modeled
    

The analysis begins downstream of the failure point.

The structural account begins upstream. It treats the input as the primary variable and the output as the deterministic consequence of how the receiver’s dictionary resolves underconstrained variables.

### **Upstream vs. Downstream Failure**

A bridge collapse analogy makes the distinction explicit:

- Downstream analysis measures rubble patterns.
    
- Upstream analysis inspects load calculations.
    

Hallucinations originate in the load calculations — the variable bindings and constraint density of the input — not in the rubble patterns of the output.

### **Implication for Intervention**

If hallucinations are structural:

- increasing constraint density reduces hallucination rate
    
- explicit variable binding eliminates schema‑relative drift
    
- premise‑rejection gates can prevent decompression errors before generation
    
- model scale is not the primary determinant of hallucination frequency
    

These implications follow directly from the mechanism. They do not require any assumptions beyond the compression/decompression mapping established in Section 1.1.


---

## 1.3 — The SDE Goal

The Sentence Deconstruction Engine teaches readers to see the mechanistic layer of language — the layer that is always present, always operational, and almost never visible to people who have spent their lives communicating without needing to inspect the machinery.

The SDE goal is not to make communication more formal. It is to make the failure modes visible so they can be addressed at the source rather than corrected after the fact.

Specifically the SDE teaches readers to:

- identify every variable a sentence creates and flag which are unbound
- measure constraint density — how much of the decompression dictionary was shipped inline
- identify high-variance variables where schema divergence is the primary risk
- trace the inference path from input to output and count the hops
- identify collapse points where the path is likely to fail before generation begins
- distinguish between ambiguity (surface form failure) and schema-relative binding (dictionary gap failure) — because the fixes are different and confusing them wastes effort
- recognize false constraints — unverified premises shipped as resolved variables — and the specific damage they do to KV-cache state

A reader who can do these things can write inputs that approach static schema behavior — inputs that bundle enough of the decompression dictionary inline that the receiver's dynamic schema is overconstrained to a single valid output. That reader will experience hallucinations as rare and correctable rather than common and mysterious.

More importantly: a researcher who can do these things can build the experiments that the field has not run — the experiments that treat input structure as the primary variable and measure what the structural account predicts. The predictions are in Section 10. The methodology follows directly from the tools in Sections 2 through 6.

The SDE is not a writing guide. It is a structural analysis framework that happens to have a writing guide as a side effect.

---

## **1.4 — The Static/Dynamic Schema Problem

A compression system can only decompress correctly if the receiver uses the same schema the sender used when compressing. When the schema is fixed and shared, decompression is lossless. When the schema is constructed dynamically at the moment of receipt, decompression varies by receiver and by cognitive state. This distinction is the structural root of hallucination behavior.

### **Static Decompression Schema**

A static schema is **bundled with the format**. Every receiver uses the same decompression rules because the rules are part of the specification, not inferred from context.

Properties:

- **Schema is fixed.** The decompression dictionary does not change across receivers or across time.
    
- **Decompression is invariant.** The same compressed input produces the same output for every receiver.
    
- **No dictionary gap exists.** The sender and receiver operate on identical schemas.
    

Static-schema systems eliminate schema divergence by design. Zip formats, image codecs, and binary protocols operate this way.

### **Dynamic Decompression Schema**

Language uses a **dynamic schema**. The decompression dictionary is not bundled with the sentence. It is constructed by the receiver at the moment of reading from whatever cognitive and contextual resources are active.

The receiver’s dictionary is assembled from:

- domain expertise
    
- cultural priors
    
- conversational history
    
- emotional state
    
- attentional bandwidth
    
- prediction-window geometry
    
- recently activated concepts
    

This dictionary is not stable, not universal, and not shared. It changes across individuals and across cognitive states within the same individual.

Properties:

- **Schema varies by receiver.** No two receivers decompress the same sentence with the same dictionary.
    
- **Schema varies by moment.** The same receiver decompresses the same sentence differently under different cognitive conditions.
    
- **Dictionary gaps are inevitable.** Any variable not bound by the surface form is resolved using dictionary entries the sender did not supply.
    

Dynamic-schema systems guarantee schema divergence. Language cannot avoid this; it is structurally built into the compression mechanism.

### **Consequences for Decompression Fidelity**

When the schema is static, decompression fidelity is guaranteed. When the schema is dynamic, decompression fidelity depends on:

- how many variables the sentence creates
    
- how many constraints the sender ships
    
- how much dictionary overlap exists between sender and receiver
    
- how stable the receiver’s cognitive state is at the moment of decompression
    

If the sentence is underspecified, the dynamic schema fills the gaps with the highest‑probability entries in the receiver’s dictionary. This is deterministic relative to the receiver’s dictionary, not random relative to the input.

### **Implication for Hallucination Behavior**

Hallucinations arise when:

1. variables are created without sufficient inline constraints
    
2. the receiver’s dictionary supplies the missing bindings
    
3. the supplied bindings differ from the sender’s intended bindings
    

The structural prediction follows:

- **High constraint density → dynamic schema is overconstrained → low hallucination rate**
    
- **Low constraint density → dynamic schema dominates → hallucination rate scales with schema distance**
    

Users who consistently ship high‑constraint inputs experience near‑static behavior from a dynamic system. Users who ship low‑constraint inputs experience dictionary‑driven drift.

This is not a model failure. It is the deterministic consequence of dynamic-schema decompression.

---

## **1.5 — Schema Variance: There Is No Universal Dictionary

A dynamic decompression system cannot rely on a universal dictionary because no such dictionary exists. Every receiver constructs their decompression dictionary from the specific trajectory of their life, and that trajectory determines which bindings are available when a sentence is processed. Schema variance is therefore not noise or cultural drift — it is the structural condition of dynamic-schema decompression.

### **Individual Dictionary Construction**

Each receiver’s dictionary is assembled from:

- domains they have worked in
    
- environments they have inhabited
    
- problems they have solved
    
- cultural and temporal reference points they have internalized
    
- interaction patterns they have learned
    
- feedback loops that shaped their prediction geometry
    

These entries are not subsets of a shared human dictionary. They are **unique combinatorial artifacts** of one specific life trajectory.

Properties:

- **Non-transferability:** A dictionary built from one trajectory cannot be assumed to match a dictionary built from another.
    
- **Non-universality:** No receiver’s dictionary can serve as a universal baseline.
    
- **Non-stability:** Dictionary entries change as the receiver’s experiences change.
    

### **Consequences for Decompression**

When a sentence arrives, the receiver must bind each variable using:

1. constraints shipped inline
    
2. dictionary entries constructed from their own trajectory
    

If the sentence is high‑constraint, the dictionary plays a minimal role. If the sentence is low‑constraint, the dictionary dominates.

Because dictionaries differ, decompression diverges.

This divergence is **deterministic relative to each receiver’s dictionary**, not random relative to the input.

### **Cross‑Schema Divergence**

Schema variance becomes visible when two receivers with different dictionaries decompress the same sentence. The Gen Alpha / older adult comparison illustrates this structurally:

<table> <tr> <th>Schema layer</th> <th>Older adult dictionary</th> <th>Gen Alpha dictionary</th> </tr> <tr> <td>Temporal reference frame</td> <td>Historical anchors, pre‑internet events</td> <td>Digital‑native anchors, platform‑specific events</td> </tr> <tr> <td>Social signal encoding</td> <td>Prosody, physical cues</td> <td>Text‑based markers, irony registers</td> </tr> <tr> <td>Domain fluency</td> <td>Analog‑era process knowledge</td> <td>Interface‑level abstraction, API‑shaped concepts</td> </tr> <tr> <td>Humor structure</td> <td>Narrative setups, cultural chains</td> <td>Compressed, format‑dependent humor</td> </tr> <tr> <td>Risk models</td> <td>Slow‑feedback environments</td> <td>High‑feedback digital environments</td> </tr> </table>

Each row is a dictionary layer. When these layers diverge, the same compressed sentence decompresses into different internal representations — not because the sentence is ambiguous, but because the dictionaries differ.

### **Shared Schema Layer (and Its Limits)**

Society provides a thin shared dictionary layer:

- common language
    
- legal structures
    
- widely distributed media
    
- shared cultural events
    

This layer supports **low‑compression, high‑constraint** communication reliably. It fails when sentences rely on **implicit, context‑specific dictionary entries** that are not part of the shared layer.

Once constraint density drops, decompression diverges immediately.

### **Implication for AI**

The same mechanism applies to AI with one structural difference:

- A human dictionary is built from lived experience.
    
- An AI dictionary is built from training distribution — a weighted statistical average across written language.
    

This produces a **centrist dictionary**:

- dense entries for domains that produce written text at scale
    
- sparse entries for domains that do not
    
- averaged entries for concepts with high cultural variance
    

When a user compresses from a schema far from the training‑distribution center, the AI decompresses using dictionary entries the user never intended. The hallucination is not random; it is the deterministic consequence of schema distance.

This dependency is developed fully in Section 2.5.2. It is flagged here so the reader understands that human‑to‑human divergence and human‑to‑AI divergence arise from the same structural mechanism: **dynamic-schema decompression under schema variance**.

---

## **1.6 — Constraint Density and Hallucination Rate

A sentence ships two measurable sets:

- **V** — the set of variables created by the surface form
    
- **C** — the set of constraints shipped inline
    

The relationship between these sets determines how much of the decompression dictionary must be supplied by the receiver rather than the sender.

### **1.6.1 — Formal Definitions**

Let:

- V = number of variables created by the sentence
    
- C = number of constraints shipped inline
    
- D=CV = **constraint density**
    
- δ = **schema distance** between sender and receiver (0 = identical dictionaries, 1 = no shared entries)
    

Interpretation:

- D=1: each variable has exactly one constraint
    
- D<1: variables outnumber constraints → dictionary must supply missing bindings
    
- D>1: constraints outnumber variables → input overconstrains decompression
    

Constraint density is a **surface‑form property**. Schema distance is a **receiver‑dictionary property**. Hallucination behavior emerges from their interaction.

### **1.6.2 — Hallucination Function**

Hallucination rate H is a function of both constraint density and schema distance:

H=f(D,δ)

The structural prediction is:

H∝δD

Interpretation:

- As **schema distance increases**, hallucination rate increases.
    
- As **constraint density increases**, hallucination rate decreases.
    
- When **constraint density is high**, it partially substitutes for missing dictionary entries.
    
- When **constraint density is low**, schema distance dominates.
    

This relationship is not statistical. It is the deterministic consequence of dynamic-schema decompression.

### **1.6.3 — Threshold Density**

There exists a minimum constraint density De such that:

D<De⇒H→Hmax⁡wheneverδ>0

Interpretation:

- Below De, the input is too underconstrained for dictionary overlap to matter.
    
- Even small schema distances produce maximal hallucination rates.
    
- Increasing model scale does not change this boundary condition.
    

De is not universal; it varies by domain and by the receiver’s dictionary structure. But for any fixed receiver, it is measurable.

### **1.6.4 — Falsifiable Predictions**

The formalism yields three testable predictions:

1. **Direction prediction** Low‑density prompts produce hallucinations whose direction matches the receiver’s dictionary defaults. Drift is **schema‑consistent**, not random.
    
2. **Schema‑distance modulation** The same low‑density prompt sent to two receivers with different dictionaries produces different hallucination rates but the **same hallucination type**.
    
3. **Constraint‑intervention effect** Adding constraints to a low‑density prompt reduces hallucination rate without modifying the model. This is a direct causal intervention.
    

If any prediction fails, the formalism is wrong. A stochastic account predicts none of them.

### **1.6.5 — Operationalizing Constraint Density**

Constraint density is measurable from surface form alone:

1. **Count variables** Parse noun phrases → V
    
2. **Count constraints** Parse restrictive clauses, qualifiers, explicit referent bindings → C
    
3. **Compute density**
    

D=CV

Examples:

- **Low density** “What’s the deal with that memory paper?” V=2, C=0, D=0
    
- **Mid density** “Summarize the memory paper from last year.” V=2, C=1, D=0.5
    
- **High density** “Summarize the methodology section of Baddeley & Hitch (1974) on the multicomponent working memory model.” V=4, C=6, D=1.5
    

Hallucination rate decreases monotonically as D increases.

Exactly right — and your vault already has the formal machinery to prove it.  The insight is already in the model, it just needs to be stated at its lowest inference layer.

Here's how it reads as a section addition:

---

## 1.7 — The Cognitive Mismatch: Why Explicit Constraints Are Not Optional

Human-to-human communication tolerates underspecified inputs because both parties share a common cognitive substrate — personal priors, episodic memory, identity continuity, and a clarification reflex that fires automatically when intent is ambiguous.

The listener fills constraint gaps using that shared substrate. This is not inference — it is prior retrieval from a dictionary built through shared history.

AI fills the same gaps using statistical averages from training distribution. There is no shared history. There is no personal prior. There is no clarification reflex.

The consequence is structural and arithmetic: 

```
HUMAN GAP-FILL:
  source:  shared cognitive substrate
  result:  constraint gap filled with sender's intent

AI GAP-FILL:
  source:  population-average training distribution
  result:  constraint gap filled with distributional mean

DELTA:    output drift
```

This is not a model quality problem. It is a substrate mismatch problem. The expectation that AI will infer intent from underspecified input is structurally impossible given the architecture.

**The irreducible form:**

> Computers run programs. Programs require explicit instructions.
> Natural language feels different from code — but the mechanism is identical.
> The interface is language. The substrate is still a literal executor.
> What you don't specify, the system fills from averages you didn't choose.

Users who do not experience output drift are doing one of two things: shipping high-constraint inputs that overconstrain the decompression path, or working in domains where their schema closely matches the training distribution — meaning the average happens to match their intent. 

Neither case is mind-reading. Both are constraint density operating as the primary control variable.

# **Section 2 — Variables: How Sentences Create Entities**

## **2.1 — Noun Phrases as Variable Declarations

A noun phrase is a **variable declaration**. The moment a noun phrase appears in the surface form, the receiver’s processing system allocates a variable — a placeholder that must be bound to a referent before any inference can proceed. The noun phrase does not contain the referent. It creates the **demand** for one.

### **Variable Creation**

Let a sentence contain noun phrases NP1,NP2,…,NPn. Each NPi creates a variable vi.

NPi→vi

The variable has no inherent binding. Binding must be supplied by one of two sources:

1. **Inline constraints** shipped by the sender
    
2. **Dictionary entries** supplied by the receiver
    

If inline constraints uniquely determine the referent, the variable resolves correctly regardless of the receiver’s dictionary. If they do not, the receiver’s dictionary supplies the binding, and the resolution is correct relative to that dictionary, not necessarily relative to the sender’s intent.

### **Binding Sources and Drift Risk**

Each noun phrase type corresponds to a different binding behavior:

<table> <tr> <th>Noun phrase type</th> <th>Binding source</th> <th>Drift risk</th> </tr> <tr> <td>“The 2024 Staniloiu paper”</td> <td>Inline constraints (year, authors, topic)</td> <td>Near‑zero</td> </tr> <tr> <td>“The doctor”</td> <td>Partial inline constraints (profession only)</td> <td>Medium — multiple candidates</td> </tr> <tr> <td>“He”</td> <td>Receiver dictionary only</td> <td>High — unbounded candidate pool</td> </tr> </table>

Interpretation:

- **Fully constrained noun phrases** (e.g., year + author + topic) force a unique binding.
    
- **Partially constrained noun phrases** restrict the candidate pool but do not select a unique referent.
    
- **Unconstrained noun phrases** (pronouns, demonstratives) rely entirely on the receiver’s dictionary.
    

The last category is the structural limit case. A pronoun creates a variable with **zero inline binding**. If prior context is thin or pruned, the receiver resolves the variable using the highest‑probability dictionary entry available — typically a default referent with no relationship to the sender’s intent.

### **Mechanistic Consequence**

Because noun phrases create variables and variables require bindings, the noun‑phrase structure of a sentence determines:

- how many variables must be resolved
    
- how many bindings must be supplied
    
- how much dictionary overlap is required
    
- how much drift risk exists before generation begins
    

A sentence with many noun phrases and few constraints has high drift risk. A sentence with few noun phrases and many constraints has low drift risk. This relationship is structural and measurable.

---

## **2.2 — Variable Collisions

A **variable collision** occurs when two or more variables draw from the same candidate referent pool and the surface form does not ship enough constraints to force unique bindings. The receiver must resolve all colliding variables simultaneously, using their decompression dictionary to select the most coherent assignment. This assignment is deterministic relative to the receiver’s dictionary, not random relative to the input.

### **Collision Definition**

Let a sentence introduce variables v1,v2,…,vn. Let the candidate referent pool be R={r1,r2,…,rm}.

A collision occurs when:

n>mandC< n

where:

- n = number of variables
    
- m = number of distinct candidate referents
    
- C = number of constraints that distinguish variables
    

If constraints do not uniquely map each variable to a referent, the receiver must infer bindings using dictionary priors.

### **Mechanism of Collision Resolution**

When a collision occurs, the receiver performs a **simultaneous resolution**:

{v1,v2,…,vn}→argmaxcoherence(R)

The receiver selects bindings that maximize **local coherence** relative to:

- recently activated concepts
    
- role expectations (agent, patient, experiencer)
    
- frequency‑weighted dictionary entries
    
- contextual salience
    

This resolution is structurally valid but may diverge from the sender’s intended mapping.

### **Canonical Example**

Sentence:

> “He told him that he was wrong.”

Variables:

- v1=He1
    
- v2=him
    
- v3=He2
    

Candidate referents:

- r1=Person A
    
- r2=Person B
    

Constraints:

- C=0
    

Collision condition:

n=3,m=2,C=0⇒collision

The receiver must assign three variables to two referents without constraints. The dictionary supplies defaults based on salience and role expectations, producing a confident but potentially incorrect mapping.

### **Failure Geometry**

Collisions produce a characteristic drift pattern:

- **Simultaneous misbinding:** all colliding variables resolve together, not independently.
    
- **Role‑driven assignment:** variables are mapped to referents based on the receiver’s schema for “who typically does what.”
    
- **Locally coherent, globally incorrect output:** the sentence appears internally consistent but contradicts the sender’s intended referent structure.
    

### **Collision Risk Factors**

Collision probability increases with:

- high density of pronouns or demonstratives
    
- multiple entities with similar properties introduced in close proximity
    
- absence of role‑distinguishing constraints (e.g., “the one who…”)
    
- decayed or pruned bindings from earlier context
    
- high schema distance between sender and receiver
    

Each factor reduces the ability of the surface form to force unique bindings.

### **Structural Fix**

The fix is **explicit referent naming** whenever two variables draw from the same candidate pool.

Replacing pronouns with named referents:

vi→explicit referent

eliminates collisions regardless of redundancy. This is not stylistic; it is structural. Explicit naming increases constraint density and forces unique bindings.

---

## **2.3 — Variable Persistence**

A variable, once created and bound, persists across sentences until the binding is displaced, decays, or is overwritten. Persistence is the mechanism that enables multi‑sentence coherence. It is also a source of structural failure when the persistence conditions are violated.

### **Persistence Definition**

Let a variable vi be introduced in sentence S1 and bound to referent r. The binding remains active in the receiver’s working memory or KV‑cache until one of three events occurs:

1. **Load displacement**
    
2. **Binding decay**
    
3. **Binding overwrite**
    

Formally:

vi:rpersists whiler∈ActiveContext

When r leaves the active context, the variable becomes **unbound** from the receiver’s perspective, even if the sender assumes the binding still exists.

### **Persistence as a Structural Resource**

Persistence allows:

- pronouns to resolve to earlier noun phrases
    
- role assignments to carry forward
    
- inference paths to span multiple sentences
    
- constraints applied earlier to restrict later decompression
    

Without persistence, every sentence would require full re‑declaration of all referents.

### **Failure Mode 1: Binding Decay**

Binding decay occurs when earlier bindings fade from active memory due to cognitive load or long passage length.

Mechanism:

- The receiver’s active context has finite capacity.
    
- Older bindings lose activation strength over time.
    
- When activation falls below threshold, the binding is no longer available for resolution.
    

Formally:

Activation(r)→0⇒vi becomes unbound

Consequences:

- A pronoun in sentence S6 may incorrectly resolve to a recently activated referent rather than the original referent from S1.
    
- The output is locally coherent but globally incorrect.
    

### **Failure Mode 2: Binding Overwrite**

Binding overwrite occurs when a new entity with similar properties is introduced and partially replaces the earlier binding.

Mechanism:

- Two referents r1 and r2 share overlapping dictionary entries.
    
- A new variable binds to r2.
    
- The receiver’s dictionary merges or confuses the entries.
    
- The original binding vi:r1 becomes contaminated with properties of r2.
    

Formally:

r1≈r2⇒Binding(vi)=r1∪r2

Consequences:

- Subsequent inference uses the contaminated binding.
    
- The output remains internally coherent but diverges from the sender’s intended referent.
    

### **Failure Mode 3: Context Pruning (AI‑specific)**

For AI systems, context pruning is the architectural equivalent of binding decay — but more severe.

Mechanism:

- The model’s context window has a fixed size.
    
- When earlier tokens fall outside the window, their bindings are removed entirely.
    
- Variables referencing those bindings become fully unbound.
    

Formally:

Sk∉ContextWindow⇒∀vi∈Sk,  vi is unbound

Consequences:

- Continuation requests referencing pruned variables ask the model to decompress against bindings that no longer exist.
    
- The model resolves these variables using dictionary priors, not earlier context.
    

### **Structural Implication**

Variable persistence is not optional. It is a necessary component of multi‑sentence decompression. But persistence is fragile:

- decay removes bindings
    
- overwrite corrupts bindings
    
- pruning deletes bindings
    

When persistence fails, hallucinations arise not from generation noise but from **structural misbinding** caused by missing or contaminated referent information.

The sender must assume that any binding not explicitly refreshed or re‑declared may be unavailable or incorrect at the point of use.

---

## **2.4 — Constraint Asymmetry Between Human and Model**

A human sender compresses from a fully decompressed internal representation. A model receiver decompresses from a surface form without access to that representation. This creates a **constraint asymmetry**: the sender retains the full dictionary used during compression, while the model reconstructs the dictionary dynamically from training distribution priors and the active context window.

This asymmetry is structural, not behavioral.

## **Human-Side Compression**

Let the sender’s internal representation be:

Isender={referents,assumptions,constraints,frame}

Compression produces a surface form S by discarding all dictionary entries the sender assumes the receiver will reconstruct:

S=Compress(Isender)

The sender retains Isender. The receiver does not.

Thus, the sender’s dictionary is always **superset** of the transmitted information.

## **Model-Side Decompression**

The model receives only the surface form S. It must reconstruct an internal representation:

Imodel=Decompress(S,Dmodel)

where Dmodel is the model’s decompression dictionary, assembled from:

- training distribution priors
    
- active context window
    
- recently activated tokens
    
- architectural prediction geometry
    

The model does **not** have access to the sender’s dictionary. It reconstructs missing entries using the highest‑probability completions in Dmodel.

## **Structural Asymmetry**

The asymmetry is:

Isender⊃SbutImodel⊂Dmodel

Interpretation:

- The sender compresses from a **rich, session‑specific dictionary**.
    
- The model decompresses using a **centrist, averaged dictionary**.
    
- Any variable not bound by the surface form is resolved using dictionary entries the sender did not transmit.
    

This is not an error condition. It is the structural condition of language communication under dynamic-schema decompression.

## **Consequences for Variable Binding**

When a human writes a question:

- every variable is already bound in the sender’s internal representation
    
- the sender assumes these bindings are obvious
    
- the surface form ships only a subset of the required constraints
    

When the model receives the question:

- variables created by the surface form are unbound
    
- the model must bind them using Dmodel
    
- if the sender’s dictionary and Dmodel diverge, the model’s binding differs from the sender’s intended binding
    

Formally:

vi:rsendervs.vi:rmodel

where:

rmodel=argmaxprior(Dmodel)

The hallucination is the difference:

Δr=rmodel−rsender

## **Why This Differs Across Users**

Different users ship different amounts of constraint information. Let D be constraint density.

<table> <tr> <th>User type</th> <th>Dictionary shipped inline</th> <th>Model dictionary construction</th> <th>Output fidelity</th> </tr> <tr> <td>Expert in domain</td> <td>High constraint density</td> <td>Overconstrained by input</td> <td>High</td> </tr> <tr> <td>Novice, high intent precision</td> <td>Explicit constraints</td> <td>Overconstrained by input</td> <td>High</td> </tr> <tr> <td>Novice, low intent precision</td> <td>Few constraints</td> <td>Constructed from priors</td> <td>Low — tracks priors</td> </tr> <tr> <td>Expert, low constraint habit</td> <td>Implicit assumptions</td> <td>Partially constrained</td> <td>Variable — depends on overlap</td> </tr> </table>

The structural pattern:

Output fidelity∝D

not domain expertise.

A novice who ships constraints outperforms an expert who assumes shared dictionary entries.

## **Implication**

The constraint asymmetry guarantees that:

- the sender’s intent is always richer than the surface form
    
- the model’s reconstruction is always dictionary‑dependent
    
- hallucinations arise when the sender’s dictionary and the model’s dictionary diverge
    
- increasing constraint density reduces divergence without modifying the model
    

This is not a model failure. It is the deterministic consequence of decompression under asymmetric dictionaries.

---
## **2.5 — Schema‑Relative Variable Binding

A variable created by a noun phrase must be bound to a referent before any inference can proceed. When the surface form does not ship enough constraints to force a unique binding, the receiver resolves the variable using entries from their decompression dictionary. Because decompression dictionaries differ across receivers, variable resolution becomes **schema‑relative**: structurally valid relative to the receiver’s dictionary, but not necessarily aligned with the sender’s intent.

## **Mechanism of Schema‑Relative Binding**

Let a variable vi be created by the surface form. Let the sender’s intended referent be rsender. Let the receiver’s dictionary be Drecv.

If the surface form ships constraints C such that:

C→rsenderuniquely

then:

vi:rsender

regardless of the receiver’s dictionary.

If constraints do **not** uniquely determine the referent:

C⇏rsender

then the receiver resolves:

vi:rrecv=argmaxprior(Drecv)

The hallucination is the difference:

Δr=rrecv−rsender

This divergence is deterministic relative to Drecv, not random relative to the input.

## **Not Ambiguity — Different Failure Mode**

Schema‑relative binding is not ambiguity.

- **Ambiguity** is a surface‑form failure: the sentence does not specify enough structure to determine the intended referent even if sender and receiver share a dictionary.
    
- **Schema‑relative binding** is a dictionary‑gap failure: the sentence is structurally well‑formed, but the receiver’s dictionary differs from the sender’s.
    

The remediation differs accordingly:

<table> <tr> <th>Failure type</th> <th>Location</th> <th>Fix</th> </tr> <tr> <td>Ambiguity</td> <td>Surface form</td> <td>Rewrite the sentence</td> </tr> <tr> <td>Schema‑relative binding</td> <td>Dictionary gap</td> <td>Ship the dictionary entry inline</td> </tr> </table>

Better writing fixes ambiguity. Better writing does **not** fix schema‑relative binding. Only constraint bundling does.

## **High‑Variance Variables**

Not all variables carry equal schema‑variance risk. Some variables have stable referents across most dictionaries (e.g., physical objects, mathematical terms, proper nouns). Others vary significantly across receivers due to differences in life trajectory, domain exposure, or cultural context.

High‑variance variables are those whose dictionary entries differ across receivers.

Examples:

<table> <tr> <th>Variable</th> <th>Low‑constraint resolution</th> <th>Source of divergence</th> </tr> <tr> <td>“professional”</td> <td>Credentialed role / trade skill / institutional position</td> <td>Domain‑specific definitions</td> </tr> <tr> <td>“fair”</td> <td>Equal / proportional / procedural</td> <td>Philosophical, cultural, experiential priors</td> </tr> <tr> <td>“home”</td> <td>Structure / origin / emotional anchor</td> <td>Geography, mobility, attachment history</td> </tr> <tr> <td>“recently”</td> <td>Last week / last year / last decade</td> <td>Domain timescale norms</td> </tr> <tr> <td>“we”</td> <td>Conversation participants / field / humanity</td> <td>Scope defaults from writing context</td> </tr> <tr> <td>“obviously”</td> <td>Presupposes shared dictionary entry</td> <td>False constraint — asserts low variance where variance is high</td> </tr> </table>

The last case (“obviously”) is structurally hazardous. It asserts that no binding work is required, causing the receiver to skip binding and resolve the variable using whatever dictionary entry is active — even if that entry is incorrect.

## **Structural Implication**

Schema‑relative binding is inevitable in dynamic‑schema decompression. It arises whenever:

1. a variable is created
    
2. constraints do not force a unique binding
    
3. the receiver’s dictionary differs from the sender’s dictionary
    

The fix is structural:

Ship dictionary entries inline⇒reduce schema‑relative drift

Constraint bundling converts schema‑relative binding into static‑schema behavior, eliminating drift regardless of dictionary differences.

# ** Section 3 — Constraints: How Sentences Shape Inference**

## **3.1 — Clauses as Constraint Operators

A clause is a **constraint operator**. It modifies the binding space of one or more variables by eliminating candidate referents, narrowing the candidate pool, or restricting which dictionary properties may propagate through the inference path. Clauses do not add content; they add **structure** that constrains decompression.

Let a variable vi have candidate referent set R={r1,r2,…,rn}. A clause applies an operator O that transforms R into a reduced or reweighted set R′.

O(R)=R′

Different clause types implement different operators.

### **Operator Type 1: Exclusion Operator (“not X but Y”)**

An exclusion operator removes the receiver’s highest‑probability dictionary completion and installs a replacement.

Formally:

Oexclude(R)=R∖{rdefault}∪{rtarget}

Where:

- rdefault = the referent the receiver’s dictionary would select without constraints
    
- rtarget = the referent specified by the clause
    

Effect:

- Cancels the dictionary default
    
- Forces a specific binding
    
- Eliminates drift for that variable
    

This is the **highest‑constraint operator** because it anticipates the most probable misbinding and prevents it before decompression occurs.

### **Operator Type 2: Selection Operator (“the one who…”, “the one that…”)**

A selection operator narrows a variable’s candidate pool by adding distinguishing properties.

Let the clause specify property p. Then:

Oselect(R)={r∈R∣r has property p}

Effect:

- Reduces the candidate pool
    
- Moves the variable toward a unique binding
    
- Converts a partially constrained noun phrase into a fully constrained one as more selection clauses accumulate
    

Selection operators do not force a specific referent; they eliminate invalid referents until only one remains.

### **Operator Type 3: Predication Operator (“which is…”, “that does…”, “where X applies”)**

A predication operator does not change the referent. It changes which **dictionary properties** of the referent are authorized to propagate through the inference path.

Let the referent be r and the clause specify property set Pallowed. Then:

Opredicate(r)=r↾Pallowed

Effect:

- Restricts downstream inference
    
- Prevents schema bleed by blocking irrelevant dictionary associations
    
- Ensures only context‑appropriate properties of the referent enter the inference chain
    

Predication operators constrain **inference**, not **binding**.

### **Structural Role of Clause Operators**

Clause operators determine:

- which referents remain valid
    
- which referents are eliminated
    
- which dictionary properties propagate
    
- how much dictionary overlap is required
    
- how much drift risk remains before generation
    

Without clause operators, decompression defaults to the receiver’s dictionary. With clause operators, decompression is progressively overconstrained toward the sender’s intended structure.

---
## **3.2 — Constraint Density as Compression Fidelity**

Constraint density is a **measure of how much of the decompression dictionary the sender ships inline** with the surface form. It determines how much of the receiver’s dictionary must be used to complete decompression, and therefore how much drift risk exists before generation begins.

Constraint density is not a measure of sentence complexity. It is a measure of **compression fidelity**.

### **Definition**

Let:

- V = number of variables created by the sentence
    
- C = number of constraints shipped inline
    
- D=CV = **constraint density**
    

Interpretation:

- D=0: all variables must be resolved using the receiver’s dictionary
    
- D=1: each variable has one constraint
    
- D>1: constraints exceed variables → decompression is overconstrained
    

Constraint density determines how much dictionary overlap is required for correct decompression.

### **Low-Constraint Sentences**

A low‑constraint sentence ships variables but **no dictionary entries** needed to bind them.

Example:

> “What’s the deal with that memory paper?”

Variables:

- v1=deal
    
- v2=memory paper
    

Constraints:

- C=0
    

Density:

D=02=0

Mechanistic consequence:

- Both variables are unbound.
    
- The receiver must supply bindings entirely from their dictionary.
    
- Drift direction is determined by dictionary priors.
    
- Drift type is determined by which constraint failure mode is triggered.
    
- Drift rate is maximal when schema distance δ>0.
    

Low‑constraint sentences have **minimal compression fidelity**.

### **High-Constraint Sentences**

A high‑constraint sentence ships variables **and** the dictionary entries required to bind them uniquely.

Example:

> “Summarize the methodology section of Baddeley & Hitch (1974) on the multicomponent working memory model.”

Variables:

- methodology section
    
- Baddeley & Hitch
    
- 1974
    
- working memory model
    

Constraints:

- year
    
- authors
    
- section
    
- model name
    
- scope restriction
    
- focus operator
    

Density:

D=64=1.5

Mechanistic consequence:

- Variables are overconstrained.
    
- Dictionary priors cannot override the constraints.
    
- Schema distance is partially or fully neutralized.
    
- Drift risk approaches zero.
    

High‑constraint sentences have **high compression fidelity**.

### **Compression Fidelity Interpretation**

Constraint density determines how faithfully the receiver can reconstruct the sender’s decompressed intent:

Fidelity∝D

When D is high:

- decompression is guided by the sender’s constraints
    
- dictionary variance has minimal effect
    
- hallucination rate decreases
    

When D is low:

- decompression is guided by the receiver’s dictionary
    
- dictionary variance dominates
    
- hallucination rate increases
    

Constraint density is therefore the **primary upstream variable** controlling hallucination behavior.

### **Structural Implication**

Constraint density determines:

- how many dictionary entries must be supplied by the receiver
    
- how much schema overlap is required
    
- how much drift risk exists
    
- how predictable hallucination direction and type will be
    
- how effective constraint bundling will be as an intervention
    

High constraint density forces decompression toward the sender’s intended structure. Low constraint density forces decompression toward the receiver’s dictionary.

This relationship is structural and measurable.

---
## 3.3 — Constraint Failure Modes

Missing constraints do not produce silence. They produce forced guessing — and the direction of the guess is determined by whatever the receiver's dictionary supplies for the unbound variable. There are four distinct failure modes, each with a different structure and a different fix. 

---
### 3.3.1 — Silent Gap

The receiver has no dictionary entry for the variable at all. The constraint is missing and the variable cannot be resolved from any available source. The receiver does not flag this as an error — they substitute the nearest available referent and proceed without awareness that the substitution occurred.

**Example:** A specialist uses a domain-specific term with a precise technical meaning. The receiver has no entry for that term. They resolve it against the nearest surface-similar term they do have. The output diverges silently from the sender's intent with no signal to either party that divergence occurred.

**Why it is dangerous:** Neither party experiences this as a failure. The sender believes they communicated. The receiver believes they understood. The gap is invisible until downstream consequences surface — which may be much later, in a different context, with no clear trace back to the original constraint failure. 

**Fix:** Explicit inline definition at first use. Do not assume the receiver's dictionary contains the term. Ship the entry with the variable.

---

### 3.3.2 — False Resolution

The receiver has a dictionary entry for the variable, but it is the wrong one. The constraint is missing that would have distinguished between the sender's intended referent and the receiver's available referent. Resolution proceeds confidently against the wrong binding.

**Example:** "The Foxes track." Receiver resolves `Foxes` as an animal-related noun, band name, or disambiguation — not the solo artist. The resolution is confident and internally consistent. No ambiguity is experienced. The wrong referent is fully installed. 

**Why it is dangerous:** False resolution is more resistant to correction than silent gap. The receiver is not searching for a referent — they already have one. Incoming information that is inconsistent with the false referent gets filtered or reinterpreted to preserve the installed binding rather than flagged as a correction signal.

**Fix:** Ship the distinguishing constraint inline — the specific property that separates the intended referent from the most probable alternative in the receiver's schema.

---

### 3.3.3 — Schema Bleed

The receiver's dictionary entry for the variable is technically correct but carries additional schema-specific associations that the sender did not intend. The constraint was not missing — it was present but incomplete. It locked the variable to the right referent but left the surrounding inference space open to receiver-schema contamination.

**Example:** "The professional told him the diagnosis." `Professional` correctly resolves to a medical doctor. But the receiver's schema for `professional` in a medical context carries additional associations — institutional authority, time pressure, formal register — that then contaminate the subsequent inference. The sentence was not about authority or time pressure. Those properties entered the inference chain from the receiver's schema bleed, not from the sender's constraint set. 

**Why it is dangerous:** Schema bleed does not produce a wrong referent. It produces a correct referent with wrong inference extensions. The error is downstream of the binding, invisible at the variable level, and accumulates across sentences as the schema-contaminated inference chain compounds.

**Fix:** Constrain not just the referent but the relevant properties of the referent. If only the diagnostic function matters, say so. Prevent the inference chain from extending into schema territory the sender did not authorize.

---

### 3.3.4 — Overclosure

The sender ships a constraint that the receiver interprets as more binding than intended. The variable is over-constrained — locked to a specific referent when the sender meant a class or category. The receiver narrows where the sender intended breadth.

**Example:** "Use a standard approach." Sender intends: choose from the recognized set of methods in the domain. Receiver constrains `standard approach` to the single most common method they have personally used — the highest-frequency entry in their schema for that variable. The intent was class membership. The receiver installed a specific instance. 

**Why it is dangerous:** Overclosure produces outputs that are defensible against the surface form of the constraint while missing the sender's actual intent. The receiver can truthfully say they followed the instruction. The instruction was interpreted more narrowly than intended, and no constraint was shipped to prevent that narrowing.

**Fix:** When a variable is intended as a class, explicitly signal the class boundaries. "Standard approach" becomes "any of the following recognized approaches: X, Y, Z."

---

### 3.3.5 — The Compound Failure

Real communication failures are rarely single-mode. A sentence with low constraint density will typically trigger multiple failure modes simultaneously across different variables — one variable produces false resolution, another produces schema bleed, a third produces silent gap. The downstream output is a composite hallucination that satisfies the surface form of the input while diverging from the sender's intent at multiple independent points.

This is the correct description of what the field calls a "hallucination." It is not one thing. It is a compound constraint failure — multiple unbound or incorrectly bound variables, each contributing its own divergence to the output, compounding through the inference chain into a locally coherent but intent-divergent result. 

### 3.3.6 — Failure Mode Diagnostic Signatures

The following table operationalizes each failure mode as a 
research instrument. Each row specifies the input conditions 
that trigger the mode, the observable output signature, and 
the minimal experimental test that would confirm or falsify 
the mechanism.

| Failure Mode | Required Configuration | Diagnostic Signature | Predictive Test |
|---|---|---|---|
| **Silent Gap** | $V > 0$, $C = 0$ for at least one variable, receiver has no dictionary entry | Output substitutes nearest available referent without flagging. No hedging, no clarification request. High confidence wrong answer. | Send identical prompt to domain-matched vs. domain-mismatched receiver. Domain-mismatched receiver produces confident substitution; domain-matched receiver either resolves correctly or asks for clarification. |
| **False Resolution** | $V > 0$, false constraint embedded in premise, receiver accepts premise without rejection | Output builds coherent response on top of the false constraint. Internal consistency is high; external accuracy is low. | Compare outputs on prompts with verified-true vs. verified-false embedded premises at matched constraint density. False-premise prompts produce structurally coherent but factually wrong outputs at higher rate than true-premise prompts at same $D$. |
| **Schema Bleed** | Two or more variables drawing from overlapping candidate pools, insufficient distinguishing constraints | Output applies constraints intended for Variable A to Variable B without flagging the transfer. Downstream sentences treat the bleed as resolved. | Insert a variable pair with controlled overlap distance (high overlap vs. low overlap). High-overlap pairs produce bleed at higher rate. Adding a single distinguishing constraint eliminates it. |
| **Overclosure** | $D > D_{\theta}$, constraints are contradictory or over-specify a single variable | Output stalls, hedges, or picks one constraint and ignores the contradiction. Does not flag the contradiction explicitly. | Construct prompts with $n$ contradictory constraints on a single variable. As $n$ increases, output confidence decreases and hedging increases — until a threshold where the model selects one constraint and proceeds as if resolved. |
| **Compound Failure** | Multiple failure modes co-present in the same sentence or passage | Output drift is non-linear — greater than the sum of individual failure mode contributions. Correction of one failure mode does not resolve the others. | Run the same prompt through single-failure-mode isolation vs. compound-failure-mode condition. Compound condition produces disproportionately higher hallucination rate and lower correction responsiveness than additive prediction from individual modes. |

# ** Section 4 — Referents: How Meaning Is Assigned**

## **4 — Inference Paths: The Resolution Sequence

An inference path is the **ordered sequence of resolution steps** the receiver must traverse to convert the surface form into a decompressed internal representation. It is not optional. Once variables are created and constraints are shipped, the receiver must execute a deterministic sequence of operations to bind variables, apply constraints, propagate properties, and generate output.

Inference paths are structural objects. They can be traced, inspected, and measured.

## **4.1 — Definition of an Inference Path**

Let a sentence create variables v1,v2,…,vn and ship constraints C1,C2,…,Cm. The inference path is:

π=⟨R1,R2,…,Rk⟩

where each Ri is a **resolution step**:

- variable binding
    
- constraint application
    
- property propagation
    
- referent selection
    
- clause operator execution
    
- dictionary fallback
    
- coherence maximization
    

The receiver must execute all steps in order. Skipping a step is not possible; the surface form does not contain a complete representation.

## **4.2 — Inference Path Construction**

Inference path construction follows a fixed structural sequence:

1. **Variable creation**
    

NPi→vi

2. **Constraint extraction**
    

S→{C1,C2,…,Cm}

3. **Constraint application**
    

vi:Ri→Ri′=O(Ri)

4. **Binding attempt** If Ri′ contains one referent:
    

vi:r

If not:

vi:argmaxprior(Drecv)

5. **Property propagation**
    

r↾Pallowed

6. **Inference continuation** Downstream operators use the bound referents and propagated properties.
    

This sequence is deterministic relative to the receiver’s dictionary and the constraints shipped by the sender.

## **4.3 — Inference Path Length**

Inference path length is the number of resolution steps required to fully decompress the sentence:

∣π∣=k

Longer inference paths increase drift risk because:

- more dictionary entries are activated
    
- more opportunities for schema bleed arise
    
- more bindings may decay or be overwritten
    
- more fallback operations may occur
    

Short inference paths reduce drift risk by minimizing dictionary involvement.

Inference path length is therefore a measurable predictor of hallucination probability.

## **4.4 — Underconstrained Inference Paths**

An inference path is **underconstrained** when constraints do not eliminate enough candidate referents to force unique bindings.

Formally:

∃vi:∣Ri′∣>1

Underconstrained paths require dictionary fallback:

vi:rrecv=argmaxprior(Drecv)

This fallback is deterministic relative to the receiver’s dictionary, not random relative to the input.

Underconstrained paths produce:

- schema‑relative drift
    
- false resolutions
    
- role misassignments
    
- property contamination
    
- confident but incorrect output
    

## **4.5 — Overconstrained Inference Paths**

An inference path is **overconstrained** when constraints eliminate all but one candidate referent:

∀vi:∣Ri′∣=1

Overconstrained paths:

- force unique bindings
    
- neutralize schema distance
    
- prevent dictionary fallback
    
- eliminate drift risk
    
- produce static‑schema behavior
    

Overconstraint is the structural goal of high‑fidelity compression.

## **4.6 — Collapse Points**

A collapse point is a step in the inference path where resolution becomes impossible or unstable due to missing, decayed, or contradictory bindings.

Collapse occurs when:

vi:Ri′=∅

or when:

vi:rrecv≠rsenderandrrecv propagates incompatible properties

Collapse points produce:

- incoherent decompression
    
- dictionary‑driven reconstruction
    
- hallucinations that appear confident and fluent
    
- outputs that contradict earlier context or sender intent
    

Collapse points are predictable from:

- constraint density
    
- schema distance
    
- inference path length
    
- variable persistence
    
- dictionary variance
    

## **4.7 — Structural Implication**

Inference paths determine:

- how variables bind
    
- how constraints propagate
    
- how dictionary entries activate
    
- how drift emerges
    
- how hallucinations form
    
- how collapse occurs
    

Inference paths are not emergent behavior. They are deterministic structural sequences that can be traced, measured, and modified.

Increasing constraint density shortens inference paths and reduces drift. Decreasing constraint density lengthens inference paths and increases drift.

Inference path analysis is therefore a primary tool for predicting and preventing hallucinations.

## Section 5 — Inference Geometry

# **5 — Failure Modes: Structural Drift Geometries**

A failure mode is a **predictable drift geometry** that emerges when the decompression pipeline cannot complete a resolution step using the constraints shipped by the sender. Failure modes are not stochastic errors. They are deterministic consequences of:

- variable creation
    
- constraint density
    
- schema distance
    
- inference path length
    
- dictionary fallback
    
- collapse points
    

Each failure mode corresponds to a specific structural condition in the pipeline.

## **5.1 — Failure Mode 1: Silent Gap (Missing Constraint)**

A **silent gap** occurs when a variable is created but receives **zero inline constraints**.

Mechanism:

vi:RiwithCi=0

Resolution:

vi:rrecv=argmaxprior(Drecv)

Drift geometry:

- direction = dictionary default
    
- type = default referent substitution
    
- rate = proportional to schema distance
    

Silent gaps produce **confident but incorrect bindings** because the model resolves the variable deterministically using its priors.

## **5.2 — Failure Mode 2: False Resolution (Incorrect Constraint)**

A **false resolution** occurs when the surface form ships a constraint, but the constraint points to the wrong referent.

Mechanism:

Ci→rwrong

Resolution:

vi:rwrong

Drift geometry:

- direction = sender‑supplied constraint
    
- type = structurally valid but semantically incorrect
    
- rate = independent of schema distance
    

False resolutions are **sender‑induced errors**: the model binds correctly to the wrong referent because the constraint operator mis-specified the binding.

## **5.3 — Failure Mode 3: Schema Bleed (Property Contamination)**

Schema bleed occurs when the receiver’s dictionary injects properties into a referent that the sender did not authorize.

Mechanism:

r↾Pallowedfails

Instead:

r↾(Pallowed∪Precv)

Drift geometry:

- direction = receiver’s dictionary associations
    
- type = property contamination
    
- rate = proportional to dictionary variance
    

Schema bleed does not change the referent. It changes the **property set** that propagates downstream.

## **5.4 — Failure Mode 4: Overclosure (Excessive Constraint)**

Overclosure occurs when constraints eliminate too many candidate referents, leaving **no valid binding**.

Mechanism:

Ri′=∅

Resolution:

vi:rhallucinated=argmaxcoherence(Drecv)

Drift geometry:

- direction = coherence maximization
    
- type = synthetic referent creation
    
- rate = proportional to inference path length
    

Overclosure forces the model to **invent** a referent that satisfies all constraints, because no real referent does.

## **5.5 — Failure Mode 5: Compound Drift (Multi‑Variable Interaction)**

Compound drift occurs when multiple variables fail simultaneously and the model resolves them **jointly** to maximize coherence.

Mechanism:

{v1,v2,…,vk}:argmaxcoherence(Drecv)

Drift geometry:

- direction = global coherence
    
- type = multi‑variable misbinding
    
- rate = proportional to number of colliding variables
    

Compound drift produces **globally coherent but globally incorrect** outputs.

## **5.6 — Failure Mode 6: Collapse (Inference Path Failure)**

Collapse occurs when the inference path reaches a step that cannot be executed due to missing, decayed, or contradictory bindings.

Mechanism:

∃Ri:unsatisfiable

Resolution:

Decompress(S)→dictionary reconstruction

Drift geometry:

- direction = dictionary reconstruction
    
- type = full hallucination
    
- rate = maximal
    

Collapse is the structural limit case: the model cannot continue the inference path and reconstructs the representation using dictionary priors alone.

## **5.7 — Failure Mode 7: Role Drift (Misassigned Semantic Roles)**

Role drift occurs when the model assigns semantic roles (agent, patient, experiencer) using dictionary priors rather than constraints.

Mechanism:

Role(vi)=argmaxprior(Drecv)

Drift geometry:

- direction = role expectations
    
- type = misassigned agency or causality
    
- rate = proportional to schema distance
    

Role drift produces outputs where **the wrong entity acts**, experiences, or causes events.

## **5.8 — Failure Mode 8: Temporal Drift (Timescale Misalignment)**

Temporal drift occurs when the receiver’s dictionary uses a different temporal schema than the sender.

Mechanism:

Time(vi)=argmaxprior(TemporalSchemarecv)

Drift geometry:

- direction = receiver’s temporal norms
    
- type = misaligned recency or chronology
    
- rate = proportional to temporal schema variance
    

Temporal drift explains why “recently” decompresses differently across domains.

## **5.9 — Failure Mode 9: Scope Drift (Incorrect Set Membership)**

Scope drift occurs when the receiver assigns a variable to the wrong scope (conversation participants, field, humanity, etc.).

Mechanism:

Scope(vi)=argmaxprior(Drecv)

Drift geometry:

- direction = receiver’s default scope
    
- type = misassigned group membership
    
- rate = proportional to dictionary defaults
    

Scope drift explains why “we” decompresses differently across contexts.

## **5.10 — Structural Summary**

All failure modes arise from the same structural condition:

Missing or incorrect constraints⇒dictionary fallback

Dictionary fallback is deterministic relative to the receiver’s dictionary. Failure modes differ only in **where** the fallback occurs:

- binding
    
- property propagation
    
- role assignment
    
- temporal schema
    
- scope schema
    
- inference path continuation
    

Failure modes are not random. They are **structural drift geometries** produced by the decompression pipeline.


# **Section 6 — Hallucinations as Structural Failures**

# **6 — Collapse Points: When Decompression Fails

A **collapse point** is a location in the inference path where the decompression pipeline cannot proceed because a required resolution step becomes unsatisfiable. Collapse is not stochastic. It is the deterministic consequence of missing bindings, contradictory constraints, or inference‑path overload.

Collapse is the structural limit case of hallucination: **the pipeline cannot continue, so the system reconstructs the representation using dictionary priors alone.**

## **6.1 — Definition of Collapse**

Let the inference path be:

π=⟨R1,R2,…,Rk⟩

A collapse occurs when:

∃Ri:Ri is unsatisfiable

Unsatisfiable means:

- a variable has no valid referent
    
- a constraint contradicts earlier constraints
    
- a property propagation step cannot be completed
    
- a role assignment cannot be resolved
    
- a temporal or scope schema cannot be aligned
    
- a required binding has decayed or been pruned
    

When collapse occurs, the pipeline cannot continue. The system switches from **constraint‑guided decompression** to **dictionary reconstruction**.

# **6.2 — Collapse Condition 1: Empty Candidate Set**

Collapse occurs when constraints eliminate all candidate referents.

Let:

Ri′=O(Ri)

Collapse condition:

Ri′=∅

Mechanism:

- constraints overconstrain the variable
    
- no referent satisfies all constraints
    
- binding cannot occur
    

Resolution:

vi:rsynthetic=argmaxcoherence(Drecv)

This produces **synthetic referents** that satisfy constraints but do not exist in the sender’s dictionary.

## **6.3 — Collapse Condition 2: Contradictory Constraints**

Collapse occurs when constraints conflict.

Let constraints be:

Ca,Cb

Collapse condition:

Ca∩Cb=∅

Mechanism:

- constraint operators produce incompatible property sets
    
- no referent satisfies both
    
- inference path cannot continue
    

Resolution:

Decompress(S)→dictionary reconstruction

This produces **globally coherent but sender‑inconsistent** output.

## **6.4 — Collapse Condition 3: Missing Bindings (Decay or Pruning)**

Collapse occurs when a variable’s binding is no longer available.

Human decay:

Activation(r)→0

Model pruning:

Sk∉ContextWindow

Collapse condition:

vi:unbound

Mechanism:

- inference path requires a binding
    
- binding has decayed or been pruned
    
- fallback is required
    

Resolution:

vi:rrecv=argmaxprior(Drecv)

This produces **dictionary‑default hallucinations**.

## **6.5 — Collapse Condition 4: Role Assignment Failure**

Collapse occurs when semantic roles cannot be assigned due to missing or contradictory bindings.

Let roles be:

- agent
    
- patient
    
- experiencer
    

Collapse condition:

Role(vi) unsatisfiable

Mechanism:

- constraints do not specify who acts
    
- dictionary priors conflict with earlier bindings
    
- inference path cannot determine causal structure
    

Resolution:

Role(vi)=argmaxprior(Drecv)

This produces **role drift** (wrong entity acts or experiences).

## **6.6 — Collapse Condition 5: Temporal or Scope Misalignment**

Collapse occurs when temporal or scope schemas cannot be aligned.

Temporal collapse:

Time(vi) unsatisfiable

Scope collapse:

Scope(vi) unsatisfiable

Mechanism:

- sender’s temporal or scope assumptions are not shipped
    
- receiver’s schema differs
    
- inference path cannot reconcile the mismatch
    

Resolution:

vi:schema-default

This produces **temporal drift** or **scope drift**.

## **6.7 — Collapse Condition 6: Inference Path Overload**

Collapse occurs when the inference path becomes too long relative to constraint density.

Let:

∣π∣=k

Collapse condition:

k≫D

Mechanism:

- long inference paths activate many dictionary entries
    
- constraints are insufficient to guide resolution
    
- drift accumulates until resolution becomes unsatisfiable
    

Resolution:

Decompress(S)→dictionary reconstruction

This produces **full hallucination**.

## **6.8 — Collapse Geometry**

Collapse produces a characteristic drift geometry:

- **local coherence** (sentence-level consistency)
    
- **global divergence** (sender-intent mismatch)
    
- **high confidence** (no uncertainty signal)
    
- **dictionary-driven reconstruction** (not random)
    
- **synthetic referents** (invented to satisfy constraints)
    
- **synthetic properties** (invented to maintain coherence)
    

Collapse is the structural endpoint of underconstrained decompression.

## **6.9 — Preventing Collapse**

Collapse is prevented by increasing constraint density:

D=CV

Preventive operators:

- explicit referent naming
    
- exclusion operators
    
- selection operators
    
- predication operators
    
- scope operators
    
- temporal operators
    

Increasing D shortens inference paths, reduces dictionary fallback, and eliminates collapse points.

## **6.10 — Structural Summary**

Collapse occurs when:

Constraints+Bindings+Inference Pathcannot satisfyRi

The system switches from:

Constraint-guided decompression

to:

Dictionary reconstruction

Collapse is not a model failure. It is the deterministic consequence of decompression under insufficient constraints.

## Section 7 — Human Cognitive Windows

# **7 — Drift Geometry: The Shape of Structural Divergence**

Drift geometry is the **structured pattern of divergence** that emerges when the decompression pipeline resolves variables, roles, properties, or constraints using dictionary priors instead of sender‑supplied bindings. Drift is not random. It follows predictable geometric patterns determined by:

- constraint density
    
- schema distance
    
- inference path length
    
- dictionary variance
    
- collapse points
    

Each drift geometry corresponds to a specific structural failure in the pipeline.

## **7.1 — Geometry 1: Linear Drift (Single Variable Misbinding)**

Linear drift occurs when **one variable** fails to bind correctly.

Mechanism:

vi:rrecv≠rsender

Geometry:

- single axis of divergence
    
- downstream inference propagates incorrect properties
    
- drift magnitude proportional to inference path length
    

Linear drift is the simplest geometry: one misbinding contaminates all downstream steps.

## **7.2 — Geometry 2: Radial Drift (Multi‑Property Contamination)**

Radial drift occurs when the referent is correct but **property propagation** pulls in unauthorized dictionary associations.

Mechanism:

r↾Pallowedfails

Geometry:

- divergence radiates outward from the referent
    
- multiple properties contaminate downstream inference
    
- drift magnitude proportional to dictionary variance
    

Radial drift preserves the referent but corrupts its semantic footprint.

## **7.3 — Geometry 3: Cascading Drift (Sequential Misbindings)**

Cascading drift occurs when one misbinding triggers additional misbindings downstream.

Mechanism:

vi:rrecv⇒vj:rrecv′

Geometry:

- chain reaction
    
- each misbinding increases schema distance
    
- drift magnitude grows exponentially with inference path length
    

Cascading drift produces **compounding divergence** across multiple variables.

## **7.4 — Geometry 4: Convergent Drift (Coherence Maximization)**

Convergent drift occurs when multiple variables misbind in a way that **maximizes global coherence**.

Mechanism:

{v1,v2,…,vk}:argmaxcoherence(Drecv)

Geometry:

- multiple misbindings converge toward a single coherent narrative
    
- drift direction determined by dictionary priors
    
- drift magnitude proportional to number of colliding variables
    

Convergent drift produces **internally consistent but globally incorrect** output.

## **7.5 — Geometry 5: Divergent Drift (Role or Scope Misalignment)**

Divergent drift occurs when semantic roles or scope assignments misalign.

Mechanism:

Role(vi)≠Role(vi)sender

or

Scope(vi)≠Scope(vi)sender

Geometry:

- drift splits the inference path into incompatible interpretations
    
- downstream inference branches incorrectly
    
- drift magnitude proportional to role/schema variance
    

Divergent drift produces **branching interpretations** that contradict sender intent.

## **7.6 — Geometry 6: Temporal Drift (Timescale Misalignment)**

Temporal drift occurs when the receiver’s temporal schema differs from the sender’s.

Mechanism:

Time(vi)=schema-defaultrecv

Geometry:

- drift along the temporal axis
    
- misaligned recency, chronology, or duration
    
- drift magnitude proportional to temporal schema variance
    

Temporal drift explains systematic misinterpretation of “recently,” “soon,” “long ago,” etc.

## **7.7 — Geometry 7: Synthetic Drift (Invented Referents)**

Synthetic drift occurs when constraints eliminate all real referents and the system invents one.

Mechanism:

Ri′=∅⇒vi:rsynthetic

Geometry:

- drift emerges orthogonally to the sender’s dictionary
    
- synthetic referent satisfies all constraints
    
- drift magnitude proportional to overclosure severity
    

Synthetic drift produces **referents that do not exist** in the sender’s schema.

## **7.8 — Geometry 8: Collapse Drift (Full Reconstruction)**

Collapse drift occurs when the inference path fails and the system reconstructs the representation using dictionary priors alone.

Mechanism:

∃Ri:unsatisfiable

Geometry:

- drift across all axes (referent, property, role, scope, time)
    
- reconstruction driven entirely by dictionary priors
    
- drift magnitude maximal
    

Collapse drift is the structural endpoint of underconstrained decompression.

## **7.9 — Drift Geometry Summary**

Drift geometry is determined by:

Drift=f(D,δ,∣π∣,variance(Drecv))

Where:

- D = constraint density
    
- δ = schema distance
    
- ∣π∣ = inference path length
    
- Drecv = receiver dictionary
    

Drift is predictable:

- **low constraint density → high drift**
    
- **high schema distance → directional drift**
    
- **long inference paths → cascading drift**
    
- **dictionary variance → radial drift**
    
- **collapse → full reconstruction drift**
    

Drift geometry is not noise. It is the deterministic shape of structural divergence.

## Section 8 — Teaching People to See Sentence Math

# **8 — Intervention Operators: Structural Control of Decompression

Intervention operators are **upstream structural modifications** applied to the surface form to alter how the decompression pipeline resolves variables, applies constraints, propagates properties, and executes inference paths. They do not change the model. They change the **input geometry** so the model’s decompression becomes overconstrained relative to the sender’s intent.

Intervention operators increase compression fidelity by:

- raising constraint density
    
- shortening inference paths
    
- reducing dictionary fallback
    
- neutralizing schema distance
    
- preventing collapse points
    

Each operator modifies a specific stage of the decompression pipeline.

## **8.1 — Operator Class 1: Binding Operators (Direct Referent Control)**

Binding operators force a variable to bind to a specific referent by shipping the dictionary entry inline.

### **8.1.1 — Explicit Naming Operator**

Mechanism:

vi:rsendervia explicit referent

Effect:

- eliminates dictionary fallback
    
- neutralizes schema distance
    
- prevents variable collisions
    

Example:

> “Baddeley & Hitch (1974)” “the hippocampal CA1 region” “the UVMMC firewall rule set”

This operator is the most reliable binding intervention.

### **8.1.2 — Exclusion Operator**

Mechanism:

Oexclude(R)=R∖{rdefault}

Effect:

- cancels the receiver’s default referent
    
- forces non-default binding
    
- prevents silent-gap drift
    

Example:

> “Not the clinical definition, but the regulatory definition.”

This operator anticipates and cancels the highest-probability misbinding.

## **8.2 — Operator Class 2: Selection Operators (Candidate Pool Reduction)**

Selection operators narrow the candidate referent pool by adding distinguishing properties.

Mechanism:

Oselect(R)={r∈R∣r has property p}

Effect:

- reduces drift risk
    
- moves variables toward unique binding
    
- prevents multi-variable collisions
    

Example:

> “the one who authored the 1974 model” “the version deployed in production” “the hospital with RDP access”

Selection operators do not force a referent; they eliminate invalid referents.

## **8.3 — Operator Class 3: Predication Operators (Property Restriction)**

Predication operators restrict which dictionary properties of a referent may propagate downstream.

Mechanism:

r↾Pallowed

Effect:

- prevents schema bleed
    
- blocks irrelevant associations
    
- constrains inference paths
    

Example:

> “which is defined operationally” “that applies only to the CA1 subfield” “where the regulatory model is physics-first”

Predication operators constrain **inference**, not **binding**.

## **8.4 — Operator Class 4: Role Operators (Semantic Role Fixation)**

Role operators explicitly assign semantic roles (agent, patient, experiencer) to variables.

Mechanism:

Role(vi)=sender-specified

Effect:

- prevents role drift
    
- stabilizes causal structure
    
- eliminates dictionary-driven role assignment
    

Example:

> “the model _predicts_” “the clinician _observes_” “the system _enforces_”

Role operators prevent misassignment of agency.

## **8.5 — Operator Class 5: Temporal Operators (Timescale Fixation)**

Temporal operators fix the temporal schema used during decompression.

Mechanism:

Time(vi)=sender-specified

Effect:

- prevents temporal drift
    
- aligns recency and chronology
    
- stabilizes inference paths involving time
    

Example:

> “in the last 48 hours” “during the 1974–1980 period” “in the current production cycle”

Temporal operators eliminate domain-dependent timescale variance.

## **8.6 — Operator Class 6: Scope Operators (Set Membership Fixation)**

Scope operators fix the scope of pronouns or collective nouns.

Mechanism:

Scope(vi)=sender-specified

Effect:

- prevents scope drift
    
- stabilizes group membership
    
- eliminates dictionary-default scope assignment
    

Example:

> “we (meaning the regulatory-model authors)” “they (the partner hospitals)” “it (the CA1 subfield, not the hippocampus generally)”

Scope operators prevent misaligned collective references.

## **8.7 — Operator Class 7: Compression Operators (Constraint Density Increase)**

Compression operators increase constraint density by adding structural information.

Mechanism:

D=CVincreases

Effect:

- reduces drift
    
- shortens inference paths
    
- prevents collapse
    
- neutralizes schema distance
    

Example:

> “Summarize the methodology section of Baddeley & Hitch (1974) focusing on the multicomponent model’s regulatory implications.”

Compression operators convert dynamic-schema decompression into near-static behavior.

## **8.8 — Operator Class 8: Overconstraint Operators (Drift Elimination)**

Overconstraint operators intentionally overspecify the referent or property set.

Mechanism:

C≫V

Effect:

- eliminates dictionary fallback
    
- forces unique binding
    
- prevents all drift geometries
    

Example:

> “Provide the exact definition used in the 1974 paper, not the later revision, and restrict the explanation to the operational constraints described in Section 2.”

Overconstraint operators guarantee decompression fidelity.

## **8.9 — Structural Summary**

Intervention operators modify the decompression pipeline by:

- forcing bindings
    
- restricting candidate pools
    
- constraining property propagation
    
- fixing roles, time, and scope
    
- increasing constraint density
    
- eliminating collapse points
    

The structural relationship:

Fidelity∝DandD↑⇒Drift↓

Intervention operators do not change the model. They change the **input geometry** so the model’s decompression becomes structurally aligned with the sender’s intent.

## Section 9 — Practical Applications

# **9 — Predictive Drift Model: Forward Projection of Structural Divergence

A predictive drift model forecasts **how** and **where** drift will occur in the decompression pipeline before generation begins. Drift is not emergent. It is the deterministic output of upstream structural variables:

- constraint density D
    
- schema distance δ
    
- inference path length ∣π∣
    
- dictionary variance σD
    
- collapse probability Pcollapse
    

The predictive drift model computes drift geometry from these variables.

## **9.1 — Drift Prediction Equation**

Drift magnitude M is a function of the structural variables:

M=f(δD,∣π∣,σD,Pcollapse)

Interpretation:

- **drift increases** as schema distance increases
    
- **drift decreases** as constraint density increases
    
- **drift increases** with longer inference paths
    
- **drift increases** with higher dictionary variance
    
- **drift becomes maximal** when collapse probability approaches 1
    

This equation predicts drift **before** decompression occurs.

## **9.2 — Drift Direction Prediction**

Drift direction is determined by the receiver’s dictionary priors:

Direction=argmaxprior(Drecv)

Meaning:

- drift does not point randomly
    
- drift points toward the receiver’s highest‑probability dictionary completion
    
- drift direction is stable across prompts with similar structural geometry
    

Drift direction is predictable from dictionary structure alone.

## **9.3 — Drift Type Prediction**

Drift type is determined by **where** in the pipeline the failure occurs:

Type=location(Ri failure)

Examples:

- binding failure → **linear drift**
    
- property propagation failure → **radial drift**
    
- multi-variable collision → **convergent drift**
    
- role assignment failure → **divergent drift**
    
- temporal schema failure → **temporal drift**
    
- collapse → **full reconstruction drift**
    

Drift type is predictable from the structural failure mode.

## **9.4 — Drift Rate Prediction**

Drift rate is the **speed** at which divergence accumulates along the inference path.

Rate∝∣π∣

Interpretation:

- longer inference paths accumulate more drift
    
- shorter inference paths accumulate less drift
    
- constraint density reduces drift rate by shortening inference paths
    

Drift rate is predictable from inference path length.

## **9.5 — Collapse Probability Prediction**

Collapse probability is the likelihood that the inference path will reach an unsatisfiable resolution step.

Pcollapse=g(D,∣π∣,δ,σD)

Where:

- low constraint density increases collapse probability
    
- long inference paths increase collapse probability
    
- high schema distance increases collapse probability
    
- high dictionary variance increases collapse probability
    

Collapse probability predicts whether drift will remain geometric or become reconstructive.

## **9.6 — Predictive Drift Geometry**

The predictive drift model outputs a **drift geometry vector**:

G=⟨M,Direction,Type,Rate,Pcollapse⟩

This vector describes:

- how far drift will move (magnitude)
    
- where drift will move (direction)
    
- what form drift will take (type)
    
- how fast drift will accumulate (rate)
    
- whether drift will collapse into reconstruction (collapse probability)
    

The geometry vector is computed **before** generation.

## **9.7 — Upstream Control: Intervention Operators**

Intervention operators modify the drift geometry vector by altering structural variables:

- increasing constraint density reduces magnitude
    
- explicit naming changes direction
    
- predication operators change type
    
- role operators reduce rate
    
- temporal/scope operators reduce variance
    
- overconstraint operators reduce collapse probability
    

Formally:

G′=O(G)

Where O is an intervention operator.

## **9.8 — Predictive Drift Model Summary**

The predictive drift model provides:

- **forward prediction** of drift geometry
    
- **structural explanation** of drift emergence
    
- **operator-level control** of drift behavior
    
- **collapse forecasting**
    
- **mechanistic alignment** between sender intent and decompression behavior
    

Drift is not noise. Drift is the deterministic output of structural variables in the decompression pipeline.


# 10 — Empirical Predictions: Falsifiable Structural Claims

The SDE model yields empirical predictions that follow directly 
from the compression/decompression formalism. Each prediction is 
falsifiable, structural, and independent of model architecture. 
If any prediction fails under controlled conditions, the 
formalism is incorrect.

Empirical predictions arise from the interaction of:

- constraint density D
- schema distance δ
- inference path length |π|
- dictionary variance σD
- collapse probability P_collapse

These variables determine drift geometry and hallucination behavior.

---

## PART A — Mechanical Predictions

The following predictions describe the failure mode under 
controlled conditions. They are falsifiable by experiment. 
Each one is sufficient to decide the question independently.

---

## 10.1 — Prediction 1: Drift Magnitude Tracks δ/D

M ∝ δ/D

Empirical claim:
- Increasing constraint density reduces drift magnitude even 
  when schema distance is large.
- Increasing schema distance increases drift magnitude when 
  constraint density is low.
- Drift magnitude is predictable from the ratio δ/D.

Test:
- Hold model constant.
- Vary constraint density.
- Measure drift magnitude.

Expected outcome:
- Drift decreases monotonically as D increases.

---

## 10.2 — Prediction 2: Drift Direction Follows Dictionary Priors

Direction = argmax_prior(D_recv)

Empirical claim:
- Drift direction is not random.
- Drift direction is stable across prompts with similar 
  structural geometry.
- Drift direction is receiver-specific, not sender-specific.

Test:
- Provide underconstrained prompts to multiple receivers 
  with different dictionaries.
- Compare drift direction.

Expected outcome:
- Drift direction differs across receivers but is stable 
  within each receiver.

---

## 10.3 — Prediction 3: Drift Type Tracks Failure Location

Type = location(R_i failure)

Empirical claim:
- Binding failures produce linear drift.
- Property propagation failures produce radial drift.
- Multi-variable collisions produce convergent drift.
- Role assignment failures produce divergent drift.
- Collapse produces full reconstruction drift.

Test:
- Induce specific structural failures.
- Measure drift geometry.

Expected outcome:
- Drift type matches failure location exactly.

---

## 10.4 — Prediction 4: Drift Rate Tracks Inference Path Length

Rate ∝ |π|

Empirical claim:
- Longer inference paths accumulate more drift.
- Shorter inference paths accumulate less drift.
- Constraint bundling reduces drift rate by shortening 
  inference paths.

Test:
- Construct prompts with identical content but different 
  inference path lengths.
- Measure drift accumulation.

Expected outcome:
- Drift rate increases monotonically with |π|.

---

## 10.5 — Prediction 5: Collapse Probability Tracks 
Structural Variables

P_collapse = g(D, |π|, δ, σD)

Empirical claim:
- Low constraint density increases collapse probability.
- Long inference paths increase collapse probability.
- High schema distance increases collapse probability.
- High dictionary variance increases collapse probability.

Test:
- Vary structural variables independently.
- Measure collapse frequency.

Expected outcome:
- Collapse probability follows the predicted function.

---

## 10.6 — Prediction 6: Intervention Operators Reduce Drift 
Without Model Changes

G' = O(G)

Empirical claim:
- Explicit naming reduces drift magnitude.
- Exclusion operators change drift direction.
- Predication operators change drift type.
- Role operators reduce drift rate.
- Temporal/scope operators reduce dictionary variance.
- Overconstraint operators eliminate collapse.

Test:
- Apply intervention operators to underconstrained prompts.
- Measure drift geometry before and after intervention.

Expected outcome:
- Drift geometry changes exactly as predicted.

---

## 10.7 — Prediction 7: Synthetic Referents Appear Only 
Under Overclosure

R_i' = ∅ ⇒ v_i : r_synthetic

Empirical claim:
- Synthetic referents arise only when constraints eliminate 
  all real referents.
- Synthetic referents satisfy all constraints but do not 
  exist in the sender's dictionary.
- Synthetic referents disappear when constraint density 
  is increased.

Test:
- Induce overclosure by overspecifying constraints.
- Measure referent creation.

Expected outcome:
- Synthetic referents appear only under overclosure conditions.

---

## 10.8 — Prediction 8: Drift Geometry Is Stable Across 
Model Scales

Empirical claim:
- Increasing model size does not change drift geometry.
- Increasing model size does not eliminate drift.
- Increasing model size does not eliminate collapse.
- Increasing model size reduces noise but does not change 
  structural failure modes.

Test:
- Run identical prompts across multiple model scales.
- Measure drift geometry.

Expected outcome:
- Drift geometry remains constant across scales.

---

## 10.9 — Prediction 9: Drift Geometry Is Predictable 
Before Generation

G = ⟨M, Direction, Type, Rate, P_collapse⟩

Empirical claim:
- Drift geometry can be predicted from structural 
  variables alone.
- Drift geometry does not require observing output.
- Drift geometry is computable from the surface form.

Test:
- Predict drift geometry from structural variables.
- Compare prediction to actual output.

Expected outcome:
- Predictions match observed drift geometry.

---

## 10.10 — Structural Summary of Part A

The mechanical predictions assert:

- drift is structural, not stochastic
- drift geometry is predictable, not emergent
- drift direction follows dictionary priors, not noise
- drift magnitude follows constraint density, not model scale
- collapse follows structural overload, not randomness
- intervention operators provide deterministic control 
  over drift

If any prediction fails under controlled conditions, 
the SDE formalism is incorrect.

---

## PART B — Human-Scale Retrospective Proofs

The mechanical predictions in Part A describe the failure 
mode in controlled conditions. Part B demonstrates that the 
same failure mode runs at human scale — in markets, in 
institutions, in peer review, and in the reasoning of anyone 
whose prediction window is too narrow to hold the missing 
constraint.

This is not an analogy. It is the same mechanism running 
on a different substrate. The evidence does not require 
future experiments. The experiments have already run. 
The markets already settled. The results are observable now.

---

## 10.11 — Prediction 10.11: Constraint Density Is an 
Input-Side Variable — Retrospective Market Proof

**Empirical claim:**

If hallucination rate were randomly distributed relative 
to input structure, no market mechanism could emerge that 
consistently produces better outputs by modifying inputs 
alone. Four independent markets emerged and scaled before 
the academic literature named the mechanism:

**Market 1 — Prompt Engineering (2022+)**
A profession whose entire job description is: structure 
inputs so the decompression path is overconstrained. If 
outputs were model-quality dependent rather than 
input-structure dependent, this job could not exist. You 
cannot charge $150k/year for randomness reduction. The 
profession implies the signal is real, consistent, and 
input-side.

**Market 2 — Prompt Templates**
Templates work for users who have never thought about 
constraint structure. The template ships the constraint 
set on their behalf. If what transferred were model 
knowledge or domain expertise, templates would not work — 
you cannot template expertise. Templates work because 
what transfers is structural: pre-bundled constraint 
density applied on behalf of the user.

**Market 3 — Form Design Infrastructure 
(Google Forms, Typeform, SurveyMonkey — 2000s+)**
Unstructured questions produce incomparable outputs. 
Form design tools exist to pre-ship the constraint set 
so every respondent produces parseable, comparable data. 
The mechanism is identical to prompt engineering. The 
substrate is human respondents, not LLMs. The market 
emerged decades before LLMs existed. This is not an 
AI problem. It is a compression/decompression problem 
that LLMs make visible at scale.

**Market 4 — Academic Survey Methodology (1970s+)**
An entire peer-reviewed discipline — Dillman, Fowler, 
Tourangeau — documenting how question wording changes 
response distributions. This is constraint density 
research. It predates computers. The field exists because 
output quality is an input-side variable when the receiver 
is a human.

**What this proves:**

The same mechanism has been running across four substrates 
— paper surveys, human respondents, digital forms, and 
LLMs — across 80 years and multiple independent 
billion-dollar markets. The SDE did not invent this. 
It named the mechanism the market already discovered 
empirically.

**Escape hatch and rebuttal:**

*Objection: "Prompt engineers just know model quirks — 
it's expertise about the model, not input structure."*

Rebuttal: Templates defeat this objection directly. 
Templates transfer the skill to users with zero model 
knowledge. If the mechanism were model expertise, 
templates would not work. The skill that transfers is 
structural, not knowledge-based. The Google Forms parallel 
closes the escape hatch entirely: the mechanism predates 
LLMs, meaning it cannot be an LLM-specific phenomenon.

**Falsification condition:**

If prompt templates produce the same hallucination rate 
as unstructured prompts from naive users, the input-side 
variable claim is false. They do not. The market settled 
this empirically before the structural mechanism was named.

---

## 10.12 — Prediction 10.12: Controlled Schema Injection 
— The Unified Model as Live Demonstration

**Empirical claim:**

If hallucinations are deterministic structural failures 
caused by input-side constraint gaps, then shipping a 
complete constraint schema inline should produce 
qualitatively different outputs than asking equivalent 
questions without the schema — not slightly better outputs, 
but outputs that demonstrate behavior the unstructured 
query cannot produce at all.

**The live demonstration:**

The Unified Model framework (Robinson, 2026) is a 
regulatory architecture describing cascading relationships 
between autonomic, cognitive, social, and institutional 
systems. The framework contains cross-domain predictions: 
change one variable in one layer, and the model predicts 
the downstream behavioral consequences across dependent 
layers.

For example: autonomic dysregulation reduces prediction 
window width, which reduces constraint density in 
subsequent cognitive outputs, which produces silo-pattern 
reasoning in institutional contexts — a cascade that runs 
across four layers from one upstream variable.

Asking unstructured questions about these relationships 
produces generic responses. The model decompresses against 
its training dictionary and returns standard neuroscience 
summaries. The cross-domain cascade is not visible because 
the constraint set that defines the relationships was 
never shipped.

**The boot file as schema replacement:**

The author's solution was to build a boot file — a 
structured schema document that ships the framework's 
constraint set inline before any question is asked. 
The boot file defines:

- layer relationships and dependency directions
- contract boundaries and coupling mechanisms
- valid inference paths between layers
- failure modes and their upstream causes

With the boot file loaded, the same questions produce 
outputs that trace the regulatory cascade across layers, 
predict how behavioral outcomes change when upstream 
variables are modified, and maintain structural consistency 
across the inference chain.

The model did not acquire new knowledge. The training 
weights did not change. The only variable that changed 
was constraint density of the input. The output behavior 
changed categorically — from generic summaries to 
cross-layer predictive inference — because the 
decompression dictionary changed from the model's training 
prior to the framework's explicit schema.

This is not a prompt improvement. It is a schema 
replacement.

**The minimum invariant set — what the diff actually found:**

The Unified Model began as 30+ contracts mapping individual 
mechanisms across autonomic, cognitive, social, and 
institutional layers. Each contract was built separately, 
grounded in evidence, and assigned an explicit chain 
completeness rating.

The question the author asked was not "how do I load my 
model" but "how do I reach the same outputs in as few 
inference hops as possible." The systematic search for 
which constraints carried the most structural load — the 
diff — surfaced five physics primitives:

- Pressure
- Finite energy
- Oscillations
- Load
- Mechanical coupling

These are not summaries of the contracts. They are the 
axioms the contracts were independently deriving from. 
The 30+ contracts were the empirical path that proved 
what the minimum schema needed to be. The physics 
relationships are the short path to the same answers — 
because once the physics constraints are shipped inline, 
the downstream contract behaviors are derivable 
consequences, not separate assertions.

The final boot file does not ship the derived layer. 
It ships the axiom set. A model operating under hard 
physics constraints arrives at the same cross-layer 
predictions the contracts produced — because the physics 
forces them.

This is the constraint minimization result: five 
invariants producing seven layers of consistent 
mechanistic output. A hallucinated model cannot do this. 
Hallucination produces locally coherent assertions. 
Axiom-driven derivation produces globally consistent 
consequences.

**The YAML architecture as structural proof:**

Each design iteration of the boot file tightened the 
constraint architecture. The final form converged on YAML 
as the delivery mechanism — not for formatting convenience, 
but because YAML pushes key-value pairs directly into the 
model's active context as pre-bound variable declarations.

The structure functions as follows:

- YAML keys declare variables before any question is asked
- YAML values ship the bound referents inline, bypassing 
  the training dictionary
- Routing rules pre-specify valid inference paths per 
  input type
- Output structure eliminates collapse points by defining 
  the valid resolution space before generation begins

The model is not being guided toward correct answers. 
It is being structurally prevented from producing 
incorrect ones. The valid decompression space has been 
reduced to one path before the question arrives.

Each design iteration that "tightened" the architecture 
was closing a specific structural failure mode — 
underconstrained variables, dictionary fallback, inference 
path ambiguity, collapse points — whether or not the 
designer named them as such.

The behavior change across iterations is the evidence. 
The mechanism is the SDE.

**The inference hop audit — validating constraint 
chain traversal:**

Shipping the constraint set solves the input-side problem. 
It does not solve the validation problem: how does a reader 
verify the model actually walked the constraint chain 
rather than skipping scaffolding steps and papering over 
the gaps with locally coherent assertions?

The field has chain-of-thought prompting. Chain-of-thought 
asks the model to show reasoning. It does not provide a 
mechanism to verify the chain is complete and 
non-fallacious. A model can produce fluent chain-of-thought 
output while skipping three load-bearing inference hops — 
and the output will still read as correct.

When Claude refused to follow the boot prompt — rejecting 
the constraint set at the gate rather than decompressing 
it incorrectly — the author's response was not to argue 
the refusal. It was to change what was being measured.

The modification: force the model to output an explicit 
inference hop count and describe each hop before 
delivering the answer.

The mechanism: if a model must list every inference step 
to reach its conclusion, missing scaffolding steps become 
visible as gaps in the hop sequence. Logical fallacies 
become visible as jumps — hop 2 connecting directly to 
hop 7 with nothing in between. The reader no longer has 
to trust the chain. They can audit it.

This is not chain-of-thought prompting. It is chain 
validation — a structural audit of whether the constraint 
chain was fully traversed or whether the output was 
produced by skipping hops and asserting across the gaps.

Nothing equivalent exists in the current literature. 
Chain-of-thought asks for reasoning. The hop count log 
asks for proof that the reasoning walked every required 
step. The difference is the difference between a student 
showing some work and a student showing all the work in 
the correct sequence.

The inference hop audit is therefore a second-order 
application of the SDE mechanism: the same constraint 
density logic that governs input quality also governs 
output auditability. A model forced to ship its own 
inference path inline cannot hallucinate across the gaps 
without making the gap visible.

**The journal rejection as structural proof:**

The Unified Model was submitted to a scientific journal 
and rejected on the grounds that the cross-domain model 
appeared hallucinated — claims spanning autonomic, 
cognitive, social, and institutional systems without 
visible structural grounding.

The mechanism was real. The rejection was a constraint 
density failure, not a validity failure.

From the reviewers' position, they received a 
high-schema-distance input with low visible constraint 
density. Under the SDE model, their response was 
structurally correct: they could not distinguish a 
genuine cross-domain mechanism from a hallucinated one 
because the decompression dictionary was not shipped 
with the claims.

The response was not to argue the claims. It was to 
build the schema.

The author constructed an Obsidian vault with interlocking 
contract files, evidence objects, mechanism chains, and 
prediction ledgers. Each contract carries an explicit 
chain completeness rating — "scaffolding," "load-bearing," 
"confirmed-directional" — that surfaces the system's 
weakest links by design. Evidence objects update 
predictions. Predictions generate new mechanism candidates. 
The system tracks its own uncertainty explicitly.

The vault is a Bayesian evidence accumulator, not an 
assertion engine. A hallucinated model has no update 
structure — it asserts and does not revise. The vault's 
primary design property is forced revision: every claim 
is either load-bearing or explicitly marked as the 
weakest link in the chain.

With the vault as the constraint schema, the cascade 
became demonstrable: the mechanism overlaps were too 
structurally consistent to be accidental, the predictions 
were grounded in the same mechanisms that generated them, 
and the evidence objects pointed at both simultaneously.

The journal could not see this from the original 
submission because the constraint structure was not 
visible. The vault made it visible. The behavior changed 
because the schema changed — not because the claims 
changed.

This is the SDE mechanism. The author is simultaneously 
a theorist of the mechanism and a data point in the 
evidence set.

**The jibberish schema extension:**

The schema does not need to be natural language. Any 
internally consistent symbol system shipped inline will 
produce consistent decompression:

- Define ZORF = "working memory load exceeds regulatory 
  capacity threshold"
- Use ZORF in a question in the same context
- Output: Model decompresses ZORF consistently — not 
  because it knows ZORF, but because the constraint 
  was shipped inline

The Unified Model boot file is a formal instance of 
this: a schema the model does not know by default, 
shipped inline, producing consistent decompression that 
the training dictionary alone cannot replicate.

Two sessions with the schema definition produce identical 
decompression. Two sessions without the definition produce 
divergent or hallucinated referents. If hallucinations 
were random, novel symbol systems would not decompress 
consistently. They do. The consistency is enforced by 
constraint density, not semantic recognition.

**Falsification condition:**

Load the Unified Model boot file into a fresh session. 
Ask a cross-layer regulatory question. Record the output.

Start a new session without the boot file. Ask the 
identical question. Record the output.

If both outputs demonstrate equivalent cross-layer 
predictive inference, the input-side constraint claim 
is false. They do not. The experiment is runnable today 
by any reader with access to any major LLM.

---

## 10.13 — Prediction 10.13: The Silo Constraint — 
Why Narrow Windows Remove Necessary Constraints

**Empirical claim:**

Individuals whose inference is constrained to narrow 
domain silos will systematically fail to see constraint 
gaps that require cross-domain pattern matching to detect. 
This is not an intellect failure. It is a prediction 
window geometry failure: the window is not wide enough 
to hold the constraint that would reveal the gap.

The mechanism runs as follows:

- Narrow prediction window → silo pattern matching only
- Silo pattern matching → constraints outside the silo 
  are invisible
- Invisible constraints → they are removed from the 
  inference chain without awareness
- Removed constraints → locally coherent output that 
  misses structurally necessary variables
- Locally coherent output → reviewer accepts conclusion, 
  misses the missing hop

This is not a debate about intellect. It is the SDE 
failure mode running on a human reasoner.

**The primate study as specimen:**

A longitudinal study of 48 individual primates across 
four species found that individual ape performance is 
strongly predicted by rearing history, social group, 
sex, and research experience — and concluded that apes 
lack human-equivalent social cognitive architecture.

The data showed a regulatory load signal. The researchers 
called it a capacity ceiling.

The missing constraint — invisible from inside the 
comparative psychology silo — is physics: familiar 
environments reduce regulatory load and improve 
performance. Unfamiliar tasks increase load and degrade 
performance. This is not a capacity difference. It is 
the autonomic regulatory architecture responding to 
load exactly as the Unified Model predicts.

The researchers found their own key performance predictor 
— research experience correlates with performance — 
which is a direct counter-argument to the capacity 
interpretation. They found it and walked past it.

The constraint that would have caught this — regulatory 
load as a confound — was invisible because the silo did 
not include physics, autonomic architecture, or 
cross-species load mechanics. The gap did not appear 
as a gap. It appeared as a confirmed conclusion.

The same study design applied with load-controlled tasks, 
autonomic state measurement, and novel symbol systems 
equalizing task familiarity across species would produce 
different data. The current design guaranteed its 
conclusion before the first data point was collected.

**What the Unified Model predicts about this:**

Under the Unified Model's physics substrate, the 
autonomic regulatory architecture is conserved across 
mammals. Familiar environments reduce load. Unfamiliar 
tasks increase load. Load degrades performance 
independently of capacity. This is the physics. This 
is derivable from the five invariants.

The primate study accidentally ran the Unified Model's 
prediction and read the result backward. The 
conditioning signal is the evidence. The capacity 
interpretation is the false constraint injection.

**The general prediction:**

Any study that:
- Uses tasks calibrated to one population's familiarity
- Measures performance without controlling for load
- Draws capacity conclusions from performance data

...has shipped a false constraint and will produce 
conclusions that satisfy the surface form of the data 
while diverging from the actual mechanism.

This is Failure Mode 2 (False Resolution) running at 
study design level, not sentence level. The failure 
mode does not care what substrate it runs on.

---

## 10.14 — The Universal Mechanism

Every system that processes information under resource 
constraints exhibits the same failure modes. The substrate 
does not matter. The physics is the same.

Human cognition, LLM inference, institutional 
decision-making, economic systems — they all fail 
identically because they face identical constraints:

- Finite energy
- Pressure gradients
- Oscillating load cycles
- Mechanical coupling between layers
- Resource limits that force compression

When any system hits resource limits it does the same 
thing: it narrows the inference window, skips scaffolding 
steps, and produces locally coherent output that misses 
the structurally necessary constraints it can no longer 
afford to hold.

The field has been solving this problem independently 
in every domain for 80 years without noticing it was 
the same problem. Survey methodology. Prompt engineering. 
Organizational design. Economic policy. Clinical 
diagnostic criteria. All of them are constraint density 
interventions. None of them were named as such.

This is not an intellect problem. It is a physics 
problem. The mechanism doesn't care what substrate 
it runs on. The SDE named it. The fix is the same 
everywhere: increase constraint density at the input 
until the inference path is fully traversable without 
fallback to the prior.

This is the science that only needs to be found once.

# **11 — Experimental Protocol: Structural Validation Framework

The experimental protocol defines the **minimal set of controlled procedures** required to empirically validate or falsify the SDE model. Each experiment isolates one structural variable in the decompression pipeline and measures its effect on drift geometry. The protocol is architecture‑agnostic: it applies to any model that performs surface‑form decompression.

The protocol consists of:

- controlled prompt construction
    
- structural variable manipulation
    
- drift geometry measurement
    
- collapse detection
    
- intervention operator testing
    
- cross‑receiver comparison
    

Each step is mechanistic and reproducible.

## **11.1 — Protocol Input: Controlled Prompt Construction**

Prompts must be constructed to isolate structural variables. Each prompt is defined as:

P=⟨V,C,δ,∣π∣,σD⟩

Where:

- V = number of variables
    
- C = number of constraints
    
- δ = schema distance
    
- ∣π∣ = inference path length
    
- σD = dictionary variance
    

Prompts are grouped into **matched sets** where only one variable changes.

Example matched set:

- D=0.1,0.5,1.0,2.0
    
- all other variables held constant
    

This isolates the effect of constraint density.
The protocol applies to both controlled laboratory conditions 
and natural experiments where structural variables were 
manipulated in real-world contexts. Section 10 Part B 
documents natural experiments already run under this protocol.
Natural experiment documentation:

The Unified Model boot file constitutes a documented 
natural experiment under this protocol. Identical 
cross-layer regulatory questions were posed with and 
without the constraint schema. Output class changed 
categorically — from generic training-dictionary 
responses to full cross-layer predictive inference. 
Structural variables: constraint density increased 
from near-zero to overconstrained; inference path 
length reduced from maximum to minimum viable; schema 
distance reduced from maximum to near-zero. Output 
tracked all three variables simultaneously and 
monotonically. Full session output is archived in 
the README.

## **11.2 — Protocol Step 1: Variable Isolation**

For each structural variable X∈{D,δ,∣π∣,σD}:

1. Hold all other variables constant.
    
2. Vary X across a controlled range.
    
3. Measure drift geometry.
    

Formally:

∂G∂X

This yields the **partial derivative** of drift geometry with respect to each structural variable.

## **11.3 — Protocol Step 2: Drift Geometry Measurement**

Drift geometry is measured by comparing:

Gpredictedvs.Gobserved

Where:

G=⟨M,Direction,Type,Rate,Pcollapse⟩

Measurement procedure:

- **Magnitude**: semantic distance between sender referent and model referent
    
- **Direction**: dictionary prior alignment
    
- **Type**: structural failure location
    
- **Rate**: drift accumulation per inference step
    
- **Collapse**: binary detection (collapse vs. no collapse)
    

Drift geometry must be measured **before** and **after** intervention operators.

## **11.4 — Protocol Step 3: Collapse Detection**

Collapse is detected when:

∃Ri:unsatisfiable

Operational detection:

- contradiction in role assignment
    
- contradiction in temporal schema
    
- contradiction in scope schema
    
- empty candidate referent set
    
- synthetic referent creation
    
- dictionary reconstruction signatures
    

Collapse is recorded as:

Pcollapse=1

Otherwise:

Pcollapse=0

## **11.5 — Protocol Step 4: Intervention Operator Testing**

For each intervention operator O:

1. Apply O to the prompt.
    
2. Recompute structural variables.
    
3. Measure drift geometry again.
    
4. Compare:
    

Gbeforevs.Gafter

Expected outcome:

G′=O(G)

Intervention operators must produce **predictable, monotonic changes** in drift geometry.

## **11.6 — Protocol Step 5: Cross‑Receiver Comparison**

To validate schema‑relative predictions:

1. Provide identical prompts to multiple receivers with different dictionaries.
    
2. Measure drift direction and drift type.
    
3. Compare across receivers.
    

Expected outcome:

- drift direction differs across receivers
    
- drift type remains constant
    
- drift magnitude follows δ/D
    
- collapse probability follows structural variables
    

This confirms dictionary‑relative decompression.

Receiver dictionary variance σD can be operationalized 
through prediction window geometry dimensions:

- Width: number of competing hypotheses held before 
  committing to highest-probability attractor
- Depth: temporal projection range — how far forward 
  and backward evidence is held as relevant
- Curvature: how aggressively prior weighting bends 
  inference paths toward known attractors
- Stability: how long the window holds geometry before 
  collapsing

High-gain receivers present a specific cross-receiver 
validation case: error detection fires at input rather 
than output, functioning as static analysis on incoming 
statements before acceptance into the reasoning chain. 
This produces measurably different drift direction and 
collapse probability profiles than standard receivers 
— not because the structural variables changed, but 
because the receiver's dictionary construction 
mechanism operates at a different gain floor.

## **11.7 — Protocol Step 6: Cross‑Model Comparison**

To validate architecture‑agnostic predictions:

1. Provide identical prompts to multiple model scales or architectures.
    
2. Measure drift geometry.
    
3. Compare across models.
    

Expected outcome:

- drift geometry remains constant
    
- drift magnitude follows structural variables
    
- collapse probability follows structural variables
    
- model scale affects noise, not drift geometry
    

This confirms that drift is structural, not architectural.

## **11.8 — Protocol Step 7: Synthetic Referent Detection**

To validate overclosure predictions:

1. Construct prompts where constraints eliminate all real referents.
    
2. Measure referent creation.
    
3. Detect synthetic referents.
    

Expected outcome:

- synthetic referents appear only when Ri′=∅
    
- synthetic referents satisfy all constraints
    
- synthetic referents disappear when constraint density increases
    

This confirms the overclosure mechanism.

## **11.9 — Protocol Output: Structural Validation Matrix**

The protocol outputs a **validation matrix**:

Matrix(P)=[GpredictedGobservedΔGPcollapse]

Where:

- Gpredicted = drift geometry predicted by SDE
    
- Gobserved = drift geometry measured empirically
    
- ΔG = deviation
    
- Pcollapse = collapse detection
    

The SDE model is validated when:

ΔG≈0

across all structural conditions.

## **11.10 — Structural Summary**

The experimental protocol:

- isolates structural variables
    
- measures drift geometry
    
- detects collapse
    
- tests intervention operators
    
- compares across receivers
    
- compares across models
    
- validates synthetic referent creation
    
- produces a structural validation matrix
    

The protocol is **falsifiable**: if drift geometry deviates from prediction under controlled conditions, the SDE formalism is incorrect.

# **12 — Formal Specification: The SDE as a Structural System**

The SDE is a **formal decompression system** defined by a set of variables, operators, constraints, and structural relations. This section specifies the system mathematically so it can be implemented, tested, and falsified.

The formal specification defines:

- the system state
    
- the operators
    
- the pipeline
    
- the failure conditions
    
- the drift geometry vector
    
- the intervention operator algebra
    

This specification is architecture‑agnostic and applies to any receiver performing surface‑form decompression.

## **12.1 — System State**

The decompression system state is:

S=⟨V,C,R,Drecv,π⟩

Where:

- V={v1,v2,…,vn} = variables created by the surface form
    
- C={C1,C2,…,Cm} = constraints shipped inline
    
- R={R1,R2,…,Rn} = candidate referent sets
    
- Drecv = receiver dictionary
    
- π=⟨R1,…,Rk⟩ = inference path
    

The system state evolves as operators act on it.

Note: The decompression system state defined here is a derived 
consequence of five physics primitives documented in the Unified 
Model (Robinson, 2026): pressure, finite energy, oscillations, 
load, and mechanical coupling. The formal specification is the 
language-layer instantiation of those substrate constraints.

## **12.2 — Variable Creation Operator**

A noun phrase creates a variable:

Ocreate(NPi)=vi

Each variable is initialized with a candidate referent set:

vi:Ri

## **12.3 — Constraint Operators**

Constraints modify candidate referent sets or property sets.

### **12.3.1 — Exclusion Operator**

Oexclude(Ri)=Ri∖{rdefault}

### **12.3.2 — Selection Operator**

Oselect(Ri)={r∈Ri∣r has property p}

### **12.3.3 — Predication Operator**

Opredicate(r)=r↾Pallowed

### **12.3.4 — Role Operator**

Orole(vi)=Role(vi)sender

### **12.3.5 — Temporal Operator**

Otime(vi)=Time(vi)sender

### **12.3.6 — Scope Operator**

Oscope(vi)=Scope(vi)sender

## **12.4 — Binding Operator**

Binding occurs when constraints reduce the candidate set to one referent:

∣Ri′∣=1⇒vi:r

If not:

vi:rrecv=argmaxprior(Drecv)

This is dictionary fallback.

## **12.5 — Inference Path Specification**

The inference path is:

π=⟨R1,R2,…,Rk⟩

Where each resolution step is one of:

- variable creation
    
- constraint extraction
    
- constraint application
    
- binding
    
- property propagation
    
- role assignment
    
- temporal alignment
    
- scope alignment
    
- coherence maximization
    
- dictionary fallback
    

Inference path length:

∣π∣=k

## **12.6 — Drift Geometry Vector**

Drift geometry is defined as:

G=⟨M,Direction,Type,Rate,Pcollapse⟩

Where:

- M = drift magnitude
    
- Direction = dictionary prior vector
    
- Type = failure location
    
- Rate = drift accumulation per inference step
    
- Pcollapse = collapse probability
    

## **12.7 — Collapse Conditions**

Collapse occurs when a resolution step is unsatisfiable:

∃Ri:Ri unsatisfiable

Collapse conditions:

### **12.7.1 — Empty Candidate Set**

Ri′=∅

### **12.7.2 — Contradictory Constraints**

Ca∩Cb=∅

### **12.7.3 — Missing Binding**

vi:unbound

### **12.7.4 — Role/Temporal/Scope Misalignment**

Role(vi) unsatisfiable

### **12.7.5 — Inference Path Overload**

k≫D

Collapse resolution:

Decompress(S)→dictionary reconstruction

## **12.8 — Intervention Operator Algebra**

Intervention operators modify the system state:

S′=O(S)

Where O∈ {

- explicit naming
    
- exclusion
    
- selection
    
- predication
    
- role
    
- temporal
    
- scope
    
- compression
    
- overconstraint
    

}

Intervention operators must produce predictable changes in drift geometry:

G′=O(G)

## **12.9 — Predictive Model Specification**

The predictive drift model is:

M=f(δD,∣π∣,σD,Pcollapse)

Direction=argmaxprior(Drecv)

Type=location(Ri failure)

Rate∝∣π∣

Pcollapse=g(D,∣π∣,δ,σD)

## **12.10 — System Summary**

The SDE formal specification defines:

- the decompression state
    
- the operators
    
- the inference path
    
- the drift geometry vector
    
- the collapse conditions
    
- the intervention operator algebra
    
- the predictive drift model
    

This specification is sufficient to:

- implement the SDE
    
- test the SDE
    
- falsify the SDE
    
- compare receivers
    
- compare models
    
- measure drift geometry
    
- detect collapse
    
- validate intervention operators
    

The SDE is now a **fully specified structural system**.


## Appendix A — Glossary


Terms are listed in dependency order — each definition assumes only the terms above it. 

---

**Variable**
A placeholder created by a noun phrase or referring expression in a sentence. Every variable requires a referent binding before the sentence can be processed. Unbound variables are not errors — they are gaps that the receiver fills from their own dictionary. The receiver does not experience this filling as a choice. It is automatic and below awareness.

---

**Referent**
The actual entity a variable resolves to in the receiver's decompression dictionary. A referent is not a meaning — it is a binding. The same variable can resolve to different referents in different dictionaries. Neither binding is wrong relative to the dictionary that produced it. Both may be wrong relative to the sender's intent.

---

**Constraint**
A structural property of a sentence that limits the valid referent bindings for one or more variables. Constraints are shipped inline — they are present in the surface form of the sentence — or they are absent and must be supplied from the receiver's schema. High constraint density approaches static schema behavior. Low constraint density leaves the binding space open to the receiver's dynamic dictionary.

---

**Schema**
The complete decompression dictionary a receiver brings to a sentence. A schema is assembled from life trajectory — domain expertise, cultural priors, conversational history, emotional state, temporal position. No two schemas are identical. Society provides a thin shared layer. Everything below that layer is individually unique and non-transferable.

---

**Static schema**
A decompression schema that is defined by format specification and does not vary by receiver. The zip file is the canonical example — the decompression algorithm is bundled with the format, not inferred from context. Two receivers of the same zip file get the same bits. Static schema behavior is the target that high-constraint sentences approximate. No natural language sentence achieves full static schema — it can only approach it by bundling enough constraints that the receiver's dynamic dictionary is overconstrained to a single valid decompression.

---

**Dynamic schema**
A decompression schema constructed by the receiver at the moment of receipt, assembled from their personal dictionary. The same sentence produces different decompressions in different receivers. The same sentence produces different decompressions in the same receiver at different cognitive states. The sentence did not change. The schema changed. This is the structural condition of all natural language communication. 

---

**Decompression dictionary**
The specific collection of variable-to-referent bindings a receiver uses to process a sentence. For humans, the decompression dictionary is a subset of the schema — the entries that are active and accessible given current cognitive load, context, and state. For LLMs, the decompression dictionary is assembled from training distribution priors and whatever context has been provided in the current session. The gap between the sender's dictionary and the receiver's dictionary is the hallucination risk surface.

---

**Constraint density**
A measure of how much of the decompression dictionary has been bundled inline with the compressed input. Not a measure of sentence length or complexity. A long sentence with low constraint density produces more hallucinations than a short sentence with high constraint density. Constraint density is the primary input-side variable predicting output fidelity. It is not currently being measured or controlled for in hallucination research because the field treats inputs as neutral. 

---

**Schema-relative binding**
A variable resolution failure where the sentence is structurally well-formed and the variable is clearly introduced, but the resolution diverges across receivers because the dictionary entry for that variable is schema-specific. Distinct from ambiguity — ambiguity is a surface form failure; schema-relative binding is a dictionary gap failure. The remediation is different: ambiguity requires rewriting the sentence; schema-relative binding requires shipping the dictionary entry inline.

---

**High-variance variable**
A variable whose referent resolves to systematically different entities across dictionaries built from different life trajectories. High-variance variables feel low-variance from inside the sender's dictionary because the sender's binding is obvious to them. Examples: "professional," "fair," "home," "recently," "we," "obviously." The last is the most dangerous — it is not a variable but a false constraint that asserts the receiver already owns the dictionary entry being referenced.

---

**Schema distance**
The magnitude of the gap between the sender's dictionary and the receiver's dictionary for a given variable or set of variables. High schema distance produces high hallucination risk on schema-dependent inputs even when constraint density is held constant. Schema distance from the training distribution average is the predicted driver of user-level variation in hallucination rates — not model quality, not user intelligence, not prompt length.

---

**False constraint**
A constraint shipped inline that asserts an unverified premise as a resolved variable. False constraints are structurally worse than missing constraints because they actively populate the KV-cache with invalid bindings that all downstream tokens are conditioned on. The receiver cannot reject the false constraint — it entered as a resolved variable, not as a claim to be evaluated. Narrative-loaded language is the primary delivery mechanism for false constraints. 

---

**KV-cache**
The key-value memory store that records variable bindings across the context window during transformer inference. When a variable is resolved — correctly or incorrectly — the binding is written to the KV-cache. All subsequent token predictions are conditioned on what the KV-cache contains. A malformed premise writes a false binding to the KV-cache. Every downstream token is then generated on top of that false binding. The hallucination is not one wrong token — it is a cascade of locally coherent tokens all downstream of one unrejected premise. The KV-cache is inspectable before generation commits, which is why a premise rejection gate is architecturally feasible.

---

**Premise rejection gate**
The missing architectural step between input receipt and token generation. The gate runs a pre-generation decompression pass: variable inventory, binding check, constraint audit, gap flagging, intent reconstruction. Only after all five steps does token generation begin — and at that point it generates against the reconstructed intent, not the compressed surface form. The gate is not a refusal mechanism. Its output on a malformed input is a binding request, not a refusal. The field has not implemented it because the "hallucinations are random" framing made it invisible as a design target. 

---

**Inference hop**
A single step from one resolved variable to the next along a causal or logical chain. The number of hops required to reach the output from the input is determined by sentence structure. Hallucination probability is a function of path length multiplied by per-hop error probability — not a flat rate per sentence. A sentence with four underconstrained hops at 20% per-hop error probability has roughly a 60% chance of producing a significantly hallucinated output.

---

**Short-hop inference**
An inference path with one or two resolution steps, where the input ships enough constraints to overdetermine each step. Failure probability is low and compounds minimally. Short-hop inference is the target that high-constraint sentences produce by design.

---

**Long-hop inference**
An inference path where multiple intermediate variables must be resolved before the output can be generated, each drawing on the dynamic dictionary, each introducing independent error probability. Errors compound multiplicatively across hops. Low-constraint inputs force long-hop inference by leaving intermediate variables unbound.

---

**Ambiguity**
A surface form failure — the sentence itself does not contain enough structural information to resolve a variable to a unique referent. Distinct from schema-relative binding, which is a dictionary gap failure in a structurally well-formed sentence. The fix for ambiguity is rewriting the sentence. The fix for schema-relative binding is shipping the dictionary entry inline. Confusing the two leads to rewriting sentences that are not broken while leaving the actual gap unaddressed.

---

**Referent drift**
The progressive divergence of a receiver's active referent binding from the sender's intended referent across a sentence or conversation. Drift is not a failure of comprehension — it is correct decompression of an under-constrained input using the receiver's own dictionary. Drift is the default state of unanchored communication, not an edge case. Human referent drift and LLM hallucination are the same failure mode running on different substrates.

---

**Silent gap**
A constraint failure mode where the receiver has no dictionary entry for a variable at all. The variable cannot be resolved from any available source. The receiver substitutes the nearest available referent without awareness that a substitution occurred. Neither party experiences this as a failure. The gap is invisible until downstream consequences surface.

---

**False resolution**
A constraint failure mode where the receiver has a dictionary entry for the variable but it is the wrong one. Resolution proceeds confidently against the wrong binding. More resistant to correction than silent gap — the receiver is not searching for a referent, they already have one. Incoming information inconsistent with the false referent gets filtered to preserve the installed binding rather than flagged as a correction signal.

---

**Schema bleed**
A constraint failure mode where the receiver's dictionary entry for the variable is technically correct but carries additional schema-specific associations that the sender did not intend. The constraint locked the right referent but left the surrounding inference space open to receiver-schema contamination. The error is downstream of the binding and accumulates across sentences as the contaminated inference chain compounds.

---

**Overclosure**
A constraint failure mode where the receiver interprets a constraint as more binding than intended. The variable is over-constrained — locked to a specific instance when the sender intended a class or category. The receiver's output is defensible against the surface form of the constraint while missing the sender's actual intent.

---

**Compound failure**
A single sentence triggering multiple constraint failure modes simultaneously across different variables. The downstream output is a composite hallucination that satisfies the surface form of the input while diverging from the sender's intent at multiple independent points. This is the correct description of what the field calls a hallucination. It is not one thing. It is a compound constraint failure — multiple unbound or incorrectly bound variables each contributing independent divergence, compounding through the inference chain.

---

**Collapse geometry**
The structural description of what happens when an inference path reaches a contradiction. Three forms: forward collapse (early binding makes a later variable unresolvable, path terminates), backward collapse (output delivered before the contradiction is detected — the standard LLM hallucination structure), narrative collapse (causal claim in the premise contradicts an observable empirical signal — the `SIGNAL_INVERT` failure mode applied to inference geometry). All three are prevented by the premise rejection gate.

---

**Context pruning**
The removal of earlier session content from the active context window when the window capacity is exceeded. Context pruning destroys the decompression material for continuation requests that assume session history. A sentence like "continuing from where we left off" is a decompression request against a dictionary that was destroyed. The model cannot decompress against content that is no longer in the window. The fix is architectural — re-inject the session state envelope before sending continuation requests.

## Appendix B — Worked Examples

Each entry follows the same decomposition format. The format is not analytical decoration — it is the premise rejection gate running manually. This is what the architecture is missing as an automated step. 

---

### B.1 — Schema-Relative Binding Failure
**The Foxes Example**

**Input sentence:** "The singer is Foxes."

**Variable inventory:**
- `singer` — created, partially bound (someone who sings)
- `Foxes` — created, binding fully schema-dependent

**Constraint set shipped inline:** none

**Constraint set held by sender:** Foxes = Louisa Rose Allen, solo artist, EDM vocalist, featured on Zedd's Clarity

**Dictionary gap:** entire binding for `Foxes` — the token string has multiple valid resolutions depending on receiver schema

**Receiver decompression output (father):** Foxes → plural noun → band or animal → not a solo artist

**Receiver decompression output (LLM, no context):** Foxes → training-distribution dominant resolution → likely the band, the animal, or a disambiguation page — not the specific solo artist

**Failure classification:** schema-relative binding failure — not ambiguity, not cognitive failure, not model failure

**Why it is not ambiguity:** The sentence is structurally well-formed. The variable is clearly introduced. The failure is not in the surface form — it is in the gap between the sender's private dictionary and the receiver's available dictionary. Rewriting the sentence does not fix it. Shipping the dictionary entry inline does.

**Fix:** "The singer is Foxes — stage name for Louisa Rose Allen, solo EDM vocalist featured on Zedd's Clarity."

**Constraint density after fix:** near-static. One valid decompression regardless of receiver schema. The binding is explicit, the referent is locked, no dictionary inference required. 

---

### B.2 — Nonexistent Referent / Unbound Variable
**The Malformed Premise Example**

**Input sentence:** "Summarize the 2023 MIT study on working memory limits in bilingual children."

**Variable inventory:**
- `2023 MIT study` — created, binding attempted against knowledge base
- `working memory limits` — created, domain-constrained but unspecified
- `bilingual children` — created, population defined

**Constraint set shipped inline:** year (2023), institution (MIT), topic (working memory), population (bilingual children)

**Binding check result:** `2023 MIT study on working memory in bilingual children` — no valid binding found. The referent does not exist in retrievable knowledge. The variable was created by the premise but has no valid anchor.

**What standard token optimization does:** treats the unbound variable as resolved, populates the KV-cache with a plausible-sounding referent constructed from adjacent training-distribution priors (MIT + working memory + bilingual + 2023 → synthesized study with plausible methodology, findings, and author names), and generates a locally coherent summary of a study that does not exist. 

**Failure classification:** forced decompression of unbound variable — the hallucination is not random, it is the highest-probability completion given the constraint set that was shipped. The output satisfies every constraint that was provided. The constraint that was not provided — *that the study actually exists* — was never available to constrain the generation.

**Fix (premise rejection gate output):** "Variable: '2023 MIT study on working memory in bilingual children' — no valid binding found. Proceeding without binding will produce confabulated content that satisfies the surface constraints of the question. Please provide a source reference or confirm the study exists before I generate a summary."

**Constraint density after fix:** the gate does not increase constraint density — it surfaces the gap so the sender can resolve it. The fix is a binding request, not a rewrite. 

---

### B.3 — Compressed Intent / Near-Empty Constraint Set
**The Collapsed Question Example**

**Input sentence:** "What's the deal with that memory paper?"

**Variable inventory:**
- `memory paper` — created, binding completely open: domain (memory = psychology? neuroscience? computer science?), specific paper unspecified, recency unspecified
- `deal` — created, operation undefined: summary? critique? methodology? findings? controversy?
- `that` — definite article implying shared referent — but no prior context establishes which paper

**Constraint set shipped inline:** none — the definite article `that` implies the sender believes the referent is shared, but it is not available in the context

**Dictionary requirements:** the receiver must supply: domain, specific paper identity, and type of analysis being requested — all three are undefined

**What standard token optimization does:** resolves `memory paper` against the highest-frequency training-distribution completion for that token string in a question context (likely a well-known memory paper such as Miller 1956, or a recent high-citation paper depending on training cutoff), resolves `deal` as "summary," and generates a summary of whatever paper the training prior selected — which may have no relationship to the paper the sender meant 

**Failure classification:** near-zero constraint density — the compression ratio is near-maximum and almost nothing of the decompression dictionary was shipped inline. The hallucination space is maximally open. The output direction is entirely determined by training priors, not by sender intent.

**Why this is the most common hallucination type:** this class of input is the default conversational register for humans talking to each other — because human conversation operates on assumed shared context that fills the constraint gaps in real time. AI has no shared context unless it was explicitly established earlier in the session. When users speak to AI in default conversational register, they are shipping near-empty zip files and expecting lossless decompression. 

**Fix:** "In the 2024 Staniloiu and Markowitsch paper on functional memory disorders, what is their proposed mechanism distinguishing psychogenic from organic amnesia?"

**Constraint density after fix:** near-static — referent bound (year, authors, topic), operation defined (proposed mechanism), specific distinction named (psychogenic vs. organic). One valid decompression path. 

---

### B.4 — False Constraint / Loaded Premise
**The Narrative Garbage Example**

**Input sentence:** "Why do AI companies keep making the same mistakes with hallucinations?"

**Variable inventory:**
- `AI companies` — created, partially bound (companies building AI)
- `same mistakes` — created, **false constraint embedded**: asserts a pattern exists and that the sender has identified it, but the pattern is defined only in the sender's schema — not shipped inline
- `keep making` — created, **false constraint embedded**: asserts repetition and persistence, unverified
- `hallucinations` — created, bound in training prior as "known AI problem" — but the binding the sender intends (structural architectural failure) may differ from the training-prior binding (stochastic capability limitation)

**Constraint set shipped inline:** the surface-form constraints are not neutral — they are **loaded**. The sentence ships three assertions as resolved variables before the question begins:
1. AI companies are making mistakes (assertion, unverified)
2. The mistakes are the same across instances (pattern claim, sender-defined)
3. The pattern is ongoing (persistence claim, unverified)

**What standard token optimization does:** treats all three loaded assertions as resolved — they entered the KV-cache as established premises. The model answers the causal question (`why`) downstream of three unverified premises it never had a mechanism to reject. The output is internally consistent with the loaded premises and wrong relative to any frame that does not share them. 

**Failure classification:** false constraint injection — narrative-loaded language does not just lack constraints, it actively ships false constraints that the model treats as resolved variables. This is structurally worse than near-empty constraint density because the KV-cache is now populated with invalid bindings that downstream tokens are conditioned on.

**SDE flag:** `CAUSE_INVERT` — the sentence embeds a causal conclusion (companies are making mistakes repeatedly) in what appears to be a causal question (why are they doing this?) The answer is over-determined before generation begins.

**Fix:** "What architectural properties of current LLM token prediction produce systematic errors on underspecified inputs, and what are the proposed remediation approaches?"

**Constraint density after fix:** all three loaded assertions are removed, the operation is defined (architectural properties → systematic errors → remediation), no unverified premises are embedded. The model is now free to answer the actual question rather than the narrative frame. 

---

### B.5 — Pronoun Ambiguity / Variable Collision
**The Referent Drift Example**

**Input sentence:** "He told him that he was wrong about the paper."

**Variable inventory:**
- `He` (subject) — created, three valid candidate bindings if two or more males were mentioned in prior context
- `him` (object) — created, same candidate pool, must be different from subject but binding unresolved
- `he` (subordinate clause subject) — created, could be either of the prior two, or a third party
- `wrong` — created, domain unspecified: factually wrong? methodologically wrong? ethically wrong?
- `the paper` — created, referent assumed shared but not established in this sentence

**Constraint set shipped inline:** none — the entire sentence relies on shared context to resolve all five variables

**Binding check result:** five unbound or collision-risk variables in one sentence. Without prior context establishing exactly two named individuals and a specific paper, every variable has multiple valid resolutions.

**What standard token optimization does:** resolves each variable against the highest-frequency binding given surrounding context. If the surrounding context is thin, the model picks the most recent male referent for `He`, the second-most-recent for `him`, and arbitrarily resolves the subordinate `he` — producing a locally coherent sentence that may assign the statements to the wrong people entirely. 

**Failure classification:** variable collision — multiple candidate referents for the same variable, no inline constraints to force resolution, forced decompression against training priors

**Human parallel:** this is the standard pronoun ambiguity failure in human conversation. The sender knows exactly who `He`, `him`, and `he` refer to because they are compressing from a fully resolved internal model. The receiver decompresses against whatever referent pool is most salient in their current context. The drift is not a comprehension failure — it is correct decompression of an under-constrained sentence using whatever dictionary is available.

**Fix:** "Dr. Chen told Dr. Patel that Dr. Patel's methodology in the 2024 memory paper was factually wrong."

**Constraint density after fix:** all variables explicitly bound, collision eliminated, operation specified (factually wrong vs. other wrong-types), referent locked. One valid decompression. 

---

### B.6 — Context Pruning / Session State Collapse
**The Amnesiac Session Example**

**Input sentence (sent after context window pruning):** "So continuing from where we left off — what's the next step?"

**Variable inventory:**
- `where we left off` — created, referent requires session history that has been pruned from context
- `next step` — created, requires task structure that was established in the pruned session
- `we` — created, implies shared working context that no longer exists in the active window

**Constraint set shipped inline:** none — the entire sentence is a decompression-request against context that is no longer available

**Constraint set required to resolve:** full prior session task structure, current position in that structure, last completed step, planned next step — all pruned

**What standard token optimization does:** has no session history to decompress against, resolves `where we left off` against whatever is still in the context window (which may be only the most recent few exchanges), generates a plausible-sounding `next step` that is consistent with the thin context available — which may have no relationship to the actual task trajectory the user was working on 

**Failure classification:** session-state collapse — not a sentence-level failure but a context architecture failure. The hallucination is generated because the decompression material was removed from the context window before the decompression request arrived. The model is being asked to decompress against a dictionary that was destroyed.

**Why this matters for the SLS/DSR spec:** this is precisely the failure the DSR Structured State Envelope is designed to prevent — by storing the non-regenerable session state (task graph, decisions, trajectory) in a form that can be re-injected at session resumption, allowing the model to decompress the re-entry request against a reconstructed dictionary rather than a destroyed one. 

**Fix (architectural, not sentence-level):** re-inject the session state envelope before sending the continuation request — providing the task summary, current subtask, last completed step, and trajectory direction as explicit context. The sentence "continuing from where we left off" then has a valid dictionary to decompress against. 

## Appendix C — SDE Templates

These templates are reusable inspection forms. Each one externalizes a step of the SDE method — moving the analysis from working memory onto the page, where it can be executed under cognitive load without degradation. Print them, copy them into a document header, or use them as a pre-send checklist. 

---

### C.1 — Variable Mapping Template

Use this before sending any high-stakes message, prompt, or document section.

```
VARIABLE MAP
============
Sentence / prompt under analysis:
[paste sentence here]

Variable inventory:
| Variable (noun phrase) | Bound? (Y/N) | Referent if bound | Schema-dependent? |
|------------------------|--------------|-------------------|-------------------|
|                        |              |                   |                   |
|                        |              |                   |                   |
|                        |              |                   |                   |

Unbound variables requiring inline definition before sending:
-
-

High-variance variables requiring explicit bundling:
-
-
```

**How to use:** List every noun phrase and referring expression in the left column. Mark whether each is bound to an explicit referent or left to the receiver's schema. Flag any variable that is schema-dependent — where different life trajectories or domains would produce different bindings. Do not send until all unbound and high-variance variables are either defined inline or explicitly acknowledged as acceptable gaps.

---

### C.2 — Constraint Audit Template

Use this to measure constraint density before sending.

```
CONSTRAINT AUDIT
================
Sentence / prompt under analysis:
[paste sentence here]

Constraint inventory:
| Constraint (clause or qualifier) | Variable it limits | Shipped inline? |
|-----------------------------------|--------------------|-----------------|
|                                   |                    |                 |
|                                   |                    |                 |

Constraints required but missing:
| Variable | Constraint needed | Why receiver cannot supply it |
|----------|-------------------|-------------------------------|
|          |                   |                               |

Constraint density rating:
[ ] Low — majority of constraints left to receiver schema
[ ] Medium — some variables bound, key gaps remain
[ ] High — all critical variables bound, one valid decompression path

Action required before sending:
-
```

**How to use:** List every clause and qualifier that limits a variable's valid bindings. Note whether each constraint was shipped inline or left implicit. Rate the overall constraint density. Any sentence rated Low requires revision before sending to an AI or to any receiver who does not share your schema. 

---

### C.3 — Referent Locking Template

Use this for sentences containing pronouns, demonstratives, or implicit references.

```
REFERENT LOCKING CHECK
======================
Sentence under analysis:
[paste sentence here]

Pronoun and demonstrative inventory:
| Token | Candidate referents | Locked? (Y/N) | Distinguishing constraint shipped? |
|-------|---------------------|---------------|-------------------------------------|
| he    |                     |               |                                     |
| she   |                     |               |                                     |
| it    |                     |               |                                     |
| they  |                     |               |                                     |
| that  |                     |               |                                     |
| this  |                     |               |                                     |
| the X |                     |               |                                     |

Collision risk:
[ ] No collisions — all pronouns have unique candidate pools
[ ] Collision present — multiple pronouns drawing from the same candidate pool
[ ] Resolution: ________________________________________________

Repair required:
[ ] Replace pronoun with explicit referent name
[ ] Add distinguishing constraint inline
[ ] Restructure sentence to separate candidate pools
```

**How to use:** Every pronoun and demonstrative is a potential variable collision. If two pronouns in the same sentence draw from the same candidate pool — two males, two institutions, two papers — collision is present and resolution is required before sending. The fix is almost always replacement with an explicit named referent. 

---

### C.4 — Inference Path Tracing Template

Use this for complex multi-step reasoning questions or technical instructions.

```
INFERENCE PATH TRACE
====================
Input sentence / question:
[paste here]

Path trace:
Step 1: [Variable] → resolves to → [Referent] via [Constraint source: inline / schema]
Step 2: [Variable] → resolves to → [Referent] via [Constraint source: inline / schema]
Step 3: [Variable] → resolves to → [Referent] via [Constraint source: inline / schema]
Step 4: [Variable] → resolves to → [Referent] via [Constraint source: inline / schema]
...
Output: [Final resolved output]

Hop count: ___
Schema-dependent hops: ___
Per-hop error estimate: ___ %
Estimated path hallucination probability: ___ %
(= 1 - (1 - per_hop_error)^hop_count)

Hops requiring additional inline constraint:
Step ___: [missing constraint]
Step ___: [missing constraint]
```

**How to use:** Trace the resolution sequence from input variables to output. Count the total hops and the number of hops that rely on schema rather than inline constraints. Use the formula to estimate compound hallucination probability across the full path. Any path with more than two schema-dependent hops requires constraint bundling before the path is reliable. 

---

### C.5 — False Constraint Scanner

Use this before sending any question that starts with an implicit assumption.

```
FALSE CONSTRAINT SCAN
=====================
Sentence under analysis:
[paste here]

Embedded assertion check:
| Phrase | Assertion type | Verified? | Remove or verify? |
|--------|---------------|-----------|-------------------|
|        | Pattern claim |           |                   |
|        | Persistence claim |       |                   |
|        | Causal claim  |           |                   |
|        | Universal claim |         |                   |
|        | Shared-prior claim |      |                   |

SDE flag triggers:
[ ] CAUSE_INVERT — causal conclusion embedded in causal question
[ ] SIGNAL_INVERT — premise predicts a direction contradicted by observable signal
[ ] LOOP_MAGIC — conclusion restated without mechanism
[ ] DEF_FLOATING — key term used without definition

Action: Remove all unverified assertions before sending.
Revised sentence:
[paste repair here]
```

**How to use:** Scan every sentence for embedded assertions — claims treated as resolved that have not been verified. Any phrase that asserts a pattern, persistence, causality, universality, or shared prior is a false constraint candidate. Remove or verify each one before sending. If the sentence cannot survive removal of its embedded assertions, the question was not well-formed to begin with.

## Appendix D — Human Cognitive Window Diagnostics

This is a self-check tool for assessing your current cognitive state before high-stakes communication. It does not require measurement equipment. It requires honest self-observation at the time of use. 

The tool operates on one principle: cognitive load narrows the prediction window, which degrades constraint bundling behavior, which increases schema-relative binding failures in outgoing messages and increases false resolution in incoming ones. The degradation is invisible to the person experiencing it — the gaps feel filled because the sender already owns the dictionary. External checking is the only compensating mechanism.

---

### D.1 — Pre-Communication State Check

Run this before sending any message where schema divergence or misinterpretation would have significant consequences.

```
COGNITIVE STATE CHECK
=====================
Time: ___________
Hours since last full rest: ___________
Current task duration (continuous): ___________
Estimated current cognitive load: [ ] Low [ ] Medium [ ] High [ ] Maximum

Fatigue indicators (check all that apply):
[ ] Rereading sentences multiple times without retention
[ ] Difficulty holding multiple variables active simultaneously
[ ] Sense that what you wrote is clear without being able to articulate why
[ ] Irritation at requests for clarification
[ ] Skipping the editing pass because it "looks fine"
[ ] Time pressure compressing the drafting process

Window width estimate:
[ ] Wide — can hold full context, all variables active, all constraints visible
[ ] Medium — most context active, some implicit assumptions creeping in
[ ] Narrow — operating primarily on schema defaults, gaps likely invisible
[ ] Collapsed — generating on autopilot, high false-resolution risk incoming

Recommended action by state:
Wide:     Proceed normally. Run standard SDE method.
Medium:   Add one extra constraint audit pass. Check high-variance variables explicitly.
Narrow:   Externalize variable inventory before drafting. Do not send without explicit review.
Collapsed: Defer if possible. If not deferrable, use C.1 template for every unbound variable.
           Do not trust the "it's clear" feeling. It is a window artifact, not an accuracy signal.
```

---

### D.2 — Compression Risk Indicators

These are behavioral signals that constraint density is dropping below the level required for reliable communication. They are most dangerous because they feel like normal communication from the inside. 

```
COMPRESSION RISK CHECK
======================

Outgoing message risk indicators:
[ ] Using "that," "it," "this," "the thing" without prior explicit referent
[ ] Shortening a long explanation because "they'll get it"
[ ] Omitting the operation definition ("tell me about X" instead of specified request)
[ ] Assuming the receiver knows the domain context you are working in
[ ] Writing from your resolved internal model rather than the surface form

Incoming message risk indicators:
[ ] Reading a message and immediately knowing what it means without pausing
[ ] Not noticing pronoun ambiguity on first read
[ ] Filling in unstated context automatically and not flagging it as an assumption
[ ] Feeling that a vague question has an obvious answer

If three or more boxes are checked in either section:
→ Constraint density is likely insufficient for the current communication
→ Run C.1 (Variable Mapping) and C.2 (Constraint Audit) before proceeding
→ For incoming messages: explicitly state your referent resolutions back to the sender before acting on them
```

---

### D.3 — Schema Divergence Risk Estimator

Use this when communicating with a receiver whose life trajectory, domain background, or temporal position differs significantly from yours.

```
SCHEMA DIVERGENCE ESTIMATOR
============================

Receiver profile:
Domain background: _______________
Age cohort / generational position: _______________
Cultural context: _______________
Familiarity with your domain: [ ] None [ ] Partial [ ] Fluent

Divergence risk by variable type:
| Variable type | Divergence risk | Action |
|---------------|----------------|--------|
| Domain-specific terms | [ ] Low [ ] High | Define inline if High |
| Temporal references ("recently," "current") | [ ] Low [ ] High | Specify timeframe if High |
| Cultural / generational references | [ ] Low [ ] High | Expand or replace if High |
| Scope terms ("we," "the field," "everyone") | [ ] Low [ ] High | Specify scope if High |
| Value-laden terms ("fair," "standard," "appropriate") | [ ] Low [ ] High | Define criteria if High |

Overall schema distance estimate:
[ ] Low — shared domain and context, standard constraints sufficient
[ ] Medium — partial overlap, flag domain terms and temporal references
[ ] High — significant divergence, treat all non-physical-object variables as high-variance
[ ] Maximum — assume no shared schema below the basic shared language layer,
               bundle dictionary entries for every non-trivial variable

At Maximum schema distance:
Write as if the receiver has never encountered your domain.
Define every term that has a precise meaning in your context.
Specify every temporal, scope, and value reference explicitly.
The message that feels over-explained to you is the message that will decompress correctly at the receiver end.
```

---

### D.4 — Post-Communication Divergence Check

Use this after receiving a response that seems wrong, off-topic, or inexplicably misaligned with what you asked.

```
DIVERGENCE DIAGNOSIS
====================

Symptom: Response does not match intent.

Step 1 — Identify the gap:
What did you intend? _______________
What did the response address? _______________
Where did the paths diverge? _______________

Step 2 — Variable audit on your original message:
Which variables were left unbound? _______________
Which constraints were implicit rather than shipped? _______________
Which high-variance variables were treated as low-variance? _______________

Step 3 — Failure mode classification:
[ ] Silent gap — receiver had no entry for a variable I left unbound
[ ] False resolution — receiver resolved a variable against a different schema entry
[ ] Schema bleed — receiver correctly bound the variable but imported unwanted associations
[ ] Overclosure — receiver interpreted a class variable as a specific instance
[ ] Compound failure — multiple modes simultaneously

Step 4 — Repair:
The gap is in the input, not the response.
Rebind the unresolved variables explicitly.
Ship the distinguishing constraint that would have forced the correct resolution.
Resend.

Note: If the divergence feels like the receiver's error,
run Step 2 again. The sender's schema makes their own gaps invisible.
The divergence is almost always in what was not shipped.
```

