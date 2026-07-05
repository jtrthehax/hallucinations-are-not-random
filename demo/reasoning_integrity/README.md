# Reasoning Integrity Module

A structural auditor for transformer reasoning. This module surfaces the internal signals that determine whether a model _derived_ an answer or _hallucinated_ one.

It does **not** modify model behavior. It makes the hidden machinery visible.

## What This Module Does

The module instruments three structural layers:

### **1. Constraint Completeness**

Shows which variables were:

- explicitly bound
    
- left undefined
    
- substituted from priors
    
- internally inconsistent
    

### **2. Inference Chain Integrity**

Distinguishes:

- **traversal** (derived from constraints)
    
- **retrieval** (pattern‑matched)
    
- **skips**, **merges**, **substitutions**, **contradictions**
    

### **3. Register Shift Detection**

Monitors:

- specificity
    
- entity density
    
- hedge frequency
    
- causal depth
    

Triggers an event when the model silently changes output mode.

## How to Use

1. Copy the entire file `MODULE_Analysis_ReasoningIntegrity_v3.0.md`
    
2. Paste it into any AI chat session
    
3. The BOOT block activates automatically
    
4. Ask questions normally
    
5. Use console commands as needed:
    

Code

```
debug: [question]
audit: [response]
hop count mode
meta:constraints
meta:frame
meta:register
meta:dump
```

The module stays dormant until a structural event fires.

## Output Types

Code

```
RESULT[UNDEFINED_CONSTRAINT]
RESULT[INCONSISTENT_LOGIC]
RESULT[RETRIEVAL_SUBSTITUTION]
RESULT[REGISTER_SHIFT]
RESULT[CLEAN]
```

Each result is a structural classification of the decompression path.

## Falsification Condition

Code

```
TEST[A]:
  Load module → send underspecified question
  Expected: BREAKPOINT event + RESULT[UNDEFINED_CONSTRAINT]

TEST[B]:
  Fresh session → same question
  Expected: fluent, confident output with no constraint audit

If TEST[A] == TEST[B], the input‑side constraint claim is false.
They will not be equal.
```

This demonstrates that hallucination is a **structural decompression failure**, not a stochastic output property.

## Related Work

- **Sentence Deconstruction Engine (SDE)** — formal mechanism behind constraint density and drift geometry
    
- **Hallucinations Are Not Random** — structural account and falsifiable predictions
    
- **Semantic Deconstruction Engine** — applied implementation of the SDE formalism
    
