# CLONE/MIGRATE: Two-Tier Development Process

**Date:** 2026-01-02
**Status:** Narrative (Non-Canonical)
**Purpose:** Document the conceptual foundation for CLONE and MIGRATE processes

---

## The Problem

The current SSQS-governed process has significant strengths:
- **Governed** - Work orders, audit trails, multi-agent coordination
- **Low regression** - Careful, documented changes prevent errors
- **Effective error detection** - Issues discovered and resolved quickly (e.g., PR ID systematic error)

However, the process is **ponderous for new work**:
- Creating new artifact types requires full work order overhead
- Governance slows down creative/exploratory work
- Experimentation feels heavy

---

## The Solution: Two-Tier Approach

### Tier 1: JAM SESSION (Cursor Environment)
**Purpose:** Rapid prototyping, unstructured exploration, pre-canonical work

**Environment:** Cursor IDE (separate from production Claude Code)

**Characteristics:**
- ✅ Fast, creative, experimental
- ✅ Safe to fail (isolated from production)
- ✅ No governance overhead during exploration
- ❌ Non-canonical (not part of official system until migrated)

### Tier 2: PRODUCTION (Claude Code Environment)
**Purpose:** Governed integration, canonical system maintenance

**Environment:** VSCode + Claude Code (current setup)

**Characteristics:**
- ✅ Governed (SSQS work orders)
- ✅ Canonical (authoritative system state)
- ✅ Audit trail maintained
- ✅ Multi-agent coordination

---

## CLONE Process (Formal Operation)

**CLONE** creates an isolated sandbox environment for jam session work.

### Benefits of Formalizing CLONE:

1. **Efficiency via Selectivity**
   - Not everything needs to be cloned for every prototype
   - Clone specification defines exact scope
   - Example: "For sagemaster development, clone presentation.json + lmasters/ + container specs, skip corrections/"

2. **Information Hiding**
   - Create new artifact types without legacy assumptions
   - Start with clean slate
   - Avoid "we've always done it this way" bias

3. **Works Within Governance**
   - CLONE work orders can be bandy_locked
   - Audit trail: Why cloned? What's the goal?
   - Exit criteria defined upfront

4. **Guardrails in Cursor**
   - Clone WO specifies forbidden operations
   - Example: "NEVER modify presmaster in clone" or "presmaster is READ-ONLY reference"
   - Cursor init script enforces boundaries

5. **Guides MIGRATE**
   - CLONE spec documents WHAT was cloned and WHY
   - MIGRATE reads CLONE spec to understand scope
   - "We cloned X, Y, Z → MIGRATE must handle X', Y', Z'"

6. **Facilitates Diffing**
   - `diff -r /rdgtrans/ /rdgtrans_clone/` shows what changed
   - MIGRATE WO uses diff output to plan integration
   - Catches unintended modifications

7. **Physical Portability** (USB Drive Target)
   - Clone target: `/media/scott/USB_1TB/rdgtrans_clone/`
   - Work on laptop disconnected from production
   - Physical isolation = additional safety
   - Sync back when ready for MIGRATE

---

## MIGRATE Process (Formal Operation)

**MIGRATE** integrates validated prototypes from clone into canonical system.

### Key Aspects:

1. **Triggered by User Approval**
   - Prototype complete and validated in Cursor
   - User creates MIGRATE work order
   - Claude Code executes governed migration

2. **References Source CLONE**
   - MIGRATE WO references CLONE WO ID
   - Inherits context: what was cloned, why, with what constraints

3. **Diff-Driven**
   - Analyzes differences between clone and production
   - Plans integration based on actual changes
   - Verifies no unintended modifications

4. **Verification Requirements**
   - How to validate successful migration
   - Regression testing if applicable
   - Rollback plan if migration fails

---

## Implementation Strategy

### CLONE and MIGRATE as Transformation Operations

Treat them like T1-T6 transformations (if those were formalized):

