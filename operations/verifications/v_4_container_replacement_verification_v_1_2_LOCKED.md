# V4 — Container Replacement Verification

**Status:** LOCKED
**Version:** v1.2
**Scope:** Verification specification  
**Applies to:** Existing container instances  

---

## Lock Declaration

This document is **LOCKED**.

- The transformation law defined herein is complete and authoritative.
- No further expansion, clarification, or edge-case handling shall be added to this specification.
- Any future changes require a new major version and explicit re-opening of T4.

---

## 1. Purpose

T4 defines a controlled transformation for **replacing container models** while preserving all paragraph-level invariants.

T4 exists to allow **explicit, authorized substitution of one container model for another** when presentation architecture evolves, without altering paragraph identity, order, or content.

---

## 2. Definitions (Local)

- **jmaster** — Authority for paragraph identity, existence, and canonical logical paragraph order.
- **presauth / presmaster** — Authority defining authorized container models and permitted replacement mappings.
- **tmaster** — A language-specific, paragraph-identity-preserving container instance.
- **Container model** — A template or pattern defining wrapper hierarchy, semantic markers, and layout rules for a class of containers.
- **Container replacement** — Substituting the structural wrapper hierarchy defined by one container model with another authorized model, while preserving all paragraph identities, order, and content.

---

## 3. What T4 Is (and Is Not)

### T4 Is
- Structural substitution
- Model-altering
- Deterministic given explicit authorization
- Authority-governed
- Paragraph-preserving

### T4 Is Not
- Container reshaping (T1)
- Container regeneration (T2)
- Container reordering (T3)
- Paragraph split or merge (T5)
- Authority migration

---

## 4. Governing Authorities

| Aspect | Authority | Operational Meaning |
|------|----------|---------------------|
| Paragraph identity | jmaster | Invariant; read-only |
| Paragraph order | jmaster | Invariant; canonical |
| Container models | presauth | Defines valid container models |
| Replacement eligibility | presauth | Explicitly enumerates authorized model pairs (source → target) |

presauth MUST explicitly define authorized replacement mappings. Replacement authority is expressed as a whitelist of valid model pairs.

---

## 5. Allowed Operations

T4 **may**:
- Replace one authorized container model with another
- Substitute non-semantic structural wrappers
- Apply an explicit replacement instruction validated against presauth

T4 **may not**:
- Modify paragraph text
- Modify paragraph order
- Add or remove paragraphs
- Change paragraph-container association
- Perform incidental reshaping (T1 territory)

---

## 6. Hard Invariants (Non-Negotiable)

A T4 transformation **must abort** if any invariant is violated:

1. Paragraph identity invariant
2. Paragraph cardinality invariant
3. Paragraph order invariant (global)
4. Authority invariant (jmaster immutable)
5. Language isolation invariant
6. Replacement authorization invariant (model pair must exist in presauth)

---

## 7. Inputs and Outputs

**Inputs**
- Existing container instance
- jmaster
- presauth (including authorized model pairs)
- Explicit replacement instruction (source model → target model)

**Outputs**
- Container instance emitted using the target model
- Paragraph layer unchanged

---

## 8. Verification Requirements

Verification is gated and MUST occur in the following order:

1. Paragraph identity check
2. Paragraph cardinality check
3. Global paragraph order check
4. Replacement authorization check
5. Wrapper substitution check

Failure at any gate aborts T4.

---

## 9. Relationship to Other Transformations

- Operates on containers that have passed T1 verification or been regenerated via T2
- Independent of T3 reordering history
- Boundary with T1: T1 reshapes within a model; T4 replaces the model
- Precedes T5 split/merge

---

## 10. Operational Notes

- Replacement must be explicit, not inferred
- Authorization is binary; unauthorized model pairs abort
- T4 changes models, not content
