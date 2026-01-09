# CursorClone
CLONE/MIGRATE: Two-Tier Development Process
Date: 2026-01-06
Status: Narrative (Non-Canonical)
Purpose: Document the conceptual foundation for CLONE and MIGRATE processes

## Jam Session
### Goal
- Our goal is to build a system that lets us safely buildi artifacts that can later to be imported into our current, highly goverend production system in a safe manner  while allowing for improvitory level of flexibilirty

### The Jam Session Envirnment
#### Virtual Envrionments
I have 2 VMS running under vmplayer for running cursorai in a sandbox  
Since VMPlayer supports snapshoting,  the web1 vm can be snapshotted and reinited 

 
    
##### Cursor VM
Jammy Jellyfist Ubuntu Desktop 22.04 LTS
user;  cuser: password animalFrac45
ssh keys in stored for ssh into Web1
 - Cursor AI runs here
  
##### Web1 VM    
36 GB   HD 
web1 resolves to 192.168.62.128  on the local Windows system 
Ubuntu Server 22.04 LTS 
User is freeagent password is masNo480    
  Installed the openssh server  
ssh keys in stored for ssh from cursorai

##### Shared Drives
Web1: C:\Users\scott\Documents\AIProjects\VMShares\web1
  Both VM's have direct access to this 
  

#### Git setup
I have a number of public git repos at this path:  https://github.com/scott009/    
I would like to Claude   to make sure they are uptodate and then I would like them  to be "cloned"  
  
I will give CursorAI access to these Repos and I will NOT give it access to the repos they are sourced from 
Here is the list 
 rdgtrans   ->c-trans
rdgtransdocs  ->c-transdocs
showoff -> c-showoff
InquiryCircle -> c-ic







The Problem
The current SSQS-governed process has significant strengths:

Governed - Work orders, audit trails, multi-agent coordination
Low regression - Careful, documented changes prevent errors
Effective error detection - Issues discovered and resolved quickly (e.g., PR ID systematic error)
However, the process is ponderous for new work:

Creating new artifact types requires full work order overhead
Governance slows down creative/exploratory work
Experimentation feels heavy
The Solution: Two-Tier Approach
Tier 1: JAM SESSION (Cursor Environment)
Purpose: Rapid prototyping, unstructured exploration, pre-canonical work

Environment: Cursor IDE (separate from production Claude Code)

Characteristics:

✅ Fast, creative, experimental
✅ Safe to fail (isolated from production)
✅ No governance overhead during exploration
❌ Non-canonical (not part of official system until migrated)
Tier 2: PRODUCTION (Claude Code Environment)
Purpose: Governed integration, canonical system maintenance

Environment: VSCode + Claude Code (current setup)

Characteristics:

✅ Governed (SSQS work orders)
✅ Canonical (authoritative system state)
✅ Audit trail maintained
✅ Multi-agent coordination
CLONE Process (Formal Operation)
CLONE creates an isolated sandbox environment for jam session work.

Benefits of Formalizing CLONE:
Efficiency via Selectivity

Not everything needs to be cloned for every prototype
Clone specification defines exact scope
Example: "For sagemaster development, clone presentation.json + lmasters/ + container specs, skip corrections/"
Information Hiding

Create new artifact types without legacy assumptions
Start with clean slate
Avoid "we've always done it this way" bias
Works Within Governance

CLONE work orders can be bandy_locked
Audit trail: Why cloned? What's the goal?
Exit criteria defined upfront
Guardrails in Cursor

Clone WO specifies forbidden operations
Example: "NEVER modify presmaster in clone" or "presmaster is READ-ONLY reference"
Cursor init script enforces boundaries
Guides MIGRATE

CLONE spec documents WHAT was cloned and WHY
MIGRATE reads CLONE spec to understand scope
"We cloned X, Y, Z → MIGRATE must handle X', Y', Z'"
Facilitates Diffing

diff -r /rdgtrans/ /rdgtrans_clone/ shows what changed
MIGRATE WO uses diff output to plan integration
Catches unintended modifications
Physical Portability (USB Drive Target)

