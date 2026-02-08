# Decision-only Observability

## Position

This repository is part of the **Judgment Boundary** work:
a set of experiments and specifications focused on
*when AI systems must stop or not execute*.

See the overarching map:
→ https://github.com/Nick-heo-eg/stop-first-rag/blob/master/JUDGMENT_BOUNDARY_MANIFEST.md

---

This repository evaluates when to invoke or stop execution as a boundary problem, not as a performance competition.

---

## Non-Goals

This project does not aim to replace human or organizational judgment authority; does not provide sealed or proprietary judgment layers; does not claim legal, court-level, or regulatory admissibility; does not own, trademark, or enforce 'judgment language'. This project focuses on pre-execution judgment boundaries, STOP/HOLD/ALLOW as first-class outcomes, fail-closed behavior for unknown cases, negative proof logging, and observability-friendly reference patterns.

---

Notes on observing decision-only (non-executed) operations using existing OpenTelemetry concepts.

This repository is an informational reference and does not propose new standards or semantic conventions.

This repository intentionally avoids introducing new signals, decision semantics,
or automated enforcement.
