# V2 — Container Regeneration Verification
**Status:** LOCKED specification
**Version:** v1.2
**Scope:** Verification specification  
**Applies to:** Regeneration of container instances from authoritative sources  

**Authoritative working directory:**
```
C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations\workingfiles\workingfiles
```

---

## Lock Declaration

This document is **LOCKED**.

- The transformation law defined herein is complete and authoritative.
- No further expansion, edge-case handling, or implementation detail shall be added to this core specification.
- Clarifications and implementation guidance MUST be captured in the companion document:
  **t_2_container_regeneration_amendments_v_1_0.md**
- Any future changes require a new major version and explicit re-opening of T2.

---

## 1. Purpose

T2 defines a controlled transformation for **regenerating a container instance** from authoritative sources.

Unlike T1, which reshapes an existing container, **T2 discards any prior container instance and re-emits a new instance from authority**, restoring trust when drift, corruption, or ambiguity is suspected.

T2 exists to:
- Reset container correctness
- Restore confidence in identity, order, and structure
- Provide a clean baseline for subsequent transformations

---

## 2. Definitions (Local)

**jmaster**  
The authoritative source for paragraph identity, existence, and canonical logical order.

**presauth / presmaster**  
The authoritative source for presentation intent, including grouping semantics and structural intent.

**Language-specific content source**  
The authoritative store of paragraph text and language-specific attributes for a given target language. Indexed by paragraph `data-id` as defined in jmaster. Governs text and language attributes only.

**tmaster**  
A language-specific, paragraph-identity-preserving container instance derived from authoritative sources.

**Container regeneration**  
The act of producing a new container instance using authoritative inputs only, without reference to any prior instance.

---

## 3. What T2 Is (and Is Not)

### T2 Is
- Regenerative, not mutative
- Deterministic given correct inputs
- Authority-driven
- Identity-preserving
- Explicitly discard-and-rebuild

### T2 Is Not
- Repair or patch
- Diff-based update
- Content editing
- Paragraph reordering
- Partial regeneration
- Authority migration

---

## 4. Governing Authorities

| Aspect | Authority | Meaning |
|------|----------|--------|
| Paragraph existence | jmaster | Defines full paragraph set |
| Paragraph identity | jmaster | Emitted exactly |
| Logical order | jmaster | Canonical sequence |
| Presentation intent | presauth | Grouping & structure intent |
| Structural realization | presauth | Permitted wrappers & markers |
| Text & language attrs | Language source | Language-specific content |

presauth does **not** authorize reordering, filtering, identity change, or content alteration.

---

## 5. Allowed Operations

- Discard existing container
- Emit new container from authority only
- Reconstruct structure per presauth
- Emit all paragraph identities exactly once
- Limited normalization (well-formedness, whitespace, authorized wrappers)

If any operation requires inference, fallback, or unauthorized change, T2 must abort.

---

## 6. Hard Invariants

- Identity invariant
- Cardinality invariant
- Order invariant
- Authority invariant
- Language isolation invariant
- Input authority validation invariant

Violation of any invariant aborts T2.

---

## 7. Inputs and Outputs

**Inputs:** jmaster, presauth, language content source  
**Outputs:** fully regenerated container instance

Entire container only. No partial regeneration.

---

## 8. Verification Requirements

Verification MUST confirm:
- All input authority validations
- Identity, cardinality, order correctness
- Implementation isolation (no prior container read during regeneration)

Failures are collected and reported together.

---

## 9. Relationship to Other Transformations

- T2 is a root transformation
- Independent of T1 execution order
- Explicitly excludes T3–T7

---

## 10. Operational Notes

- T2 restores trust by removing history
- Regeneration is all-or-nothing
- On failure, no partial output may persist
