# V3 — Container Reordering Verification

**Status:** LOCKED
**Version:** v1.2
**Scope:** Verification specification  
**Applies to:** Existing container instances  

---

## Lock Declaration

This document is **LOCKED**.

- The transformation law defined herein is complete and authoritative.
- No further expansion, clarification, or edge-case handling shall be added to this specification.
- Any future changes require a new major version and explicit re-opening of T3.

---

## 1. Purpose

T3 defines a controlled transformation for **reordering container-level structures** while preserving all paragraph-level invariants.

T3 exists to allow **presentation-intent-driven re-sequencing of containers** when grouping or ordering intent changes, without altering paragraph identity, order, or content.

---

## 2. Definitions (Local)

- **jmaster** — Authority for paragraph identity, existence, and canonical logical paragraph order.
- **presauth / presmaster** — Authority for presentation grouping intent and allowable container sequencing constraints.
- **tmaster** — A language-specific, paragraph-identity-preserving container instance.
- **Container reordering** — Changing the sequence of authorized container blocks *above the paragraph layer* without reshaping container internals.

---

## 3. What T3 Is (and Is Not)

### T3 Is
- Structural
- Deterministic given explicit presauth constraints
- Authority-governed
- Paragraph-order preserving
- Container-sequence altering

### T3 Is Not
- Paragraph reordering
- Content editing
- Identity mutation
- Container reshaping (T1)
- Container regeneration (T2)
- Container replacement (T4)

---

## 4. Governing Authorities

| Aspect | Authority | Operational Meaning |
|------|----------|---------------------|
| Paragraph identity | jmaster | Invariant; read-only |
| Paragraph order | jmaster | Invariant; canonical |
| Container grouping | presauth | Defines grouping boundaries |
| Container sequencing | presauth | Defines permitted ordering variance within grouping boundaries |

presauth either specifies an explicit container sequence or defines grouping scopes within which reordering is permitted. T3 is deterministic relative to these constraints.

---

## 5. Allowed Operations

T3 **may**:
- Reorder sibling container blocks at explicitly authorized structural levels
- Apply container sequences specified or permitted by presauth
- Reorder containers only as whole units

T3 **may not**:
- Reorder paragraphs
- Move paragraphs between containers
- Change container nesting depth
- Operate within container internals
- Cross container types

---

## 6. Hard Invariants (Non-Negotiable)

A T3 transformation **must abort** if any invariant is violated:

1. Paragraph identity invariant
2. Paragraph cardinality invariant
3. Paragraph order invariant (global)
4. Authority invariant (jmaster immutable; presauth honored exactly)
5. Language isolation invariant
6. Traceability invariant (reordering traceable to presauth rules)

---

## 7. Inputs and Outputs

**Inputs**
- Existing container instance
- jmaster
- presauth

**Outputs**
- Container instance with reordered containers
- Paragraph layer unchanged

---

## 8. Verification Requirements

Verification is gated and MUST occur in the following order:

1. Paragraph identity check
2. Paragraph cardinality check
3. Global paragraph order check
4. Authorized container sequencing check
5. Traceability confirmation

Failure at any gate aborts T3.

---

## 9. Relationship to Other Transformations

- Assumes container free of T1-class structural drift
- Independent of T2 regeneration history
- Boundary with T1: T1 incidental reordering vs T3 intentional presentation sequencing
- Precedes T4 and T5

---

## 10. Operational Notes

- T3 operates strictly above the paragraph layer
- T3 changes sequence, not structure
- Insufficient presauth intent requires abort