- **C1: CLONE Operation Spec** → `dochome/transformations/C1_Clone_Spec.md`
- **M1: MIGRATE Operation Spec** → `dochome/transformations/M1_Migrate_Spec.md`

### Work Order Templates

- **CLONE Work Order Template** → `SSQS/CLONE_WorkOrder_Template.md`
- **MIGRATE Work Order Template** → `SSQS/MIGRATE_WorkOrder_Template.md`

### Critical Success Factors

1. **Clone Management**
   - Clear naming conventions (e.g., `/rdgtrans_clone_sagemaster_001/`)
   - Clone inventory specification
   - Clone lifespan (disposable vs. archival)

2. **Migration Protocol**
   - Acceptance criteria for prototype
   - Integration verification steps
   - Rollback procedures

3. **Boundary Discipline**
   - Cursor NEVER writes to production paths
   - Only Claude Code writes to canonical directories
   - Physical separation enforced (USB vs. WSL)

---

## Example Use Case: Sagemaster Development

### Phase 1: CLONE
**Work Order:** `wo-clone-sagemaster-001.md`

**Clone Inventory:**
- presentation.json (read-only reference)
- Sample lmaster files (for testing)
- Container spec templates
- Exclude: corrections/, archive/, workorders/

**Clone Target:** `/media/scott/USB_1TB/rdgtrans_clone_sagemaster_001/`

**Guardrails:**
- NEVER modify presmaster in clone
- Create sagemaster.json separately
- Test patterns isolated from production

**Success Criteria:**
- Sagemaster container spec complete
- Sample sagemaster file generated and validated
- Ready for integration review

### Phase 2: JAM SESSION (Cursor)
- Prototype sagemaster structure
- Experiment with field layouts
- Test with sample content
- Iterate rapidly without governance overhead

### Phase 3: MIGRATE
**Work Order:** `wo-migrate-sagemaster-001.md`

**Source:** References `wo-clone-sagemaster-001.md`

**Diff Analysis:**
- New file: `sagemaster_container_spec.md`
- New file: `sagemaster.json` (or section in presentation.json)
- Modified: container type documentation

**Integration Plan:**
1. Add sagemaster spec to dochome
2. Update presentation.json with sagemaster container type
3. Verify against presmaster v3.0.0 validation
4. Update related documentation

**Verification:**
- Sagemaster spec passes validation
- No regressions in existing container types
- Documentation updated

---

## Next Steps

1. **Define Clone Protocol**
   - Start with `CloneProtocol.md` (lightweight documentation)
   - Evolve into formal C1_Clone_Spec.md after testing

2. **Test with Small Prototype**
   - Prove concept with low-risk artifact
   - Refine protocols based on learnings

3. **Formalize MIGRATE**
   - Create M1_Migrate_Spec.md
   - Define verification requirements

4. **Establish Cursor Environment**
   - Set up Cursor account
   - Configure USB clone target
   - Test CLONE → JAM SESSION → MIGRATE workflow

---

## Relationship to Existing Process

CLONE/MIGRATE **extends** (not replaces) current governance:

- **Before CLONE:** SSQS governance for all work (heavy but safe)
- **After CLONE/MIGRATE:**
  - **Exploratory work:** CLONE → Cursor jam session → MIGRATE (fast + safe)
  - **Production work:** Direct SSQS governance (unchanged)
  - **Error correction:** Direct fixes in production (unchanged, like PR ID fix)

**Best of both worlds:** Creative freedom + production safety

---

## Key Principles

1. **Cursor = Disposable Sandbox** - Don't get attached to clone environments
2. **Claude Code = Canonical Authority** - All production writes through Claude Code only
3. **Formal Processes** - CLONE and MIGRATE are documented, governed operations
4. **Clear Boundaries** - Physical and logical separation between tiers
5. **Diff-Driven Integration** - MIGRATE based on actual changes, not assumptions

---

**End of Narrative Document**
