Artifact Transformation Processes (T-Series)
===========================================

## Purpose

This directory contains the authoritative **Artifact Transformation Process (ATP)** specifications for the **T-series transformations (T1–T5)**.

These documents define **how** lawful transformations are carried out — not what is lawful.

They function as the **executive layer** of the system:

- sequencing transformation steps
- enforcing authority boundaries
- defining abort semantics
- binding execution to SSQS v2 governance
- coordinating verification without redefining it

Nothing in this directory defines legality, invariants, or verification semantics.

---

## What These Documents Are

Files in this directory:

- Define **how to perform** authorized transformations
- Specify inputs, outputs, sequencing, and checkpoints
- Reference governing **V-series verification specs**
- Enforce authority boundaries (jmaster, presauth, language sources)
- Define failure modes and abort semantics
- Bind transformations to **SSQS v2 Work Orders**
- Are **implementation-agnostic** and **executor-agnostic**
- Are authoritative once **LOCKED**

They answer questions like:

- How is this transformation executed safely?
- What must be checked before, during, and after execution?
- When must execution abort?
- How does this transformation integrate with Work Orders?
- How is verification invoked and enforced?

---

## What These Documents Are Not

This directory does **not** contain:

- Verification semantics or invariants
- Execution code, scripts, or automation
- Tool-specific instructions
- Work Orders
- Authorization decisions
- Governance rules
- Path, storage, or runtime assumptions
- Project narrative or onboarding material

Those concerns belong to other layers.

---

## Relationship to Verification (V-Series)

Transformation processes are **subordinate to verification specifications**.

- **V-series specs** define what is lawful
- **T-series specs** define how lawful transformations are executed
- T-series documents may **reference** V-series specs
- T-series documents may **not redefine, weaken, or reinterpret** verification rules

Verification is:

- Required
- External
- Gated
- Authoritative

If verification fails, transformation **must abort**.

This separation is intentional.

> The judiciary defines what is lawful.  
> The executive defines how work is carried out.  
> Neither implements the other.

---

## Transformation Series Overview

| Transformation | Scope | Purpose |
|---------------|------|---------|
| **T1 — Container Reshape** | Structure | Structural hygiene without semantic change |
| **T2 — Container Regeneration** | Whole container | Discard-and-rebuild from authority |
| **T3 — Container Reordering** | Container sequence | Presentation-intent-driven sequencing |
| **T4 — Container Replacement** | Container model | Authorized model substitution |
| **T5 — Container Split / Merge** | Container boundaries | Structural regrouping |

Each T-series ATP:

- Applies only to **existing container instances**
- Preserves **paragraph identity, order, and content**
- Requires **explicit authority**
- Executes as a **single atomic operation**

---

## Relationship to Work Orders (SSQS v2)

T-series ATPs **do not authorize execution**.

Execution is permitted **only** via a valid **SSQS v2 Work Order** that:

- Explicitly references the applicable T-series ATP
- Explicitly references the governing V-series verification spec
- Defines execution, rollback, and reporting mechanics
- Assigns responsibilities to Sonnet and Haiku correctly

T-series documents:

- Define *what the execution must do*
- Define *when execution must abort*
- Do **not** execute or schedule work

---

## Authority Boundaries

All T-series transformations operate under strict authority boundaries:

- **jmaster** — paragraph identity, existence, and order (immutable)
- **presauth / presmaster** — presentation intent, structure, models, and boundaries
- **Language sources** — language-specific content only
- **V-series specs** — sole authority on lawfulness

T-series ATPs may **enforce** these authorities, but may not redefine them.

---

## Atomicity and Abort Semantics

All T-series transformations are **atomic**:

- Partial output must not persist
- Multi-step operations are treated as a single unit
- Any invariant violation requires immediate abort
- Rollback and cleanup are execution-model concerns

Transformation processes must **fail fast** and **fail safely**.

---

## Locked Specifications

Only files explicitly marked as **LOCKED** are authoritative.

Locked transformation processes:

- `t_1_container_reshape_transformation_*.md`
- `t_2_container_regeneration_transformation_*.md`
- `t_3_container_reordering_transformation_*.md`
- `t_4_container_replacement_transformation_*.md`
- `t_5_container_split_merge_transformation_*.md`

Drafts, prior versions, and working copies are retained for auditability but must not be used for execution or governance decisions.

---

## Change Control

- All changes require a **bandy-and-lock** process
- New versions must increment version numbers
- Prior versions must be preserved
- Semantic drift without explicit lock is prohibited

---

## Scope Boundary

These specifications apply only to **existing container instances**.

They do **not** cover:

- Creation of new container or product-layer types
- Authority migration
- Product-level composition
- Execution infrastructure

---

## Rationale

Transformation processes exist to make execution:

- Boring
- Predictable
- Auditable
- Safe
- Governed

Once T-series ATPs are locked, execution becomes mechanical — and that is the goal.

---

End of document
