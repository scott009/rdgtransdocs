# T_1 — Container Reshape Transformation Process (ATP)

**Status:** LOCKED  \
**Version:** v1.1  \
**Scope:** Artifact Transformation Process (T-series)  \
**Applies to:** Existing container instances only  \
**Governs:** Execution of T1 (Container Reshape) transformations  \
**Defers to:** `v_1_container_reshape_verification_v_1_2_LOCKED.md`

---

## 1. Purpose

T_1 defines the **Artifact Transformation Process (ATP)** for performing a *Container Reshape* operation.

This document specifies **how** a lawful T1 transformation is carried out, in an implementation-agnostic manner, while deferring all legality, invariants, and verification semantics to the governing V-series specification.

T_1 exists to:

- Provide a safe, repeatable executive process for structural container reshaping
- Ensure authority-preserving behavior
- Define sequencing, checkpoints, and abort expectations
- Bind execution to SSQS v2 governance

T_1 does **not** define what is lawful. Lawfulness is defined exclusively by V_1.

---

## 2. What T_1 Is (and Is Not)

### T_1 Is

- A process specification for executing lawful T1 transformations
- Implementation-agnostic and tool-agnostic
- Executor-agnostic (human or automated)
- Explicitly governed by verification law
- Suitable for invocation only via SSQS v2 Work Orders

### T_1 Is Not

- A verification specification
- An execution script or automation recipe
- A Work Order
- A definition of invariants or legality
- An authorization to execute

---

## 3. Definitions (Local)

These definitions are scoped to this ATP and do not override authoritative definitions in verification specifications.

- **Container instance** — A concrete realization of a container type (e.g., tmaster) containing paragraphs indexed by `data-id`.
- **Reshape operation** — A structural modification of a container instance that does not alter meaning, identity, authority, or order.
- **Execution agent** — The system or agent performing the transformation under an SSQS v2 Work Order.
- **Verification gate** — A required invocation of the governing verification specification at a defined checkpoint.

---

## 4. Governing Authorities

This ATP operates under the following authority model, as enforced by verification:

| Aspect | Authority | Role in T_1 |
|------|----------|-------------|
| Paragraph identity & order | jmaster | Read-only authority; must be preserved |
| Presentation intent & structure | presauth / presmaster | Defines allowable structural realizations |
| Transformation lawfulness | V_1 | Sole authority on legality |

T_1 may not weaken, reinterpret, or bypass any authority.

---

## 5. Preconditions

Before execution of T_1 may begin, the following conditions must be satisfied:

1. Authoritative sources (jmaster, presauth) are accessible
2. The target container instance is identified and within scope
3. The governing verification spec `v_1_container_reshape_verification_v_1_2_LOCKED.md` is available and referenced
4. A valid SSQS v2 Work Order explicitly authorizing a T1 transformation exists

Failure to satisfy any precondition aborts the process before execution begins.

---

## 6. Inputs and Outputs

### Inputs

- Existing container instance (e.g., `tmasterViet.html`)
- Authoritative sources:
  - jmaster
  - presauth / presmaster

### Outputs

- A reshaped container instance of the **same container type**
- No new identities
- No semantic changes

Partial or speculative outputs are not permitted to persist.

---

## 7. Transformation Process (Abstract)

The T_1 process proceeds through the following phases. These steps are **logical**, not executable.

### Phase 1 — Baseline Verification

- Invoke V_1 verification in scan-only mode against the input container
- Confirm that the container satisfies all hard invariants prior to transformation

Failure at this phase aborts execution.

### Phase 2 — Structural Planning

- Identify intended structural changes permitted under T1
- Confirm that planned changes are structural-only and container-local
- Reject any plan requiring:
  - Identity mutation
  - Paragraph movement
  - Cross-container transfer

### Phase 3 — Structural Reshape

- Apply structural changes to container elements only
- Preserve paragraph text, identity, order, and language attributes byte-for-byte
- No semantic inference, fallback, or auto-correction is permitted

### Phase 4 — Post-Transformation Verification

- Invoke full V_1 verification against the transformed container
- Execute verification gates in the required order

Failure at any gate aborts the process.

### Phase 5 — Finalization

- If verification succeeds, designate the transformed container as the candidate output
- Handoff persistence responsibility to the execution model

---

## 8. Verification Integration

Verification is mandatory and external.

T_1 requires:

- Pre-transformation verification (baseline)
- Post-transformation verification (compliance)

T_1 does not implement verification logic and may not override verification outcomes.

---

## 9. Failure Modes and Abort Semantics

The following conditions require immediate abort:

- Any V_1 invariant violation
- Loss of authoritative source access
- Detection of semantic or identity mutation
- Partial output persistence

Rollback mechanics, cleanup, and reporting are execution-model concerns and must be defined by the SSQS v2 Work Order.

---

## 10. Relationship to Other Transformations

- T_1 corresponds exclusively to T1 (Container Reshape)
- T_1 is a prerequisite process for transformations governed by T2–T5
- T_1 explicitly excludes:
  - Reordering
  - Replacement
  - Split / merge
  - Authority migration

---

## 11. Relationship to Work Orders

T_1 may only be executed via an SSQS v2 Work Order that:

- Explicitly references this ATP
- Explicitly references the governing V_1 specification
- Defines execution and rollback mechanics

This ATP does not authorize execution.

---

## 12. Status

This document is **LOCKED**.

It has completed bandy-style review and is authoritative for T_1 transformation process execution.

---

End of document