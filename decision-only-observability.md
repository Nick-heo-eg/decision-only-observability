# Decision-only Observability

## Overview

In many systems, a request or intent is evaluated but intentionally not executed.
Examples include policy denials, safety gates, compliance holds, or approval-pending flows.

These outcomes are often operationally significant, yet they frequently disappear from traces
because no downstream work is performed.

This document outlines a minimal, execution-agnostic approach to observing
**decision-only (non-executed) operations** using existing OpenTelemetry concepts.

---

## Problem Statement

Common challenges observed across systems:

- Decision outcomes such as *deny*, *hold*, or *abort-by-policy* are not consistently represented
  in traces when no execution occurs.
- Teams encode these outcomes differently (custom attributes, status codes, ad-hoc events),
  reducing cross-tool and cross-team interoperability.
- From audit or compliance perspectives, non-executed paths may be as important as
  successful execution paths.

---

## Scope and Non-Goals

This document intentionally keeps a minimal scope.

**In scope:**
- Representing decision-only outcomes as valid observability signals
- Using existing span, event, and attribute mechanisms
- Remaining applicable across HTTP, RPC, and background jobs

**Out of scope:**
- Introducing new signal types
- Standardizing decision semantics (e.g. allow/deny enums)
- Performing or recommending automated enforcement

---

## Observability Model

### Decision vs. Execution

A decision-only operation is defined here as:

> An operation where evaluation occurs, but no side-effecting execution is performed.

Observability focuses on *recording the fact that a decision occurred*,
not on interpreting or enforcing that decision.

---

## Representation Patterns

### Spans

A span MAY represent a decision-only operation when:
- The span represents the evaluation phase
- The absence of child spans indicates no execution followed

The span status SHOULD reflect instrumentation success,
not the semantic outcome of the decision.

### Events

An event MAY be attached to a span to record:
- That a decision was reached
- That execution was intentionally skipped

Events are preferred when the decision is part of a larger operation.

### Attributes

Attributes MAY be used to record:
- The existence of alternative evaluated outcomes
- The selected outcome, without semantic interpretation
- References to external policy or authority identifiers (opaque identifiers only)

Attributes SHOULD remain domain-agnostic and avoid encoding business meaning.

---

## Interoperability Considerations

To remain interoperable across tools and domains:

- Avoid overloading span status to represent business outcomes
- Prefer descriptive attributes over inferred semantics
- Treat non-executed paths as first-class observability data

---

## Rationale

This approach preserves:

- Observability without enforcement
- Trace completeness without execution
- Responsibility attribution without decision delegation

It allows systems to answer:
> "What happened, and who decided?"

Without attempting to answer:
> "Was the decision correct?"

---

## Summary

Decision-only outcomes are valid observability targets.

By recording them using existing OpenTelemetry constructs,
systems can improve trace completeness and auditability
without introducing new signal types or decision semantics.
