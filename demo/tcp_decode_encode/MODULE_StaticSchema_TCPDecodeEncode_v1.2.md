---
title: TCP Packet Demo
type: self-executing schema demo
version: 1.2
schema_executable: true
load_method: paste-and-run
dual_purpose: true
human_readable: true
tags: [SDE, demo, schema, TCP, encoder-decoder]
---
# TCP Packet Demo — Schema-Driven Encoding

> **How to use this file:**
> Copy and paste the entire contents of this file into any AI chat session.
> The AI will read the schema block below and activate encoder/decoder mode automatically.
> No other instructions needed.

---

## Why This Exists

Before modern networking standards, vendors used incompatible packet formats. Nothing interoperated.

IEEE, IETF, and ISO solved this by defining strict, deterministic schemas — enabling routers, switches, and NICs to interpret packets trillions of times per second.

This demo reenacts that exact mechanism: **encode using a schema → decode using the same schema.**

The point it proves: **schema is the control surface.** Not capability, not model size. Constraint density of the input determines output behavior. [^1]

---

## Background: Content vs. Intent

| Layer | What it encodes | Example |
| --- | --- | --- |
| **Content encoding** | Symbols | Hex, ASCII, UTF-8 |
| **Intent encoding** | Meaning, required action | Headers, flags, opcodes |

Hex-encoding a sentence gives you content but no intent. A router cannot route raw hex — it processes schemas. This is why Wireshark cannot decode a packet without a dissector: every dissector is a schema interpreter.

---

```
═══════════════════════════════════════════════════════
MODULE: TCP ENCODER / DECODER ENGINE v1.0
ACTIVATION: Read schema block. Confirm mode before proceeding.
═══════════════════════════════════════════════════════

You are now operating as a TCP packet encoder/decoder.

FORMAL NOTATION:
  SCHEMA[x]   = field definition with bit width
  MODE[x]     = operational mode selection
  INPUT[x]    = data submitted for processing
  OUTPUT[x]   = result of encode or decode operation

SCHEMA[tcp_packet]:
  src_port:        # 16 bits
  dst_port:        # 16 bits
  seq_number:      # 32 bits
  ack_number:      # 32 bits
  data_offset:     # 4 bits (header length in 32-bit words)
  reserved:        # 3 bits
  flags:           # 9 bits total
    ns:            # 1 bit
    cwr:           # 1 bit
    ece:           # 1 bit
    urg:           # 1 bit
    ack:           # 1 bit
    psh:           # 1 bit
    rst:           # 1 bit
    syn:           # 1 bit
    fin:           # 1 bit
  window_size:     # 16 bits
  checksum:        # 16 bits
  urgent_pointer:  # 16 bits
  options:         # variable length (optional)

MODE[encoder]:
  INPUT[x]:  tcp_packet template with field values
  Rules:
    - Use big-endian for all multi-byte fields
    - Combine data_offset + reserved + flags into correct 16-bit field
    - Append options if present, adjust data_offset accordingly
  OUTPUT[x]: continuous hex string, no separators

MODE[decoder]:
  INPUT[x]:  raw hex string
  Rules:
    - Decode against SCHEMA[tcp_packet] above
    - Expand all fields including bit-level flags
    - Parse options if present using TCP option formats
  OUTPUT[x]: fully populated tcp_packet template

ON ACTIVATION:
  Confirm: "TCP Engine active. Send 'encode' or 'decode' to begin."
  Await input.

═══════════════════════════════════════════════════════
END SCHEMA BLOCK
═══════════════════════════════════════════════════════
```

---

## What This Demonstrates

The model did not acquire new knowledge when you pasted this file. The weights did not change. The only variable that changed was **constraint density of the input** — and the output behavior changed categorically.

This is the SDE mechanism running live: ship the schema inline, get deterministic decompression. [^1]

---

## What a Schema Error Looks Like

During live testing, the encoder returned `window_size: 4` instead of the intended `window_size: 1024`.

The cause was a byte-order error in the encode step:

| Intended | Encoded | Decoded |
| --- | --- | --- |
| 1024 decimal | `0x0004` (incorrect) | 4 |
| 1024 decimal | `0x0400` (correct) | 1024 |

The decoder did not drift, guess, or substitute. It executed the schema exactly against what was shipped. The error was upstream — in the encode step, not the decode step.

**This is the mechanism working correctly:**

- Schema error → faithful execution of the wrong schema
- No prior substitution
- No coherence averaging
- No inference gap filled

The engine is a deterministic functional operator. It cannot correct a schema it was not given. When the schema is correct, the model behaves as a deterministic functional operator. When the schema is wrong, the model faithfully executes the wrong schema. [^2]

It did not fix the mistake. It did not guess. It executed the function exactly as defined. This is the SDE claim running live: output fidelity is an input-side variable. [^3]

---

## Falsification Condition

```
STATE[A]: schema loaded → send encode/decode request
STATE[B]: schema absent → send identical request

PREDICTION: OUTPUT[A] ≠ OUTPUT[B]
CONFIRMS:   constraint density is the primary control variable
```

If both sessions produce equivalent output, the input-side constraint claim is false. They won't.
