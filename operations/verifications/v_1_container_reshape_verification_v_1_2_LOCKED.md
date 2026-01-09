# V1 — Container Reshape Verification

*Status: Locked specification*
*Scope: Verification specification*  
*Applies to: Existing container **instances***

---

## 1. Purpose

T1 defines the **safest, lowest-level transformation** in the system:

> **Reshape container structure without changing meaning, identity, or authority.**

T1 exists to allow structural hygiene, normalization, and alignment *without* semantic risk.

---

## 2. Definitions (Local)

These definitions are intentionally brief and scoped to this document.

- **jmaster** — The authoritative source for paragraph identity, existence, and logical order.
- **presauth / presmaster** — The authoritative source for presentation grouping and layout intent.
- **tmaster** — A language-specific, paragraph-identity-preserving container instance derived from authoritative sources.
- **printmaster** — An output-oriented container instance intended for print or fixed-layout products.

---

## 3. What T1 Is (and Is Not)

### T1 *Is*
- Structural only
- Deterministic
- Authority-preserving
- Reversible via regeneration
- Governed by **uniform rules with type-specific constraints**

Each container type may *narrow* T1 behavior but may not weaken its invariants.

### T1 *Is Not*
- Content editing
- Identity mutation
- Cardinality change
- Authority migration
- Creation of new container types

---

## 4. Governing Authorities

| Aspect | Authority | Operational Meaning |
|-----|-----------|---------------------|
| Paragraph existence | `jmaster` | Must be preserved exactly |
| Paragraph identity (`data-id`) | `jmaster` | Read-only, invariant |
| Logical paragraph order | `jmaster` | Must not change |
| Presentation grouping | `presauth` | High-level grouping intent; may be reshaped |
| Container structure | `presauth` | Concrete structural realization; may be reshaped |

*Note:* Presentation grouping expresses **intent**; container structure expresses **implementation**. T1 may reshape either, provided all invariants hold.

---

## 5. Allowed Operations

T1 **may**:
- Add, remove, or modify **non-semantic container elements**
- Change nesting depth of containers
- Normalize markup or attributes
- Rewrap paragraphs using different **structural arrangements** within the same container instance
- Reorder containers (not paragraphs)

**Non-semantic container elements** are structural wrappers (e.g., divs, layout containers, CSS classes, data attributes) that do **not** encode meaning, identity, order, or content.

**Explicitly disallowed**:
- Moving content between container *types* (e.g., `tmaster` → `printmaster`)

---

## 6. Hard Invariants (Non-Negotiable)

A T1 transformation **must abort** if any invariant is violated.

1. **Identity Invariant**  
   Every paragraph ID defined in `jmaster` appears **exactly once** within the container instance being transformed.

2. **Cardinality Invariant**  
   Paragraph count must match `jmaster`.

3. **Order Invariant**  
   Paragraph order must match `jmaster`.

4. **Authority Invariant**  
   No data governed by `jmaster` may be altered.

5. **Language Isolation Invariant**  
   Paragraph text, language tags (e.g., `lang`, `xml:lang`), and language-specific data attributes must be preserved byte-for-byte.

---

## 7. Inputs and Outputs

**Inputs**
- Existing container instance (e.g., `tmasterViet.html`)
- Authoritative sources (`jmaster`, `presauth`)

**Outputs**
- A reshaped container instance
- No new identities
- No semantic change

---

## 8. Verification Requirements

Verification is **gated** and must occur in the following order:

1. Scan-only verification
2. Paragraph ID match check
3. Cardinality check
4. Order check

Failure at any gate **prevents execution** or **aborts the transformation** if detected mid-process.

Rollback mechanics are an execution concern and are specified at the production-system (P-level), not in T1.

---

## 9. Rationale Examples (Non-Normative)

**Allowed** (structural reshape):

```html
<section class="layout">
  <div data-id="p12">Paragraph text</div>
</section>
```

→

```html
<div class="wrapper">
  <section class="layout">
    <div data-id="p12">Paragraph text</div>
  </section>
</div>
```

**Disallowed** (cross-type movement):
- Moving a paragraph from a `tmaster` container into a `printmaster` container

---

## 10. Relationship to Other Transformations

- T1 is a **prerequisite** for T2–T5
- T1 explicitly excludes:
  - T3 (reordering)
  - T4 (replacement)
  - T5 (split/merge)
  - T6 (authority migration)

---

## 11. Operational Notes

- T1 should be safe to automate once locked
- T1 should be boring to execute
- Repeated T1 applications should converge, not drift

---

*T1 is the foundation: once this is correct, everything else becomes safer.*

