# T_5 — Container Split / Merge Transformation Process (ATP)

**Status:** DRAFT  
**Version:** v1.0  
**Scope:** Artifact Transformation Process (T-series)  
**Applies to:** Existing container instances  
**Governs:** Execution of T5 (Container Split / Merge) transformations  
**Defers to:** `v_5_container_split_merge_verification_v_1_2_LOCKED.md`

---

## 1. Purpose

T_5 defines the **Artifact Transformation Process (ATP)** for performing *Container Split* and *Container Merge* operations.

This document specifies **how** a lawful T5 transformation is carried out in an implementation-agnostic manner. All legality, invariants, and verification semantics are defined exclusively by the governing V-series specification.

T_5 exists to:

- Enable explicit, authorized modification of container boundaries
- Support finer or coarser presentation grouping without content risk
- Preserve all paragraph identity, order, and language invariants
- Ensure split / merge operations are deterministic, traceable, and atomic
- Bind boundary changes to SSQS v2 governance

T_5 does **not** define what is lawful. Lawfulness is defined exclusively by V_5.

---

## 2. What T_5 Is (and Is Not)

### T_5 Is

- A process specification for executing lawful container split and merge operations
- Structural boundary modification
- Deterministic given explicit authorization
- Paragraph-preserving
- Authority-governed by jmaster and presauth
- Executor-agnostic and implementation-agnostic
- Suitable for invocation only via SSQS v2 Work Orders

### T_5 Is Not

- Paragraph split or merge
- Content editing
- Paragraph reordering
- Container reshaping (T1)
- Container regeneration (T2)
- Container reordering (T3)
- Container replacement (T4)
- Authority migration
- A verification specification
- An authorization to execute

---

## 3. Definitions (Local)

These definitions are scoped to this ATP and do not override authoritative definitions in verification specifications.

- **Container split** — Dividing a single authorized container into two or more authorized containers by introducing new container boundaries.
- **Container merge** — Combining two or more adjacent containers into a single authorized container by removing a boundary between them.
- **Adjacent containers** — Containers at the same structural level that are sequentially positioned under the same parent.
- **Explicit split / merge instruction** — A deterministic specification describing authorized boundary operations, referencing presauth rules and paragraph IDs.
- **Execution agent** — The system or agent performing the split / merge under an SSQS v2 Work Order.
- **Verification gate** — A required invocation of the governing verification specification at a defined checkpoint.

---

## 4. Governing Authorities

This ATP operates under the following authority model, as enforced by verification:

| Aspect | Authority | Role in T_5 |
|------|----------|-------------|
| Paragraph identity | jmaster | Invariant; read-only |
| Paragraph order | jmaster | Invariant; canonical |
| Container boundaries | presauth / presmaster | Defines permitted boundary changes |
| Split / merge eligibility | presauth / presmaster | Explicitly authorizes boundary operations |
| Transformation lawfulness | V_5 | Sole authority on legality |

T_5 may not weaken, reinterpret, or bypass any authority.

---

## 5. Preconditions

Before execution of T_5 may begin, the following conditions must be satisfied:

1. Authoritative sources (jmaster, presauth) are accessible  
2. The target container instance is identified and within scope  
3. presauth explicitly authorizes all requested split / merge boundaries  
4. An explicit split / merge instruction is provided, including operation ordering  
5. The governing verification spec `v_5_container_split_merge_verification_v_1_2_LOCKED.md` is available and referenced  
6. A valid SSQS v2 Work Order explicitly authorizing a T5 transformation exists  

Failure to satisfy any precondition aborts the process before execution begins.

---

## 6. Inputs and Outputs

### Inputs

- Existing container instance  
- Authoritative sources:
  - jmaster  
  - presauth / presmaster (including boundary authorization rules)  
- Explicit split / merge instruction

### Outputs

- Container instance with modified container boundaries  
- Paragraph layer unchanged  
- All resulting containers preserve the original container type and model  

Partial or speculative outputs are not permitted to persist.

---

## 7. Transformation Process (Abstract)

The T_5 process proceeds through the following phases. These steps are **logical**, not executable.

### Phase 1 — Baseline Verification

- Invoke V_5 verification against the input container
- Confirm paragraph identity, cardinality, and global order invariants

Failure at this phase aborts execution.

### Phase 2 — Boundary Authorization Resolution

- Resolve all requested split and merge operations
- Validate each operation against presauth authorization rules
- Confirm all operations are explicitly authorized and unambiguous

Unauthorized or inferred boundary operations abort execution.

### Phase 3 — Boundary Modification

- Apply split operations by introducing authorized container boundaries
- Apply merge operations by removing authorized boundaries between adjacent containers
- Preserve paragraph identities, order, and content exactly
- Maintain container type and model consistency across all resulting containers

No inference, reshaping, reordering, or cross-type changes are permitted.

### Phase 4 — Post-Transformation Verification

- Invoke full V_5 verification against the modified container
- Execute verification gates in the required order:
  - Paragraph identity
  - Paragraph cardinality
  - Global paragraph order
  - Boundary authorization
  - Container type and model consistency

Failure at any gate aborts the process.

### Phase 5 — Finalization

- If verification succeeds, designate the modified container as the candidate output
- Handoff persistence responsibility to the execution model

All split and merge operations are treated as a single atomic transformation.

---

## 8. Verification Integration

Verification is mandatory and external.

T_5 requires:

- Baseline verification prior to boundary modification
- Post-transformation verification for full compliance

T_5 does not implement verification logic and may not override verification outcomes.

---

## 9. Failure Modes and Abort Semantics

The following conditions require immediate abort:

- Any V_5 invariant violation  
- Unauthorized or inferred split / merge boundary  
- Paragraph-level mutation or movement  
- Cross-container-type or cross-model operation  
- Partial application of a multi-step split / merge instruction  

Rollback mechanics, cleanup, and reporting are execution-model concerns and must be defined by the SSQS v2 Work Order.

---

## 10. Relationship to Other Transformations

- T_5 corresponds exclusively to T5 (Container Split / Merge)  
- Operates on containers that have passed T1 verification or been regenerated via T2  
- Independent of T3 reordering history  
- Boundary with T4:
  - T4 changes container models while preserving boundaries  
  - T5 changes boundaries while preserving container models and types  

---

## 11. Relationship to Work Orders

T_5 may only be executed via an SSQS v2 Work Order that:

- Explicitly references this ATP  
- Explicitly references the governing V_5 specification  
- Defines atomic execution and rollback mechanics  

This ATP does not authorize execution.

---

## 12. Status

This document is **DRAFT**.

It is subject to bandy-style review and must not be treated as authoritative until explicitly LOCKED.

---

End of document
