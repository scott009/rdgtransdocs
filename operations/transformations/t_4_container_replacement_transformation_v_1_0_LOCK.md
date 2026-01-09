# T_4 — Container Replacement Transformation Process (ATP)

**Status:** LOCK  
**Version:** v1.0  
**Scope:** Artifact Transformation Process (T-series)  
**Applies to:** Existing container instances  
**Governs:** Execution of T4 (Container Replacement) transformations  
**Defers to:** `v_4_container_replacement_verification_v_1_2_LOCKED.md`

---

## 1. Purpose

T_4 defines the **Artifact Transformation Process (ATP)** for performing a *Container Replacement* operation.

This document specifies **how** a lawful T4 transformation is carried out in an implementation-agnostic manner. All legality, invariants, and verification semantics are defined exclusively by the governing V-series specification.

T_4 exists to:

- Enable explicit, authorized substitution of one container model for another
- Support evolution of presentation architecture without content risk
- Preserve all paragraph identity, order, and content invariants
- Bind model replacement to SSQS v2 governance

T_4 does **not** define what is lawful. Lawfulness is defined exclusively by V_4.

---

## 2. What T_4 Is (and Is Not)

### T_4 Is

- A process specification for executing lawful container model replacement
- Structural and model-altering
- Deterministic given explicit authorization
- Paragraph-preserving
- Authority-governed by jmaster and presauth
- Executor-agnostic and implementation-agnostic
- Suitable for invocation only via SSQS v2 Work Orders

### T_4 Is Not

- Container reshaping (T1)
- Container regeneration (T2)
- Container reordering (T3)
- Container split or merge (T5)
- Content editing
- Authority migration
- A verification specification
- An authorization to execute

---

## 3. Definitions (Local)

These definitions are scoped to this ATP and do not override authoritative definitions in verification specifications.

- **Container model** — A template or pattern defining wrapper hierarchy, semantic markers, and layout rules for a class of containers.
- **Container replacement** — Substituting the structural wrapper hierarchy defined by one container model with another authorized model, while preserving all paragraph identities, order, and content.
- **Authorized model pair** — A source → target container model mapping explicitly enumerated by presauth.
- **Execution agent** — The system or agent performing the replacement under an SSQS v2 Work Order.
- **Verification gate** — A required invocation of the governing verification specification at a defined checkpoint.

---

## 4. Governing Authorities

This ATP operates under the following authority model, as enforced by verification:

| Aspect | Authority | Role in T_4 |
|------|----------|-------------|
| Paragraph identity | jmaster | Invariant; read-only |
| Paragraph order | jmaster | Invariant; canonical |
| Container models | presauth / presmaster | Defines valid container models |
| Replacement eligibility | presauth / presmaster | Enumerates authorized model pairs |
| Transformation lawfulness | V_4 | Sole authority on legality |

T_4 may not weaken, reinterpret, or bypass any authority.

---

## 5. Preconditions

Before execution of T_4 may begin, the following conditions must be satisfied:

1. Authoritative sources (jmaster, presauth) are accessible  
2. The target container instance is identified and within scope  
3. presauth explicitly defines the source → target model pair  
4. An explicit replacement instruction is provided  
5. The governing verification spec `v_4_container_replacement_verification_v_1_2_LOCKED.md` is available and referenced  
6. A valid SSQS v2 Work Order explicitly authorizing a T4 transformation exists  

Failure to satisfy any precondition aborts the process before execution begins.

---

## 6. Inputs and Outputs

### Inputs

- Existing container instance  
- Authoritative sources:
  - jmaster  
  - presauth / presmaster (including authorized model pairs)  
- Explicit replacement instruction (source model → target model)

### Outputs

- Container instance emitted using the target container model  
- Paragraph layer unchanged  
- No incidental reshaping or reordering  

Partial or speculative outputs are not permitted to persist.

---

## 7. Transformation Process (Abstract)

The T_4 process proceeds through the following phases. These steps are **logical**, not executable.

### Phase 1 — Baseline Verification

- Invoke V_4 verification against the input container
- Confirm paragraph identity, cardinality, and global order invariants

Failure at this phase aborts execution.

### Phase 2 — Replacement Authorization Resolution

- Resolve the source container model of the input container
- Validate the source → target model pair against presauth
- Reject any replacement not explicitly authorized

Unauthorized or ambiguous model mappings abort execution.

### Phase 3 — Model Substitution

- Substitute the structural wrapper hierarchy defined by the target model
- Preserve paragraph identities, order, and content exactly
- Maintain paragraph-to-container association

No incidental reshaping, reordering, or inference is permitted.

### Phase 4 — Post-Replacement Verification

- Invoke full V_4 verification against the replaced container
- Execute verification gates in the required order:
  - Paragraph identity
  - Paragraph cardinality
  - Global paragraph order
  - Replacement authorization
  - Wrapper substitution correctness

Failure at any gate aborts the process.

### Phase 5 — Finalization

- If verification succeeds, designate the replaced container as the candidate output
- Handoff persistence responsibility to the execution model

---

## 8. Verification Integration

Verification is mandatory and external.

T_4 requires:

- Baseline verification prior to replacement
- Post-replacement verification for full compliance

T_4 does not implement verification logic and may not override verification outcomes.

---

## 9. Failure Modes and Abort Semantics

The following conditions require immediate abort:

- Any V_4 invariant violation  
- Unauthorized or missing model replacement mapping  
- Paragraph-level mutation or movement  
- Incidental reshaping or reordering  

Rollback mechanics, cleanup, and reporting are execution-model concerns and must be defined by the SSQS v2 Work Order.

---

## 10. Relationship to Other Transformations

- T_4 corresponds exclusively to T4 (Container Replacement)  
- Operates on containers that have passed T1 verification or been regenerated via T2  
- Independent of T3 reordering history  
- Boundary with T1: T1 reshapes within a model; T4 replaces the model  
- Precedes T5 (Split / Merge)

---

## 11. Relationship to Work Orders

T_4 may only be executed via an SSQS v2 Work Order that:

- Explicitly references this ATP  
- Explicitly references the governing V_4 specification  
- Defines execution and rollback mechanics  

This ATP does not authorize execution.

---

## 12. Status

This document is **DRAFT**.

It is subject to bandy-style review and must not be treated as authoritative until explicitly LOCKED.

---

End of document
