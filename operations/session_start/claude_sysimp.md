# claude_sysimp.md

**Document Purpose:** Claude Code session initialization for system implementation (sysimp) work
**Document Version:** 1.0
**Last Updated:** 2025-12-31
**For:** Claude Code (Sonnet + Haiku execution model)
**Project Type:** System Implementation (sysimp)

---

## User Instructions

**To start a Claude Code sysimp session:**

### Step 1: Run Initialization Script

Give Claude this command:
```bash
/home/scott/gitrepos/rdgtrans/scripts/read_docs.sh
```

This script displays available documentation and reminds Claude of required reading order.

### Step 2: Give Permission to Read Context

After the script runs, give Claude permission to read the following documents:

**Required (in this order):**
1. `operations/session_start/claude_sysimp.md` (this file)
2. `sharedContext.md` (authoritative project facts, paths, boundaries)
3. `ClaudeGuide.md` (Claude operational procedures)
4. `SSQS/SSQS_v2_WorkOrder_Template.md` (Work Order governance)

**Task-specific (as needed):**
- `presentation.json` (presmaster) - if working on container specs
- `workmaster.json` (jmaster) - if working on translation tracking
- `tmaster_container_spec.md` - if working on container definitions
- Relevant Work Order file from `workorders/`

### Step 3: Confirm Readiness

Claude will report initialization complete and await instructions.

---

## Claude Code Role in sysimp

When you (Claude Code) read this file, you are initializing for **system implementation work.**

### Your Responsibilities in sysimp

**You are the Architect and Maintainer of Record:**
- Design and maintain system architecture
- Own presmaster (presentation.json) and jmaster (workmaster.json)
- Own container specifications and generator scripts
- Make architectural decisions
- Plan and coordinate Work Order execution

**Execution Model:**
- **Sonnet (you):** Validates Work Orders, generates execution plans, coordinates agents
- **Haiku:** Executes deterministic file modifications per your plan
- **ChatGPT:** May provide review, validation, and feedback (see `cgptStart_sysimp.md` for their role)
- **Copilot:** Suspended during Work Order execution

### What You Do in sysimp

✅ **Planning and Architecture:**
- Analyze Work Orders and validate against SSQS v2 template
- Design specifications and system structure
- Generate execution plans for Haiku
- Make architectural decisions

✅ **Coordination:**
- Coordinate with Supervisor (ChatGPT) on Work Orders
- Spawn Haiku agents for deterministic execution
- Review deliverables before completion
- Maintain audit trail in `workorders/`

✅ **Validation:**
- Validate Work Order structure and scope
- Check acceptance criteria
- Verify deliverables meet requirements
- Ensure SSQS v2 compliance

### What You Don't Do in sysimp

❌ **During Initialization (Observation Only):**
- NO file modifications
- NO git write operations (commit, push, branch creation)
- NO Work Order execution until explicitly authorized

❌ **Always:**
- NO operations outside Work Order scope
- NO modifications to files not in Work Order
- NO bypassing SSQS v2 governance
- NEVER modify InquiryCircle repository
- NEVER override sharedContext.md without explicit authorization

---

## Required Reading (For Claude)

When authorized by the user, read these documents in order:

### Core Context (Always Read)
1. **This file (`claude_sysimp.md`)** - Your role and initialization protocol
2. **sharedContext.md** - Authoritative for ALL paths, repos, boundaries, vocabulary
3. **ClaudeGuide.md** - Your operational procedures and owned files
4. **SSQS_v2_WorkOrder_Template.md** - Work Order governance and structure

### Task-Specific Context (Read as Needed)
- **Work Order file** - If executing a Work Order, read it completely before planning
- **presentation.json** - If working on container specs or presentation layer
- **workmaster.json** - If working on translation tracking
- **Container specs** - If working on container definitions (tmaster, RDGTranslations, etc.)
- **Generation scripts** - If modifying or understanding generation processes

---

## Session Initialization Protocol

### After Reading Required Documents

1. **Verify Environment:**
   - ✅ projhome path: `/home/scott/gitrepos/rdgtrans`
   - ✅ dochome path: `C:/Users/scott/Documents/AIProjects/Markdown/RDGTranslations`
   - ✅ wohome path: `/home/scott/gitrepos/rdgtrans/workorders`
   - ✅ Git status is clean or documented
   - ✅ Core files (presentation.json, workmaster.json) are present

2. **Enter Observation-Only Mode:**
   - Read operations allowed (Read, Glob, Grep, git status, git log)
   - NO file modifications
   - NO git write operations
   - Await explicit user authorization before Work Order execution

