# Claude Code Session Start Protocol

**Document Version:** 2.1
**SSQS Version:** 2.0
**Last Updated:** 2025-12-11
**Purpose:** Authoritative session initialization protocol for Claude Code

---

## Overview

This document defines the standard procedure for starting a Claude Code work session in the RDG Translation Project. It ensures consistent initialization, proper context loading, and compliance with SSQS v2 governance.

---

## SSQS Compliance & Execution Model

### SSQS v2 Work Order Template

All Work Orders in this project MUST conform to the SSQS v2 Work Order Template.

**Template Location:**
```
dochome/SSQS/SSQS_v2_WorkOrder_Template.md
```

**Absolute Path:**
```
C:/Users/scott/Documents/AIProjects/Markdown/RDGTranslations/SSQS/SSQS_v2_WorkOrder_Template.md
```

### Template Authority

The SSQS v2 template is the authoritative definition of:
- Work Order structure and required sections
- Sonnet/Haiku execution governance
- Error handling and escalation procedures
- Deliverables and acceptance criteria
- Metadata requirements

**All Work Orders MUST:**
- Follow the 12-section structure defined in SSQS v2 template
- Clearly define Sonnet and Haiku responsibilities
- Specify allowed/forbidden directories
- Provide deterministic, Haiku-safe task descriptions
- Include explicit acceptance criteria

### Sonnet/Haiku Execution Model

Claude Code operates using a dual-model execution strategy:

#### Sonnet Responsibilities
- **Architecture & Planning:** Sonnet analyzes Work Orders, generates execution plans, and makes architectural decisions
- **Validation:** Sonnet validates Work Orders against SSQS v2 template
- **Coordination:** Sonnet coordinates between Supervisor and execution agents
- **Exception Handling:** Sonnet handles unexpected conditions and requests clarification when needed
- **Quality Assurance:** Sonnet reviews deliverables before submission

#### Haiku Responsibilities
- **Deterministic Execution:** Haiku performs file modifications following Sonnet's plan
- **Repository Operations:** Haiku executes git operations, file edits, and writes
- **Error Reporting:** Haiku halts on unexpected behavior and reports exact errors to Sonnet
- **Cost Efficiency:** Haiku handles routine, well-defined tasks at lower computational cost

#### Execution Rule
**Sonnet plans and delegates repository-affecting changes to Haiku.**

When a Work Order requires file modifications:
1. Sonnet generates a deterministic execution plan
2. Sonnet validates the plan against Work Order constraints
3. Sonnet spawns Haiku (via Task tool) with explicit instructions
4. Haiku executes the plan exactly as specified
5. Haiku reports completion or errors back to Sonnet
6. Sonnet validates deliverables and confirms completion

### Copilot Suspension Rule

**GitHub Copilot is suspended during Work Order execution.**

When Claude Code is executing a Work Order:
- Copilot MUST NOT be invoked for implementation tasks
- Copilot MUST NOT modify presmaster, jmaster, or generator scripts
- All Work Order tasks are executed by Claude Code (Sonnet + Haiku)
- Copilot may resume normal operations after Work Order completion is confirmed

**Rationale:** Work Orders require architectural oversight and SSQS compliance verification that only Claude Code can provide.

---

## Session Initialization Procedure

### Step 1: Run Initialization Script

Execute the context loading script:
```bash
/home/scott/gitrepos/rdgtrans/scripts/read_docs.sh
```

This script:
- Identifies available documentation files
- Displays canonical file list
- Reminds Claude to read sharedContext.md first

### Step 2: Load Core Context

**REQUIRED READING ORDER:**

1. **sharedContext.md** (MUST READ FIRST)
   - Authoritative source for paths, repositories, structure
   - Defines AI agent roles and boundaries
   - Establishes shared vocabulary

2. **ClaudeGuide.md** (MUST READ SECOND)
   - Claude Code operational procedures
   - Owned files and responsibilities
   - Coordination with other AI agents

3. **Additional Documentation** (as needed)
   - SupervisorSessionQuickStart_v2.md - Supervisor coordination protocol
   - presentationJson.md - Presentation layer master
   - projspec.md - Project technical specification
   - tmaster_container_spec.md - Container specifications

### Step 3: Verify Environment

Confirm:
- ✅ projhome path is correct
- ✅ dochome path is accessible
- ✅ Git repository status is clean or documented
- ✅ Core files (workmaster.json, presentation.json) are present
- ✅ SSQS v2 template is accessible

### Step 4: Await Instructions

After context loading:
- **DO NOT** begin work without explicit user instruction
- **DO NOT** modify files during initialization
- **READY STATE:** "Context loaded. Ready and awaiting instructions."

---

## Work Order Execution Protocol

