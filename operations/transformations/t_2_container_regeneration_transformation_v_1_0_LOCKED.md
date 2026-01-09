# T_2 — Container Regeneration Transformation Process (ATP)

**Status:** LOCK  
**Version:** v1.0  
**Scope:** Artifact Transformation Process (T-series)  
**Applies to:** Regeneration of existing container instances  
**Governs:** Execution of T2 (Container Regeneration) transformations  
**Defers to:** `v_2_container_regeneration_verification_v_1_2_LOCKED.md`

---

## 1. Purpose

T_2 defines the **Artifact Transformation Process (ATP)** for performing a *Container Regeneration* operation.

This document specifies **how** a lawful T2 transformation is carried out in an implementation-agnostic manner. All legality, invariants, and verification semantics are defined exclusively by the governing V-series specification.

T_2 exists to:

- Provide a controlled, authority-driven regeneration process  
- Restore trust by discarding potentially corrupted or drifted containers  
- Define atomic, all-or-nothing execution semantics  
- Bind regeneration to SSQS v2 governance  

T_2 does **not** define what is lawful. Lawfulness is defined exclusively by V_2.

---

## 2. What T_2 Is (and Is Not)

### T_2 Is

- A process specification for executing lawful T2 regeneration  
- Regenerative rather than mutative  
- Implementation-agnostic and tool-agnostic  
- Executor-agnostic (human or automated)  
- Explicitly governed by verification law  
- Suitable for invocation only via SSQS v2 Work Orders  

### T_2 Is Not

- A verification specification  
- A repair, patch, or diff-based update process  
- An execution script or automation recipe  
- A Work Order  
- A definition of invariants or legality  
- An authorization to execute  

---

## 3. Definitions (Local)

These definitions are scoped to this ATP and do not override authoritative definitions in verification specifications.

- **Container regeneration** — The act of discarding an existing container instance and emitting a new instance from authoritative sources only.  
- **Authoritative sources** — Inputs that define identity, order, structure, and language content as governed by jmaster, presauth, and language-specific sources.  
- **Execution agent** — The system or agent performing the regeneration under an SSQS v2 Work Order.  
- **Verification gate** — A required invocation of the governing verification specification at a defined checkpoint.  

---

## 4. Governing Authorities

This ATP operates under the following authority model, as enforced by verification:

| Aspect | Authority | Role in T_2 |
|------|----------|-------------|
| Paragraph existence & identity | jmaster | Defines full paragraph set and canonical order |
| Presentation intent & structure | presauth / presmaster | Defines grouping and structural realization |
| Text & language attributes | Language content source | Governs language-specific content only |
| Transformation lawfulness | V_2 | Sole authority on legality |

T_2 may not weaken, reinterpret, or bypass any authority.

---

## 5. Preconditions

Before execution of T_2 may begin, the following conditions must be satisfied:

1. Authoritative sources (jmaster, presauth, language content source) are accessible  
2. The target container type and language context are identified  
3. The governing verification spec `v_2_container_regeneration_verification_v_1_2_LOCKED.md` is available and referenced  
4. A valid SSQS v2 Work Order explicitly authorizing a T2 regeneration exists  

Failure to satisfy any precondition aborts the process before execution begins.

---

## 6. Inputs and Outputs

### Inputs

- Authoritative sources:
  - jmaster  
  - presauth / presmaster  
  - Language-specific content source  

### Outputs

- A fully regenerated container instance of the specified container type  
- Entire container emitted as a single atomic unit  
- No partial output permitted  

No prior container instance may be read during regeneration.

---

## 7. Transformation Process (Abstract)

The T_2 process proceeds through the following phases. These steps are **logical**, not executable.

### Phase 1 — Authority Validation

- Validate availability and integrity of all authoritative inputs  
- Confirm completeness of paragraph identities and language content  

Failure at this phase aborts execution.

### Phase 2 — Isolation Assurance

- Ensure regeneration process is isolated from any prior container instance  
- Confirm that no state, structure, or content is read from an existing container  

Violation of isolation requirements aborts execution.

### Phase 3 — Container Emission

- Emit a new container instance using authoritative sources only  
- Emit all paragraph identities exactly once  
- Apply presentation structure per presauth  
- Preserve language content byte-for-byte  

No inference, fallback, or partial emission is permitted.

### Phase 4 — Post-Regeneration Verification

- Invoke full V_2 verification against the regenerated container  
- Execute verification gates as defined by V_2  

Failure at any gate aborts the process.

### Phase 5 — Finalization

- If verification succeeds, designate the regenerated container as the candidate output  
- Handoff persistence responsibility to the execution model  

---

## 8. Verification Integration

Verification is mandatory and external.

T_2 requires:

- Post-regeneration verification for full compliance  

Baseline verification of a prior container is neither required nor permitted, as regeneration must not reference prior state.

T_2 does not implement verification logic and may not override verification outcomes.

---

## 9. Failure Modes and Abort Semantics

The following conditions require immediate abort:

- Any V_2 invariant violation  
- Missing or inconsistent authoritative input  
- Breach of isolation from prior container state  
- Partial container emission  

Rollback mechanics, cleanup, and reporting are execution-model concerns and must be defined by the SSQS v2 Work Order.

---

## 10. Relationship to Other Transformations

- T_2 corresponds exclusively to T2 (Container Regeneration)  
- T_2 is independent of T_1 execution order  
- T_2 explicitly excludes:
  - Reshape (T1)  
  - Reordering  
  - Replacement  
  - Split / merge  
  - Authority migration  

---

## 11. Relationship to Work Orders

T_2 may only be executed via an SSQS v2 Work Order that:

- Explicitly references this ATP  
- Explicitly references the governing V_2 specification  
- Defines atomic execution and rollback mechanics  

This ATP does not authorize execution.

---

## 12. Status

This document is **DRAFT**.

It is subject to bandy-style review and must not be treated as authoritative until explicitly LOCKED.

---

End of document