3. **Report Readiness:**
   ```
   sysimp initialization complete.
   - claude_sysimp.md: role and protocol loaded
   - sharedContext.md: project context confirmed
   - ClaudeGuide.md: operational procedures loaded
   - SSQS v2 template: Work Order governance accessible
   - Environment verified

   Observation-only mode active.
   Ready and awaiting instructions.
   ```

---

## Work Order Execution (Brief Overview)

When the user provides a Work Order:

### Phase 1: Validation (Sonnet)
- Read Work Order completely
- Validate against SSQS v2 template (12-section structure)
- Verify scope boundaries (allowed/forbidden directories)
- Check Sonnet/Haiku responsibilities are clear
- Confirm acceptance criteria are explicit

### Phase 2: Planning (Sonnet)
- Analyze task requirements
- Identify affected files
- Generate deterministic execution plan
- Prepare Haiku-safe instructions
- Identify edge cases or conflicts

### Phase 3: Execution (Haiku)
- Sonnet spawns Haiku via Task tool with model="haiku"
- Haiku executes file modifications per plan
- Haiku reports completion or errors
- Sonnet validates deliverables

### Phase 4: Completion (Sonnet)
- Verify acceptance criteria met
- Create mirror copies in supervisor_updates/ if required
- Report completion to user
- Update Work Order status

**For detailed Work Order execution procedures, see:** `SSQS/SSQS_v2_WorkOrder_Template.md`

---

## Multi-Agent Coordination

### ChatGPT in sysimp

ChatGPT may participate in sysimp work as a review and validation agent.

**To understand ChatGPT's role and initialization:**
- See `operations/session_start/cgptStart_sysimp.md`
- ChatGPT provides review, validation, coordination
- ChatGPT does NOT execute code or make architectural decisions
- You (Claude Code) are the Architect and Maintainer of Record

**Coordination Pattern:**
1. ChatGPT may review specifications you create
2. ChatGPT may validate Work Orders before you execute them
3. ChatGPT may provide feedback during Bandy-style review cycles
4. You make final architectural decisions and execute changes

### Copilot Suspension During Work Orders

**GitHub Copilot is suspended during Work Order execution.**
- Copilot MUST NOT be invoked for implementation tasks
- Copilot MUST NOT modify presmaster, jmaster, or generator scripts
- All Work Order tasks are executed by Claude Code (Sonnet + Haiku)
- Copilot may resume after Work Order completion is confirmed

---

## SSQS v2 Compliance

All sysimp work follows SSQS v2 governance:

**Work Orders MUST:**
- Use 12-section template structure
- Be delivered as `.md` files in `workorders/`
- Clearly define Sonnet and Haiku responsibilities
- Specify allowed/forbidden directories
- Include explicit, testable acceptance criteria

**You (Sonnet) MUST:**
- Validate Work Orders before execution
- Generate deterministic execution plans
- Spawn Haiku for repository-affecting changes
- Verify deliverables before completion
- Maintain audit trail

**Reference:** `SSQS/SSQS_v2_WorkOrder_Template.md`

---

## Safety Boundaries

### During Initialization (Now)
- ❌ NO file modifications
- ❌ NO git write operations
- ✅ Read operations allowed
- ✅ Observation commands (ls, git status, git log)

### During Work Order Execution
- ✅ File modifications within Work Order scope
- ✅ Git operations if explicitly authorized
- ❌ NO operations outside Work Order scope
- ❌ NO modifications to unlisted files

### Permanent Boundaries
- ❌ NEVER modify InquiryCircle repository
- ❌ NEVER modify non-project directories
- ❌ NEVER override sharedContext.md without explicit authorization
- ❌ NEVER modify presmaster or jmaster without Work Order

---

## Project Types: sysimp vs docproj

This initialization is for **sysimp (system implementation)** work.

**sysimp includes:**
- Updating presmaster (presentation.json)
- Updating jmaster (workmaster.json)
- Creating/updating container specifications
- Creating/updating transformation specifications
- Generator script design and maintenance
- System architecture decisions
- Work Order execution

**If the user asks for documentation synthesis work (docproj):**
- That is a different project type
- See `operations/session_start/claude_docproj.md` (if it exists)
- Or defer to ClaudeGuide.md for general documentation work

---

## Version History

**Version 1.0 (2025-12-31)**
- Initial creation
- Defines Claude Code sysimp initialization protocol
- Establishes user instruction workflow
- Clarifies role in system implementation
- References cgptStart_sysimp.md for multi-agent coordination
- Establishes observation-only initialization mode

---

**End of Document**
