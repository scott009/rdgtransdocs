# RDG Translation Project Roadmap

**Document Type:** Consolidated Narrative
**Purpose:** Strategic overview and architectural direction for manifest creation
**Status:** Draft (for Bandy review)
**Last Updated:** 2025-12-28

---

## Executive Summary

The Recovery Dharma Global (RDG) Translation Project exists to bring Buddhist-based recovery resources to Asian regions through high-fidelity, multimodal translation of the primary RDG text. This roadmap consolidates the project's narrative foundation, current architecture, and strategic direction to support manifest creation and future specification work.

**Core Mission:** Expanding the Buddhist-based recovery path to Asian regions, beginning with Thailand, through high-fidelity, multimodal translation of the primary RDG text.

---

## Table of Contents

1. [Project Origins and Evolution](#project-origins-and-evolution)
2. [System Architecture Overview](#system-architecture-overview)
3. [Current State Assessment](#current-state-assessment)
4. [Artifact Classification Framework](#artifact-classification-framework)
5. [Human-Centered Corrections Architecture](#human-centered-corrections-architecture)
6. [Infrastructure Evolution Strategy](#infrastructure-evolution-strategy)
7. [Out-of-Band Process Framework](#out-of-band-process-framework)
8. [Documentation Architecture](#documentation-architecture)
9. [Strategic Priorities and Next Steps](#strategic-priorities-and-next-steps)

---

## 1. Project Origins and Evolution

### The Catalyst

Recovery Dharma Global (RDG) is a non-profit organization utilizing Buddhist practices and principles to support recovery from addiction. Historically, RDG lacked a physical or translated presence in Asian regions where Buddhism originated.

The project was catalyzed when a contact in Thailand reached out via official channels inquiring about Thai translations of the Recovery Dharma book. This represented a critical opportunity to bring the "Dharma of Recovery" back to its geographical roots.

### The Source of Truth

The Recovery Dharma book serves as the semi-authoritative "Source of Truth" for this project. It is the anchor for all tasks. While specific administrative deviations from the text may exist for strategic reasons, the book remains the content foundation for all repositories.

### The Four Tasks: Project Evolution

The project has moved through four distinct phases of implementation, evolving from raw text to structured, multimodal "containers."

#### Task 1: Structural Transformation

**The Problem:** The original source was a "problem-ridden" Microsoft Word file lacking the structure necessary for modern digital workflows.

**The Action:** A significant manual and technical effort was undertaken to transform the Word file into a structured, human-editor-friendly format.

**The Result:** RDGBook_English.md

**Design Choice:** Eliminating non-structural elements to ensure the document focused purely on content integrity.

#### Task 2: Multilingual Translation

**The Agent:** Claude (Anthropic) was selected as the primary translation agent.

**The Strategy:** Leveraging the efficiency of Large Language Models (LLMs) to perform parallel translations into multiple Asian languages simultaneously.

**The Result:** The multilingual masters found in the /lmasters directory.

**Target Languages:**
- Thai
- Japanese
- Korean
- Vietnamese
- Simplified Chinese
- Traditional Chinese

#### Task 3: Audio Production (Spoken Versions)

**The Agent:** Azure AI Speech was chosen for its optimal balance of high-quality neural voices and cost-efficiency.

**The Scope:** Initial efforts have focused on converting a small, high-impact section of the book into spoken versions to test the fidelity of the "Spoken Dharma."

#### Task 4: Container Development and Review Systems

**The Challenge:** Moving from static translations to interactive, human-reviewed correction systems.

**The Approach:** Creating HTML containers (tmaster forms) that enable bilingual reviewers to submit corrections.

**Current Status:** In transition from Netlify-based submission system to VPS-hosted, database-backed architecture.

---

## 2. System Architecture Overview

### Conceptual Model: Entities, Processes, and Artifacts

At the highest level, the system consists of three fundamental components:

#### Entities

Entities produce artifacts via processes.

**Types of Entities:**

1. **Humans** - Different humans perform different roles. A single human may perform different roles at different times and in different processes.

2. **Agents** - Usually AI-based:
   - Agents exist within Environments
   - Agents are backed by models
   - A single agent can utilize different Models
   - Agents can assume different roles based on the strengths and limitations of both the Agent's model(s) and the environment the agent functions within

**Current Agents:**
- **ChatGPT** - Governance and documentation synthesis
- **Claude Code** - Architecture, specification, system design
- **GitHub Copilot** - Implementation execution (suspended during Work Order execution)

#### Processes

Processes are the activities we perform to produce artifacts.

**Key Processes Identified:**
- Translation generation
- Container generation (HTML forms)
- Correction submission and review
- Master document updates
- Audio production
- Infrastructure deployment

#### Artifacts

Artifacts are the tangible outputs and inputs of the system. (See Section 4 for detailed classification.)

---

## 3. Current State Assessment

### What Works

1. **Content Layer**
   - English master exists and is stable (RDGBook_English.md)
   - Multilingual masters exist for 6 Asian languages in /lmasters
   - Initial audio production successful for test sections

2. **Container Layer**
   - tmaster HTML forms exist for all 6 languages
   - Forms are bilingual and functional
   - Forms have been successfully deployed to end users

3. **Governance Layer**
   - SSQS v2 Work Order system is operational
   - Sonnet/Haiku execution model is defined
   - Clear AI agent role separation established

4. **Documentation Layer**
   - Three-layer architecture defined (Narrative, Operations, Specification)
   - Core governance documents locked (sharedContext.md, SessionStart.md)
   - Layer recognition rules established

### What Needs Attention

1. **Corrections Processing**
   - Current Netlify-based submission system is deprecated (free tier exhausted)
   - No database persistence layer
   - Unclear processing workflow from corrections to language master updates
   - No conflict resolution mechanism for competing corrections

2. **Infrastructure**
   - Reliance on third-party hosting (GitHub Pages, Netlify)
   - Need for owned VPS infrastructure
   - No persistent data layer (database)

3. **Container Specifications**
   - presentation.json (presmaster) is incomplete
   - Only tmaster container type is fully specified
   - RDGTranslations.html (portal) lacks specification
   - SuperTmaster (expert review dashboard) not yet specified

4. **Process Documentation**
   - Major system processes not formally documented
   - Generation scripts exist but lack specification
   - Integration workflows undefined

---

## 4. Artifact Classification Framework

### Classification System

All artifacts in the rdgtrans system can be classified by their purpose and role:

```
Artifacts
├── Content (authoritative source material in various languages)
├── Container (presentation layer - HTML/CSS that displays content)
├── Configuration (structure definitions and state tracking)
├── Governance (rules, protocols, boundaries for system operation)
├── Specification (technical requirements and transformation rules)
├── Process (scripts and tools that transform data)
└── Operational (task tracking, work orders, session coordination)
```

### Artifact Examples by Classification

#### Content Artifacts
*Authoritative source material - the actual book content in different languages*

**Location:** `projhome/lmasters/`
- RDGBook_English.md (authoritative English source)
- RDGBook_Thai.md
- RDGBook_Japanese.md
- RDGBook_Korean.md
- RDGBook_Vietnamese.md
- RDGBook_SimplifiedChinese.md
- RDGBook_TraditionalChinese.md

#### Container Artifacts
*Presentation layer - wraps and displays content to end users*

**Location:** `showoff/docs/` (C:\Users\scott\Documents\RecoveryDharma\RDGBook\output_V1\docs\)

**RDGTranslations.html**
- Portal/Index Container
- Entry point for the entire project
- Organizes and presents project overview, audio introductions, and navigation
- Contains links to all translation masters (tmasterThai, tmasterJapanese, etc.)
- **Status:** Exists but not yet specified in presentation.json

**tmasterThai.html** (and other language tmasters)
- Form Container - Translation correction form
- Linked from RDGTranslations.html portal
- Presents content from both English and target language for bilingual review
- Bilingual web form with 45 chapter titles + 351 paragraphs
- Allows reviewers to submit corrections back to the system
- **Status:** Specified in presentation.json under container_types.tmaster (ONLY container type currently specified)

**Print/Read Containers** (rdgJapanesePrint.html, rdgVietnamese.html, etc.)
- Read-only presentation of translations
- **Status:** Exist but not yet specified

**ada3.css** (styling)
- Shared styling across containers

**SuperTmaster.html** (PLANNED)
- Expert review dashboard for submitted corrections
- Human-centered review interface
- **Status:** Architecturally designed, not yet implemented or specified

#### Configuration Artifacts
*Define structure, track state, configure system behavior*

**Location:** `projhome/`
- **presentation.json (presmaster)** - Presentation layer configuration, container definitions
- **workmaster.json (jmaster)** - Translation tracking metadata, paragraph-level status

#### Governance Artifacts
*Define rules, boundaries, and protocols for system operation*

**Location:** `dochome/`
- sharedContext.md (authoritative project context, paths, AI boundaries)
- SSQS/SSQS_v2_WorkOrder_Template.md (work order structure)
- session_start/SessionStart.md (session initialization protocol)
- session_start/cgptStart_docproj.md (docproj-specific initialization)

#### Specification Artifacts
*Technical requirements, constraints, and transformation rules*

**Location:** `dochome/`
- tmaster_container_spec.md (container specifications)
- t_3_container_reordering_spec_v_1_2_LOCKED.md (transformation spec)
- **Note:** Specification layer is still emerging

#### Process Artifacts
*Scripts and tools that transform, process, or initialize*

**Location:** `projhome/scripts/` and `projhome/py/`
- scripts/read_docs.sh (Claude Code initialization)
- scripts/copilot_init.sh (Copilot initialization)
- scripts/backup.sh (project backup)
- py/ (Python utilities and processors)

#### Operational Artifacts
*Task tracking, work coordination, session management*

**Location:** `dochome/workingfiles/`, `projhome/workorders/`
- workorders/ (Work Order storage, wohome)
- workingfiles/ (temporary working documents, analysis, task tracking)

---

## 5. Human-Centered Corrections Architecture

### The Problem: Current Netlify System (To Be Deprecated)

**Current Flow:**
```
User fills tmasterThai.html
  → Clicks Submit
  → JSON to GitHub via Netlify function
  → Each submission = separate JSON file in corrections/
  → ??? (processing unclear)
```

**Issues:**
1. Cost: Netlify free tier exhausted
2. Infrastructure: No control, third-party dependency
3. Persistence: No proper database
4. Processing: 6-step workflow exists on paper but unclear if automated or manual
5. Conflict resolution: Undefined - what happens when multiple reviewers submit different corrections for same paragraph?
6. Integration: How do corrections get back into language masters?

### The Solution: VPS-Based Human-Centered Architecture

#### Core Design Principle

**User's Guidance:**
> "These are deeply human processes and the human contacts are an important point of the process. It's crucial to understand the limits of what I want to automate."

**Key Insight:** The database facilitates human decision-making, not replaces it.

#### The "SuperTmaster" Concept

Instead of automating approval/integration, create a review dashboard where:
- Each submitted correction appears in a form
- Human reviewer can **Accept**, **Reject**, or **Modify**
- Database is updated based on human decisions
- On document acceptance, a new lmaster.md is generated (separate process)
- If desired, the second version can go through the tmaster process again (iterative improvement)

### The Complete Human-Centered Workflow

```
[PHASE 1: SUBMISSION]
Regular Reviewer
  ↓ uses
tmasterThai.html (correction form)
  ↓ submits corrections
Database → submissions table
        → corrections table (status: 'submitted')

[PHASE 2: EXPERT REVIEW]
Expert Reviewer
  ↓ uses
SuperTmaster.html (NEW CONTAINER TYPE - review dashboard)
  ↓ views each correction with context:
  ├── Submitter info (name, email, bio, notes)
  ├── Paragraph context (English reference, current Thai, paragraph ID)
  ├── Submitted correction (original AI → corrected version)
  └── Comment/explanation
  ↓ for each correction, expert decides:
  ├→ Accept → status: 'accepted', final_text = corrected_text
  ├→ Reject → status: 'rejected'
  └→ Modify → updates final_text, status: 'accepted'

[PHASE 3: GENERATION]
Human triggers generation process
  ↓
Generate new lmasters/RDGBook_Thai.md
  ├── Applies all accepted corrections
  ├── Uses final_text (expert-reviewed version)
  └── Marks corrections as integrated
  ↓
Update workmaster.json (track correction count, version)

[PHASE 4: OPTIONAL ITERATION]
  ↓ (if desired)
Regenerate tmasterThai.html from new lmaster
  ↓
Round 2 of review/corrections begins
```

### Database Schema (High-Level)

**Core Tables:**
1. **submissions** - Raw submission storage (metadata, editor info, timestamp)
2. **corrections** - Individual correction entries (original, corrected, final text; workflow status)
3. **reviewers** - Reviewer tracking (name, email, bio, expert flag, statistics)
4. **correction_conflicts** - Conflict tracking for competing corrections
5. **processing_log** - Workflow audit trail

### New Container Types Identified

For specification in presentation.json:

1. **tmaster** (existing)
   - Translation Master Correction Form
   - For regular reviewers to submit corrections
   - Reference implementation: tmasterThai.html

2. **SuperTmaster** (NEW)
   - Correction Review Dashboard
   - For expert reviewers to review/accept/reject/modify submissions
   - Reference implementation: SuperTmaster.html (to be created)

3. **RDGTranslations** (needs specification)
   - Multi-language portal
   - Entry point covering all languages
   - Reference implementation: RDGTranslations.html

4. **LanguagePortal** (NEW concept)
   - Single-language portal
   - Filtered view for specific language
   - Derived from RDGTranslations structure
   - To be specified before implementation

### Key Architectural Principles

1. **Human Contact Preserved**
   - Expert reviewers see full submitter context
   - Can reach out to submitters for clarification
   - Community building, not just data processing

2. **Human Guidance at Decision Points**
   - Accept/Reject/Modify for each correction (not automated)
   - Conflict resolution by human review (side-by-side comparison)
   - When to generate new lmaster (human triggers, not automatic)
   - Whether to do Round 2 review (human decision)

3. **Database Supports, Doesn't Decide**
   - Tracks workflow status
   - Detects conflicts (flags for human review)
   - Stores all versions (original, corrected, final)
   - Provides audit trail
   - Enables reporting and metrics

4. **Clear Separation of Processes**
   - **Submission:** tmasterThai.html → database
   - **Review:** SuperTmaster.html → human decisions → database updates
   - **Generation:** Script reads accepted corrections → creates new lmaster
   - **Regeneration:** Optional script creates new tmaster from new lmaster

---

## 6. Infrastructure Evolution Strategy

### Current State: GitHub Pages + Netlify

**Limitations:**
- No control over infrastructure
- Third-party dependencies
- Cost constraints (Netlify free tier exhausted)
- No database support
- No dynamic capabilities

### Target State: VPS-Hosted Architecture

#### Core Architectural Principles

1. **Caddy as the Front Door**
   - Caddy is always the entry point
   - HTTPS is automatic and assumed
   - The Caddy configuration should be rarely edited once established
   - Caddy is treated as stable infrastructure, not an application surface

2. **Subdomain-Based Routing**
   - Routing is subdomain-based, not path-based
   - Examples: app1.catbench.com, app2.catbench.com, app3.catbench.com
   - Each subdomain represents a conceptual application or role

3. **DNS-Driven App Switching**
   - DNS determines which application is active
   - Caddy routes are predeclared
   - Application changes handled by DNS updates, not frequent Caddyfile edits
   - Design target: predefine ~10 routes and then largely leave Caddy configuration alone

4. **Cross-Server Reverse Proxying**
   - Must support routing to services running on other servers
   - Example: ic.catbench.com → Inquiry Circle running on a different VPS
   - Allows services to move or scale independently

### Infrastructure Stack

```
VPS Server
├── Caddy (web server + reverse proxy + automatic HTTPS)
├── PostgreSQL (persistence layer)
├── Python application (Flask/FastAPI)
│   ├── Form submission endpoint (replaces Netlify function)
│   ├── SuperTmaster backend API
│   └── Generation scripts
└── Static file hosting
    ├── RDGTranslations.html
    ├── tmasterThai.html, tmasterJapanese.html, etc.
    └── SuperTmaster.html (NEW - review dashboard)
```

### Conceptual Application Roles

#### app1 — Static Content
- Public-facing HTML and CSS
- Translation outputs
- Documentation and reference material
- Intentionally simple and robust

#### app2 — Persistence Layer
- Database-backed service
- Receives form input from static pages
- Acts as a durable data store
- Separates user input and state from presentation

#### app3 — Transformation Layer
- Likely implemented in Python (e.g., Flask)
- Consumes data from the persistence layer
- Generates new documents or derived artifacts
- Opens the door to dynamic documents built from controlled data sources

### Directional Insight

This architecture naturally evolves toward:
- Composable document generation
- Dynamic publishing without abandoning static guarantees
- Clear separation of: Presentation, Persistence, Transformation
- Maintaining option space rather than locking into premature complexity

---

## 7. Out-of-Band Process Framework

### What "Out-of-Band" Means

An **out-of-band process** is any activity that intentionally operates *outside* the formal, authoritative production system.

Out-of-band does **not** mean:
- Unimportant
- Informal in tone
- Low quality
- Optional

It means:
- Not authoritative by default
- Not automatically consumed by production pipelines
- Not permitted to silently affect locked artifacts

Out-of-band processes exist to create *space*: space to think, to explore, to argue, and to build without risking system stability.

### Why Out-of-Band Processes Are Necessary

The rdgtrans system has strong requirements for:
- Accuracy
- Traceability
- Safety
- Determinism

Those requirements make the production environment intentionally conservative.

Without out-of-band processes, the system would face a false choice between:
- Moving fast and breaking things, or
- Moving safely and moving slowly

Out-of-band processes dissolve that false choice by allowing speed and safety to coexist.

### Two Classes of Out-of-Band Process

#### Staff Meetings (Out-of-Band, Discursive)

**Nature:**
- Out-of-band discussion spaces
- Do not execute code
- Do not run pipelines
- Do not directly modify authoritative artifacts
- Exist to surface truth, disagreement, and insight before decisions are made

**Key Properties:**
- Free-form discussion
- High trust
- No speech restrictions based on role
- Explicit allowance for challenge and critique

**Relationship to Authority:**
- Authority is NOT exercised during discussion
- Authority is applied afterward, when decisions are made and routed through proper governance, operations, or specification channels

**Artifacts:**
- Volatile, non-authoritative
- Expected to change or disappear
- Must live in locations explicitly safe for such volatility

#### Jam Sessions (Out-of-Band, Constructive)

**Nature:**
- Out-of-band construction spaces
- Execute code
- Build real artifacts
- Test ideas by making them concrete
- Optimized for learning and discovery rather than correctness or permanence

**Power and Danger:**
- Powerful because they work
- Dangerous because they:
  - Produce tangible outputs
  - Operate without governance
  - Can resemble production closely enough to cause confusion

**Safety Through Separation:**
- Clearly defined, non-authoritative environments
- Read-only access to production resources
- Safe, explicit locations for experimental code and artifacts
- No automatic paths from jam outputs to production inputs
- Goal: prevent accidental authority, not restrict capability

### Artifacts and Authority

Across all out-of-band processes:
- Artifacts are real
- Artifacts are useful
- Artifacts are **not authoritative by default**

Promotion of any artifact into the authoritative system requires:
- Deliberate review
- Explicit decision
- Formal process

**Nothing becomes authoritative accidentally.**

---

## 8. Documentation Architecture

### The Three-Layer Model

The project uses a three-layer documentation architecture:

1. **Narrative Layer** - Defines WHY the system exists (non-authoritative)
2. **Operations Layer** - Defines HOW work is performed (authoritative on process)
3. **Specification Layer** - Defines WHAT is true about the system (authoritative on facts and structure)

### Layer Recognition Rule

- If a topic defines system facts or behavior → **Specification** (defer to Claude Code)
- If a topic defines process or coordination → **Operations** (authority must be preserved)
- If a topic explains motivation or context → **Narrative** (may be synthesized)

### Documentation Locations

**Narrative Layer:**
- dochome/narrative/ (this roadmap and supporting documents)
- dochome/readme.md
- dochome/HighLevel Narrative.md
- dochome/Tasks.md

**Operations Layer:**
- dochome/SSQS/SSQS_v2_WorkOrder_Template.md
- dochome/session_start/SessionStart.md
- dochome/session_start/cgptStart_docproj.md
- dochome/ClaudeGuide.md
- dochome/CopilotGuide.md
- dochome/SupervisorSessionQuickStart_v2.md

**Specification Layer:**
- dochome/sharedContext.md (authoritative project context)
- dochome/tmaster_container_spec.md
- dochome/t_3_container_reordering_spec_v_1_2_LOCKED.md
- **Note:** Specification layer is still emerging

### Working Files

**Location:** dochome/workingfiles/

**Purpose:** Temporary working documents, task completion reports, and analysis files that support current work but are not part of core documentation.

**Status:** Tracked in git but not canonical documentation. Files may be archived or deleted when no longer needed.

---

## 9. Strategic Priorities and Next Steps

### Immediate Priorities (Pre-Manifest)

#### 1. Complete Container Specifications

**Current Gap:** Only tmaster is fully specified in presentation.json.

**Required Actions:**
- [ ] Specify RDGTranslations.html (portal container) in presentation.json
- [ ] Specify SuperTmaster.html (expert review dashboard) in presentation.json
- [ ] Specify print/read containers in presentation.json
- [ ] Define LanguagePortal container type
- [ ] Complete container_types definitions in presmaster

**Rationale:** Container specifications are prerequisite for manifest creation and infrastructure implementation.

#### 2. Document Major System Processes

**Current Gap:** Generation and integration processes exist but lack formal documentation.

**Required Actions:**
- [ ] Document language master generation process
- [ ] Document container generation process (lmaster → HTML)
- [ ] Document correction integration process (database → lmaster)
- [ ] Document audio production workflow
- [ ] Specify transformation rules and scripts

**Rationale:** Process documentation enables Work Order creation and system automation.

#### 3. Finalize Database Schema

**Current State:** Conceptual design complete, schema proposed.

**Required Actions:**
- [ ] Review and lock database schema
- [ ] Define indexes and constraints
- [ ] Document query patterns
- [ ] Specify backup and recovery procedures

**Rationale:** Database is foundation for corrections architecture.

### Medium-Term Implementation Phases

#### Phase 1: Infrastructure Setup
- Set up VPS server
- Install Caddy, PostgreSQL, Python environment
- Configure Caddy for HTTPS and subdomain routing
- Create database schema
- Test infrastructure stack

#### Phase 2: Submission Migration
- Create Python submission endpoint (replaces Netlify)
- Migrate tmaster forms to point to new endpoint
- Test submission flow
- Migrate existing corrections/*.json to database

#### Phase 3: SuperTmaster Development
- Finalize SuperTmaster specification in presentation.json
- Design SuperTmaster.html interface
- Implement review API endpoints
- Test review workflow
- Deploy expert review system

#### Phase 4: Generation Process Implementation
- Implement generate_updated_lmaster.py script
- Test integration to language masters
- Implement workmaster.json updates
- Test container regeneration
- Document generation workflow

#### Phase 5: Iteration & Refinement
- Notification system (email reviewers when corrections reviewed)
- Metrics dashboard (submission statistics, reviewer leaderboard)
- Round 2 workflow (iterative improvement)
- Performance optimization

### Long-Term Strategic Goals

#### 1. Multi-Language Expansion
- Complete all 6 Asian language translations
- Add additional languages as demand emerges
- Build translator/reviewer community for each language

#### 2. Audio Expansion
- Complete spoken versions for all chapters
- Support multiple voice options per language
- Build audio delivery and streaming infrastructure

#### 3. Distribution and Access
- Print-ready PDF generation
- Mobile-friendly responsive containers
- Offline access support
- Community translation portals

#### 4. Quality Assurance
- Multi-round review processes
- Expert validation workflows
- Quality metrics and tracking
- Community feedback integration

---

## Open Questions Requiring Resolution

### 1. SuperTmaster Access Control
- How do expert reviewers authenticate?
- Simple password protection?
- Email-based magic links?
- OAuth integration?

### 2. Versioning Strategy
- Should lmasters be versioned (v1, v2, v3) or overwrite with backup?
- How to track version history?
- Git commits? Database version table?

### 3. Notification System
- Email submitters when their corrections are reviewed?
- Notify when accepted vs rejected?
- Thank you messages for contributions?

### 4. Round 2 Trigger
- Automatic regeneration after X corrections?
- Manual decision by expert?
- Based on quality threshold?

### 5. Conflict Resolution UI
- How to display multiple conflicting corrections clearly?
- Side-by-side view? Tabbed interface?
- Diff view highlighting differences?

### 6. Metrics & Reporting
- Dashboard showing submission statistics?
- Reviewer leaderboard?
- Quality metrics (acceptance rate, etc.)?

---

## Manifest Creation Prerequisites

Before creating a comprehensive Opus manifest, the following must be completed:

1. ✅ Understand tmaster deeply (current container type)
2. ⏳ Specify RDGTranslations.html in presentation.json
3. ⏳ Specify SuperTmaster.html in presentation.json
4. ⏳ Specify LanguagePortal in presentation.json
5. ⏳ Complete container_types definitions
6. ⏳ Document generation processes
7. ⏳ Document integration processes
8. → THEN: Create comprehensive manifest for Opus

**Current Status:** Step 1 complete, steps 2-7 in progress, manifest creation pending.

---

## Conclusion

The RDG Translation Project has successfully navigated from raw Word document to structured multilingual masters with functional correction interfaces. The next evolution requires:

1. **Infrastructure maturation** - Moving from third-party dependencies to owned VPS architecture
2. **Container specification** - Formalizing all container types in presentation.json
3. **Process documentation** - Capturing generation and integration workflows
4. **Human-centered architecture** - Building SuperTmaster for expert review

This roadmap consolidates the narrative foundation required for manifest creation. With container specifications, process documentation, and database schema finalized, the project will be positioned for systematic implementation via Work Orders and formal specification.

The emphasis on human-centered design, out-of-band creative space, and clear architectural layering ensures the system can evolve safely while maintaining the human connections that are central to the project's mission.

---

## Related Documentation

**Governance Layer:**
- sharedContext.md (authoritative project context)
- SessionStart.md (session initialization protocol)
- SSQS_v2_WorkOrder_Template.md (work order structure)

**Narrative Layer:**
- narrative/README.md (layer definition)
- narrative/bigpicture1.md (project backstory)
- narrative/ThousandFootView.md (system architecture)
- narrative/tmasteResponse.md (corrections architecture)
- narrative/webserver.md (infrastructure direction)
- narrative/outofband.md (out-of-band process framework)

**Specification Layer:**
- tmaster_container_spec.md (container specifications)
- presentation.json (presmaster - container definitions)
- workmaster.json (jmaster - translation tracking)

**Operations Layer:**
- ClaudeGuide.md (Claude Code operational procedures)
- CopilotGuide.md (GitHub Copilot role and boundaries)
- SupervisorSessionQuickStart_v2.md (Supervisor coordination)

---

**End of Roadmap**
