# Verification Specifications (V-Series)

## Purpose

This directory contains the **authoritative verification specifications** for the V-series verifications (V1–V5).

These documents define **what verification means** for container transformations, not how verification is executed.

They function as the **judicial layer** of the system:
- establishing lawful operations
- defining invariants
- constraining behavior
- refusing ambiguity

Nothing in this directory performs work, schedules actions, or authorizes execution.

---

## What These Documents Are

Files in this directory:

- Define **verification criteria** for container transformations
- Specify **invariants and guarantees**
- Declare **what must not change**
- Are **tool-agnostic** and **executor-agnostic**
- Are authoritative once **LOCKED**
- Change only via an explicit **bandy-and-lock** process

They answer questions like:
- *How do we verify a container reshape was lawful?*
- *What identity must be preserved?*
- *What authority is required for this transformation?*
- *What outcomes are explicitly disallowed?*

---

## What These Documents Are Not

This directory does **not** contain:

- Execution logic
- Work orders
- Scripts or automation
- Operational procedures
- Promotion or approval rules
- Tool, path, or storage assumptions
- Project narratives or onboarding guides

Those concerns belong to **execution models** or operational layers.

---

## Relationship to Transformation Processes

Verification specs are **referenced by**, but never embedded in, transformation processes.

- **V-series specs** define *lawful verification criteria*
- **P-series specs** (when created) will define *how transformations are carried out*
- Execution models may enforce, sequence, or refuse transformations
- They may **not redefine verification semantics**

This separation is intentional.

> The judiciary defines what is lawful.
> The executive defines what may be done.
> Neither implements the other.

---

## Key Insight: Verification is Independent

**Verification can be called independently of transformation:**
- Before transformation (baseline check)
- After transformation (compliance check)
- Independently (audit, validation, integrity check)
- Without transformation (verify existing artifacts)

Verification answers: **"Does this artifact satisfy constraints?"**

Transformation answers: **"Perform this operation."**

---

## Locked Specifications

Only files explicitly marked `_LOCKED.md` are authoritative.

Current locked verification specs:

- `v_1_container_reshape_verification_v_1_2_LOCKED.md`
- `v_2_container_regeneration_verification_v_1_2_LOCKED.md`
- `v_3_container_reordering_verification_v_1_2_LOCKED.md`
- `v_4_container_replacement_verification_v_1_2_LOCKED.md`
- `v_5_container_split_merge_verification_v_1_2_LOCKED.md`

Earlier or working versions are retained for auditability but must not be used for execution or governance decisions.

---

## Change Control

- All changes require a **bandy-and-lock** process
- New versions must increment version numbers
- Prior versions must be preserved
- Semantic drift without explicit lock is prohibited

---

## Scope Boundary

These specifications apply **only to existing container types**.

- Creation of new container or product-layer types is out of scope
- Authority migration is handled at the execution-model boundary
- Execution mechanics are explicitly excluded

---

## Location

**Directory:** `dochome/operations/verifications/`

**Rationale:** Verification is a process (operations layer), defining HOW work is verified.

---

**End of document**