Clone target: /media/scott/USB_1TB/rdgtrans_clone/
Work on laptop disconnected from production
Physical isolation = additional safety
Sync back when ready for MIGRATE
MIGRATE Process (Formal Operation)
MIGRATE integrates validated prototypes from clone into canonical system.

Key Aspects:
Triggered by User Approval

Prototype complete and validated in Cursor
User creates MIGRATE work order
Claude Code executes governed migration
References Source CLONE

MIGRATE WO references CLONE WO ID
Inherits context: what was cloned, why, with what constraints
Diff-Driven

Analyzes differences between clone and production
Plans integration based on actual changes
Verifies no unintended modifications
Verification Requirements

How to validate successful migration
Regression testing if applicable
Rollback plan if migration fails
Implementation Strategy
CLONE and MIGRATE as Transformation Operations
Treat them like T1-T6 transformations (if those were formalized):

C1: CLONE Operation Spec → dochome/transformations/C1_Clone_Spec.md
M1: MIGRATE Operation Spec → dochome/transformations/M1_Migrate_Spec.md
Work Order Templates
CLONE Work Order Template → SSQS/CLONE_WorkOrder_Template.md
MIGRATE Work Order Template → SSQS/MIGRATE_WorkOrder_Template.md
Critical Success Factors
Clone Management

Clear naming conventions (e.g., /rdgtrans_clone_sagemaster_001/)
Clone inventory specification
Clone lifespan (disposable vs. archival)
Migration Protocol

Acceptance criteria for prototype
Integration verification steps
Rollback procedures
Boundary Discipline

Cursor NEVER writes to production paths
Only Claude Code writes to canonical directories
Physical separation enforced (USB vs. WSL)
Example Use Case: Sagemaster Development
Phase 1: CLONE
Work Order: wo-clone-sagemaster-001.md

Clone Inventory:

presentation.json (read-only reference)
Sample lmaster files (for testing)
Container spec templates
Exclude: corrections/, archive/, workorders/
Clone Target: /media/scott/USB_1TB/rdgtrans_clone_sagemaster_001/

Guardrails:

NEVER modify presmaster in clone
Create sagemaster.json separately
Test patterns isolated from production
Success Criteria:

Sagemaster container spec complete
Sample sagemaster file generated and validated
Ready for integration review
Phase 2: JAM SESSION (Cursor)
Prototype sagemaster structure
Experiment with field layouts
Test with sample content
Iterate rapidly without governance overhead
Phase 3: MIGRATE
Work Order: wo-migrate-sagemaster-001.md

Source: References wo-clone-sagemaster-001.md

Diff Analysis:

New file: sagemaster_container_spec.md
New file: sagemaster.json (or section in presentation.json)
Modified: container type documentation
Integration Plan:

Add sagemaster spec to dochome
Update presentation.json with sagemaster container type
Verify against presmaster v3.0.0 validation
Update related documentation
Verification:

Sagemaster spec passes validation
No regressions in existing container types
Documentation updated
Next Steps
Define Clone Protocol

Start with CloneProtocol.md (lightweight documentation)
Evolve into formal C1_Clone_Spec.md after testing
Test with Small Prototype

Prove concept with low-risk artifact
Refine protocols based on learnings
Formalize MIGRATE

Create M1_Migrate_Spec.md
Define verification requirements
Establish Cursor Environment

Set up Cursor account
Configure USB clone target
Test CLONE → JAM SESSION → MIGRATE workflow
Relationship to Existing Process
CLONE/MIGRATE extends (not replaces) current governance:

Before CLONE: SSQS governance for all work (heavy but safe)
After CLONE/MIGRATE:
Exploratory work: CLONE → Cursor jam session → MIGRATE (fast + safe)
Production work: Direct SSQS governance (unchanged)
Error correction: Direct fixes in production (unchanged, like PR ID fix)
Best of both worlds: Creative freedom + production safety

Key Principles
Cursor = Disposable Sandbox - Don't get attached to clone environments
Claude Code = Canonical Authority - All production writes through Claude Code only
Formal Processes - CLONE and MIGRATE are documented, governed operations
Clear Boundaries - Physical and logical separation between tiers
Diff-Driven Integration - MIGRATE based on actual changes, not assumptions
End of Narrative Document