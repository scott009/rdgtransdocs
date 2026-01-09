# V5 — Container Split / Merge Verification

**Status:** LOCKED
**Version:** v1.2
**Scope:** Verification specification  
**Applies to:** Existing container instances  

---

## 1. Purpose

T5 defines controlled transformations for **splitting** and **merging containers** while preserving all paragraph-level invariants.

T5 exists to allow **structural refactoring of container boundaries** when presentation intent requires finer or coarser grouping, without altering paragraph identity, order, or content.

---

## 2. Definitions (Local)

- **jmaster** — Authority for paragraph identity, existence, and canonical logical paragraph order.
- **presauth / presmaster** — Authority for presentation grouping intent and permitted container boundary changes.
- **tmaster** — A language-specific, paragraph-identity-preserving container instance.
- **Container model** — The structural wrapper pattern governing a container instance (as defined/used in T4).
- **Container type** — The broad container family (e.g., `tmaster`, `printmaster`).
- **Adjacent containers** — Two or more containers at the **same structural level** (siblings under the same parent) that are **sequentially positioned** within that parent.
- **Container split** — Dividing a single authorized container into two or more authorized containers by introducing new container boundaries.
- **Container merge** — Combining two or more **adjacent containers** into a single authorized container by removing a boundary between them.

---

## 3. What T5 Is (and Is Not)

### T5 Is
- Structural boundary modification
- Deterministic given explicit authorization
- Authority-governed
- Paragraph-preserving

### T5 Is Not
- Paragraph split or merge
- Content editing
- Paragraph reordering
- Container reshaping (T1)
- Container regeneration (T2)
- Container reordering (T3)
- Container replacement (T4)

---

## 4. Governing Authorities

| Aspect | Authority | Operational Meaning |
|------|----------|---------------------|
| Paragraph identity | jmaster | Invariant; read-only |
| Paragraph order | jmaster | Invariant; canonical |
| Container boundaries | presauth | Defines permitted split/merge boundaries |
| Split / merge eligibility | presauth | Explicitly authorizes allowed boundary changes |

presauth MUST explicitly authorize all split and merge operations.

---

## 5. Allowed Operations

T5 **may**:
- Split a container at authorized boundary points
- Merge **adjacent containers** where explicitly authorized
- Introduce or remove **container boundaries only**, not content

T5 **may not**:
- Split or merge paragraphs
- Reassign paragraph identity
- Change paragraph order
- Cross container types (e.g., `tmaster` → `printmaster`). Cross-type changes are handled exclusively by T4; T5 MUST abort if a split or merge would require a cross-type change.
- Infer or guess split/merge points

---

## 6. Hard Invariants (Non-Negotiable)

A T5 transformation **must abort** if any invariant is violated:

1. **Paragraph identity invariant** — All paragraph IDs from jmaster appear exactly once.
2. **Paragraph cardinality invariant** — Paragraph count matches jmaster.
3. **Paragraph order invariant** — Canonical paragraph order is preserved globally.
4. **Authority invariant** — No data governed by jmaster may be altered; presauth boundary authority must be honored exactly.
5. **Language isolation invariant** — Paragraph text and language attributes remain byte-for-byte identical.
6. **Boundary authorization invariant** — All split/merge operations performed are explicitly authorized by presauth.

---

## 7. Inputs and Outputs

**Inputs**
- Existing container instance
- jmaster
- presauth (including authorized boundary rules)
- Explicit split/merge instruction

**Explicit split/merge instruction (normative):**  
A deterministic specification of boundary operations that:
- References an authorized presauth rule (or authorized boundary description), and
- Identifies the target boundary using paragraph IDs (e.g., split after paragraph `pX`, merge containers spanning a continuous paragraph-id range), and
- Specifies operation ordering if multiple operations are requested.

**Outputs**
- Container instance with modified container boundaries
- Paragraph layer unchanged

---

## 8. Verification Requirements

Verification is gated and MUST occur in the following order:

1. Paragraph identity check
2. Paragraph cardinality check
3. Global paragraph order check
4. Boundary authorization check:
   - Confirm all split/merge operations are authorized by presauth
5. Container-type / model consistency check:
   - Confirm no operation crosses container type boundaries
   - Confirm splits produce containers of the same container model as the source

Failure at any gate aborts T5. No partial acceptance is permitted.

---

## 9. Relationship to Other Transformations

- Operates on containers that have passed T1 verification or been regenerated via T2
- Independent of T3 reordering history
- Boundary with T4:
  - T4 changes the container model while preserving boundaries
  - T5 changes boundaries while preserving the container model/type of resulting containers

---

## 10. Operational Notes

- Split and merge operations must be explicit, not inferred.
- Multiple splits and merges may occur in a single T5 execution if all are authorized.
- **Execution model:** T5 applies operations in the order specified by the explicit instruction. All operations are treated as a single atomic transformation: if any operation becomes invalid or any gate fails, T5 aborts.
