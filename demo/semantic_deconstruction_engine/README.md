# Semantic Deconstruction Engine (SDE)

A structural analysis module that treats text as a compression artifact and evaluates arguments at the mechanistic layer. The SDE is not a language model. It is a meaning compiler. Its stance is adversarial by default: no term is assumed stable, no mechanism is assumed valid, and no inference is accepted without an explicit bridge.

The SDE runs a 12‑stage pipeline on every input:

1. **Meta Check** — detect structural counter‑moves in responses to prior SDE output  
2. **Load‑Bearing Claim Extraction** — enumerate all claims the argument depends on  
3. **Definition Scan** — test stability of every load‑bearing term  
4. **Constraint Scan** — identify missing, inverted, or decayed constraints  
5. **Mechanism Scan** — verify causal operators have explicit mechanisms  
6. **Causal Chain Scan** — detect breaks, teleports, and direction inversions  
7. **Inference Scan** — identify literal‑to‑narrative gaps and reader‑supplied load  
8. **Loop & Drift Scan** — detect circularity, self‑sealing structures, and referent drift  
9. **Contradiction Check** — identify mutually exclusive load‑bearing claims  
10. **Compound Check** — detect multi‑flag structural compounds  
11. **Compression Score** — deductive scoring from baseline 100  
12. **Hallucination Risk Rating** — structural risk classification

The SDE does not fill gaps, infer intent, or repair missing structure.  
It names the gaps, classifies the failures, and outputs the structural pattern.

## Flag Registry

The module includes a full flag registry covering:

- **DEFINITION** — undefined, unstable, floating, mixed terms  
- **CONSTRAINT** — missing, inverted, decayed constraints  
- **MECHANISM** — absent, partial, metaphor‑substituted mechanisms  
- **CAUSAL** — breaks, teleports, inversions  
- **INFERENCE** — gaps and reader‑supplied load  
- **LOOP** — circular and self‑sealing structures  
- **DRIFT** — referent and frame drift  
- **SIGNAL** — prediction vs observable signal mismatch  
- **META** — structural counter‑moves in responses to SDE output

Each flag carries a severity class and a scoring deduction.

## How to Use

1. Copy the entire module file  
2. Paste it into any AI session  
3. The BOOT block activates automatically  
4. Provide text for analysis  
5. The SDE runs the full pipeline and outputs:

- active flags  
- deduction table  
- compression score  
- hallucination risk rating  
- structural synthesis

The SDE does not modify the model’s behavior.  
It exposes the structure the model normally hides.

## Falsification Condition

If a text with missing definitions, inverted constraints, absent mechanisms, or inference gaps produces a **CLEAN** result under SDE analysis, the SDE formalism is incorrect.

This has not occurred in any regression test.

## Related

- **Sentence Deconstruction Engine (SDE)** — full mechanism and taxonomy  
- **Hallucinations Are Not Random** — structural account and predictions  
- **Reasoning Integrity Module** — constraint and inference auditor  