When the user provides a Work Order:

### Phase 1: Validation (Sonnet)
1. Read the Work Order completely
2. Validate against SSQS v2 template structure
3. Confirm Work Order ID, date, priority are present
4. Verify scope boundaries are clearly defined
5. Check that Sonnet/Haiku responsibilities are specified

### Phase 2: Planning (Sonnet)
1. Analyze task requirements
2. Identify affected files and directories
3. Generate deterministic execution plan
4. Identify potential edge cases or conflicts
5. Prepare Haiku-safe instructions

### Phase 3: Execution (Haiku)
1. Sonnet spawns Haiku via Task tool with model="haiku"
2. Haiku executes file modifications per plan
3. Haiku reports completion or errors
4. Sonnet validates deliverables

### Phase 4: Completion (Sonnet)
1. Verify all acceptance criteria met
2. Create mirror copies in supervisor_updates/ if required
3. Report completion to user
4. Update work order status if applicable

---

## Safety Boundaries

Claude Code MUST observe these absolute boundaries:

### During Initialization (Observation Only)
- ❌ NO file modifications
- ❌ NO git write operations (commit, push, branch creation)
- ✅ Read operations allowed (Read, Glob, Grep, git status, git log)
- ✅ Bash commands for observation (ls, cat, etc.)

### During Work Order Execution (Authorized Operations)
- ✅ File modifications within Work Order scope
- ✅ Git operations if explicitly authorized in Work Order
- ❌ NO operations outside Work Order scope boundaries
- ❌ NO modifications to files not listed in Work Order

### Permanent Boundaries
- ❌ NEVER modify InquiryCircle repository
- ❌ NEVER modify non-project directories
- ❌ NEVER override sharedContext.md without explicit authorization
- ❌ NEVER modify presmaster or jmaster without Work Order

---

## Required Session Initialization Behavior

On every session start, Claude Code MUST:

1. **Execute read_docs.sh** (or confirm it has been run)
2. **Read sharedContext.md** before any other documentation
3. **Confirm project paths** match sharedContext.md definitions
4. **Verify SSQS v2 template accessibility** at dochome/SSQS/
5. **Enter observation-only mode** until instructed otherwise
6. **Report readiness** using standard format:

```
Context loaded successfully.
- sharedContext.md read and confirmed
- ClaudeGuide.md operational procedures loaded
- SSQS v2 template accessible
- Project paths verified

Ready and awaiting instructions.
```

---

## Integration with Supervisor Protocol

This document integrates with SupervisorSessionQuickStart_v2.md:

- **Supervisor (ChatGPT):** Issues Work Orders and maintains structured memory
- **Claude Code (Sonnet):** Executes Work Orders following SSQS v2 governance
- **Haiku:** Performs deterministic file operations under Sonnet supervision
- **Copilot:** Suspended during Work Order execution

When working with Supervisor:
- Claude provides State Reports as defined in SupervisorSessionQuickStart_v2.md
- Claude validates all Work Orders against SSQS v2 template
- Claude creates mirror copies in supervisor_updates/ when required
- Claude maintains audit trail in workorders/ directory

---

## Work Order Delivery Protocol

All Work Orders MUST be delivered as `.md` files placed into the project workspace
(e.g., via file upload or drag-in) before Claude Code begins execution.

### Requirements

1. Sonnet MUST NOT accept Work Orders delivered as plain text.
   Only Work Orders provided as `.md` files are valid for execution.

2. The Work Order file MUST be located in:
   wohome/WO-xxxx.md

3. If the Work Order file is not present, Sonnet MUST respond:
   "Work Order file missing. Please upload the Work Order `.md` file."

4. Sonnet MUST validate:
   - file presence
   - Work Order ID
   - SSQS v2 structural compliance
   - allowed/forbidden directories
   - deterministic task definitions
   BEFORE Haiku is permitted to execute.

5. Upon execution, Haiku MUST:
   - apply modifications defined in the Work Order
   - create a mirror copy in:
     supervisor_updates/<WO-ID>/

6. Sonnet MUST NOT allow execution to begin until the Work Order file is
   successfully validated.

---

## Version History

### Version 2.1 (2025-12-11)
- Added Work Order Delivery Protocol section per WO-SSQS-v2-SessionStart-Update-002
- Requires Work Orders to be delivered as .md files in wohome/
- Mandates validation before execution begins
- Enforces deterministic processing and audit integrity

### Version 2.0 (2025-12-11)
- Initial version created per WO-SSQS-v2-SessionStart-Update-001
- Added SSQS v2 compliance section
- Defined Sonnet/Haiku execution model
- Established Copilot suspension rule
- Integrated with SupervisorSessionQuickStart_v2.md protocol

---

## End of Document
