# Hallucinations Are Not Random
[![DOI](https://zenodo.org/badge/1290349582.svg)](https://doi.org/10.5281/zenodo.21210606)

A structural account of why LLM hallucinations are deterministic, predictable, and fixable at the input layer — and why the field's stochastic framing is falsified by the data it already has.

**The one-line proof:**

> If hallucinations were random, constraint density would not predict hallucination rate. It does. Therefore hallucinations are not random. QED.

---

## External Confirmation

Anthropic published empirical findings on 2026-07-06 describing a structured internal reasoning region (workspace manifold) whose activation varies with input context. This is downstream confirmation of the driver-induced regulatory state mechanism modeled in this framework — published here prior to their paper.

**The interpretive gap:** Anthropic averaged across users and attributed variance to model properties. The per-user, intraday-variable structure was erased before analysis.

→ [EC-001: Anthropic Workspace Manifold Paper — full response and remaining predictions](responses/2026-07-07-anthropic-workspace.md#entry-ec-001--anthropic-workspace-manifold-paper-2026-07-06)

---

## Repository Contents

| File | Description |
| --- | --- |
| `SDE_paper.md` | Full mechanism, failure taxonomy, and human-scale demonstrations |
| `PREDICTIONS.md` | Ten falsifiable structural predictions — any one decides the question |
| `COUNTERARGUMENTS.md` | The field's three defenses and why each collapses on contact |
| `COUNTER.md` | Log of responses, replications, and refutations |
| `responses/` | Dated responses to external empirical work confirming framework predictions |

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
3. **Read** `COUNTERARGUMENTS.md` — the structural collapse of the field's defenses.
4. **Check** `responses/` — external empirical papers landing on predictions already made here.
5. **Explore the demos** — each one is a mechanistic instantiation of an SDE invariant.
6. **Return to the paper** — the mechanism will be visible at a lower inference layer.

## Citation

Robinson, J. (2026). _Hallucinations Are Not Random._ Zenodo. https://doi.org/10.5281/zenodo.21210606

## License

CC BY 4.0 — Joel Robinson
