# Hallucinations Are Not Random

A structural account of why LLM hallucinations are deterministic, predictable, and fixable at the input layer — and why the field’s stochastic framing is falsified by the data it already has.

**The one-line proof:**

> If hallucinations were random, constraint density would not predict hallucination rate. It does. Therefore hallucinations are not random. QED.

## Repository Contents

|File|Description|
|---|---|
|`SDE_paper.md`|Full mechanism, failure taxonomy, and human-scale demonstrations|
|`PREDICTIONS.md`|Ten falsifiable structural predictions — any one decides the question|
|`COUNTERARGUMENTS.md`|The field’s three defenses and why each collapses on contact|
|`COUNTER.md`|Log of responses, replications, and refutations (empty until publication)|

## Demonstrations

This paper is accompanied by three mechanistic demos that instantiate the SDE invariants:

- **TCP Decode/Encode** — static-schema decompression (zero drift)
    
- **Reasoning Integrity Module** — constraint-density enforcement and premise-rejection
    
- **Semantic Deconstruction Engine** — full operationalization of variable creation, constraint extraction, and drift prediction
    

These demos are not examples — they are structural proofs of the mechanism.

## Applied Implementation

The Semantic Deconstruction Engine (SDE) is the applied tool built on this argument:

**SEMANTIC-DECONSTRUCTION-ENGINE**

## How to Read This Repo

1. **Start with** `SDE_paper.md` — the full mechanism and taxonomy.
    
2. **Read** `PREDICTIONS.md` — the falsifiable tests that decide the question.
    
3. **Read** `COUNTERARGUMENTS.md` — the structural collapse of the field’s defenses.
    
4. **Explore the demos** — each one is a mechanistic instantiation of an SDE invariant.
    
5. **Return to the paper** — the mechanism will be visible at a lower inference layer.
    

## Citation

Robinson, J. (2026). _Hallucinations Are Not Random._ Zenodo. https://doi.org/[pending]

## License

CC BY 4.0 — Joel Robinson

If you want, I can also generate:

- **A version with a DOI badge placeholder**
    
- **A version formatted for arXiv**
    
- **A version formatted for GitHub Pages**
    

Just pick the one you want.