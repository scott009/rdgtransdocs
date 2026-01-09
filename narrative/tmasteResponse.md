# tmaster Response: Human-Centered Corrections Architecture

**Date:** 2025-12-27
**Context:** Discussion about deprecating Netlify submission system and designing new VPS-based corrections architecture

---

## The Problem: Current Netlify System (To Be Deprecated)

### Current Flow
```
User fills tmasterThai.html
  → Clicks Submit
  → JSON to GitHub via Netlify function
  → Each submission = separate JSON file in corrections/
  → ??? (processing unclear)
```

### Issues
1. **Cost:** Netlify free tier exhausted
2. **Infrastructure:** No control, third-party dependency
3. **Persistence:** No proper database
4. **Processing:** 6-step workflow exists on paper but unclear if automated or manual
5. **Conflict resolution:** Undefined - what happens when multiple reviewers submit different corrections for same paragraph?
6. **Integration:** How do corrections get back into language masters (lmasters/RDGBook_Thai.md)?

### Current Processing Workflow (from README)
1. Review new submissions
2. Quality verification
3. Apply corrections to language markdown files in `/lmasters/`
4. Update workmaster.json tracker
5. Regenerate HTML outputs
6. Archive processed files

**Critical insight:** This workflow affects multiple artifact types:
- Input: corrections/*.json (Operational artifacts)
- Updated: /lmasters/RDGBook_Thai.md (Content artifacts)
- Updated: workmaster.json (Configuration artifact)
- Regenerated: tmasterThai.html (Container artifacts)

---

## Core Design Principle: Human-Centered Architecture

### User's Guidance
> "These are deeply human processes and the human contacts are an important point of the process. It's crucial to understand the limits of what I want to automate."

**Key insight:** The database facilitates human decision-making, not replaces it.

### The "SuperTmaster" Concept
Instead of automating approval/integration, create a review dashboard where:
- Each submitted correction appears in a form
- Human reviewer can **Accept**, **Reject**, or **Modify**
- Database is updated based on human decisions
- On document acceptance, a new lmaster.md is generated (separate process)
- If desired, the second version can go through the tmaster process again (iterative improvement)

---

## New Architecture

### Infrastructure Stack

**VPS Server (user-owned):**
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

**Directory structure:**
```
/var/www/rdgtrans/
├── static/              # HTML containers
├── app/                 # Python application
├── scripts/             # Processing scripts
└── config/              # Caddy config, app config
```

---

## The Complete Human-Centered Workflow

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

---

## Database Schema

### Core Tables

```sql
-- Raw submission storage
CREATE TABLE submissions (
    id SERIAL PRIMARY KEY,
    language VARCHAR(50) NOT NULL,
    editor_name VARCHAR(255) NOT NULL,
    editor_email VARCHAR(255) NOT NULL,
    editor_bio TEXT,
    overall_notes TEXT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    total_items INTEGER,
    edited_items INTEGER,
    affected_chapters INTEGER[],
    status VARCHAR(50) DEFAULT 'pending',
    -- Status: pending, reviewed, archived
    raw_json JSONB NOT NULL  -- Full submission for audit
);

-- Individual correction entries (human workflow)
CREATE TABLE corrections (
    id SERIAL PRIMARY KEY,
    submission_id INTEGER REFERENCES submissions(id),
    paragraph_id VARCHAR(50) NOT NULL,
    chapter INTEGER NOT NULL,

    -- Three text versions
    original_text TEXT NOT NULL,           -- AI translation
    corrected_text TEXT NOT NULL,          -- Submitted correction
    final_text TEXT,                       -- After expert review/modification

    -- Comments
    submitter_comment TEXT,
    reviewer_comment TEXT,                 -- Expert's notes

    -- Review tracking
    reviewed_by VARCHAR(255),              -- Expert reviewer email
    reviewed_at TIMESTAMP,

    -- Workflow status
    status VARCHAR(50) DEFAULT 'submitted',
    -- Flow: submitted → reviewed → accepted/rejected → integrated

    created_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    integrated_at TIMESTAMP
);

-- Reviewer tracking
CREATE TABLE reviewers (
    id SERIAL PRIMARY KEY,
    email VARCHAR(255) UNIQUE NOT NULL,
    name VARCHAR(255),
    bio TEXT,
    is_expert BOOLEAN DEFAULT FALSE,       -- Expert reviewer flag
    first_submission TIMESTAMP,
    last_submission TIMESTAMP,
    total_submissions INTEGER DEFAULT 0,
    total_corrections INTEGER DEFAULT 0
);

-- Conflict tracking
CREATE TABLE correction_conflicts (
    id SERIAL PRIMARY KEY,
    paragraph_id VARCHAR(50) NOT NULL,
    language VARCHAR(50) NOT NULL,
    correction_ids INTEGER[] NOT NULL,      -- Array of conflicting correction IDs
    detected_at TIMESTAMP DEFAULT CURRENT_TIMESTAMP,
    resolved_at TIMESTAMP,
    resolution_method VARCHAR(100),         -- expert_review, merged, etc.
    winning_correction_id INTEGER REFERENCES corrections(id)
);

-- Processing workflow log
CREATE TABLE processing_log (
    id SERIAL PRIMARY KEY,
    submission_id INTEGER REFERENCES submissions(id),
    step VARCHAR(100) NOT NULL,             -- received, validated, reviewed, integrated
    status VARCHAR(50) NOT NULL,            -- success, failure, pending
    message TEXT,
    timestamp TIMESTAMP DEFAULT CURRENT_TIMESTAMP
);
```

---

## SuperTmaster Container Type

**Purpose:** Human review interface for submitted corrections

### Structure

```html
SuperTmaster.html
├── Header
│   └── "Correction Review Dashboard - Thai Language"
│
├── Expert Reviewer Info Section
│   ├── Sign in / authentication
│   └── Reviewer profile
│
├── Filters & Navigation
│   ├── Filter by status (submitted, reviewed, accepted, rejected)
│   ├── Filter by chapter
│   ├── Filter by submitter
│   ├── Filter by conflict status
│   └── Sort options
│
└── Correction Review Blocks (repeating for each correction)
    ├── Submission Metadata
    │   ├── Submitter name, email
    │   ├── Submitter bio
    │   ├── Submission timestamp
    │   └── Overall reviewer notes
    │
    ├── Paragraph Context
    │   ├── Paragraph ID (e.g., p_24_003)
    │   ├── Chapter number
    │   ├── English reference text (from RDGBook_English.md)
    │   └── Current Thai text (from lmaster)
    │
    ├── Submitted Correction
    │   ├── Original (AI translation)
    │   ├── Corrected (reviewer's submitted version)
    │   └── Submitter's comment/explanation
    │
    ├── Review Actions
    │   ├── [Accept] button
    │   │   └→ status = 'accepted'
    │   │   └→ final_text = corrected_text
    │   │
    │   ├── [Reject] button
    │   │   └→ status = 'rejected'
    │   │   └→ Optional: rejection reason
    │   │
    │   ├── [Modify] option
    │   │   └→ Editable text field
    │   │   └→ Save modified version to final_text
    │   │   └→ status = 'accepted'
    │   │
    │   └── Reviewer comment field (optional notes)
    │
    └── Conflict Indicator
        └── If multiple submissions exist for same paragraph_id,
            show side-by-side comparison
```

### Conflict Resolution in SuperTmaster

When multiple corrections exist for the same paragraph:
```
Conflict detected: 3 corrections for p_24_003
├── Correction A (submitted by Reviewer 1)
├── Correction B (submitted by Reviewer 2)
└── Correction C (submitted by Reviewer 3)

Expert reviewer sees side-by-side:
├── English reference
├── Current Thai text
├── Correction A with comment
├── Correction B with comment
└── Correction C with comment

Expert can:
├→ Accept one (others marked rejected)
├→ Merge elements from multiple (create final_text)
└→ Reject all (keep current text)
```

---

## Generation Process (Major System Process)

**Process name:** Generate Updated Language Master

**Trigger:** Human decision (expert clicks "Generate New Master" after reviewing corrections)

### Implementation

```python
# Python script: generate_updated_lmaster.py

def generate_updated_lmaster(language):
    """
    Human-triggered process to create new lmaster.md
    with all accepted corrections integrated.
    """

    # 1. Load current lmaster
    current_lmaster = f"lmasters/RDGBook_{language}.md"
    content = read_markdown(current_lmaster)

    # 2. Get all accepted, unintegrated corrections
    accepted = db.query("""
        SELECT paragraph_id, final_text, reviewer_comment, chapter
        FROM corrections
        WHERE status = 'accepted'
        AND integrated_at IS NULL
        AND language = %s
        ORDER BY chapter, paragraph_id
    """, (language,))

    # 3. Apply each correction
    correction_count = 0
    for correction in accepted:
        # Use final_text (expert-reviewed version, may be modified)
        success = replace_paragraph(
            content,
            correction.paragraph_id,
            correction.final_text
        )
        if success:
            correction_count += 1

    # 4. Version the new lmaster (or overwrite?)
    # Option A: Versioned
    version = get_next_version(language)
    new_file = f"lmasters/RDGBook_{language}_v{version}.md"

    # Option B: Overwrite with backup
    backup_current(current_lmaster)
    new_file = current_lmaster

    # 5. Write new lmaster
    write_markdown(new_file, content)

    # 6. Mark corrections as integrated
    db.execute("""
        UPDATE corrections
        SET status = 'integrated', integrated_at = NOW()
        WHERE id IN (%s)
    """, [c.id for c in accepted])

    # 7. Update workmaster.json
    update_workmaster(language, {
        'correction_count': correction_count,
        'last_updated': datetime.now(),
        'version': version
    })

    # 8. Log the generation
    log_generation(language, correction_count, new_file)

    return {
        'new_file': new_file,
        'corrections_applied': correction_count,
        'version': version
    }


def regenerate_tmaster_optional(language, new_lmaster):
    """
    Optional: Generate new tmaster.html from updated lmaster
    for Round 2 of review.
    """
    # Read new lmaster
    # Generate new tmaster HTML with updated content
    # Deploy to VPS static folder
    pass
```

---

## Iterative Improvement Workflow

```
ROUND 1
├── AI generates initial translations
├── Create tmasterThai.html (from RDGBook_Thai.md v1)
├── Reviewers submit corrections via tmaster
├── Database stores submissions
├── Expert reviews via SuperTmaster
├── Expert accepts/rejects/modifies corrections
└── Generate RDGBook_Thai.md v2

ROUND 2 (Optional)
├── Create tmasterThai.html (from RDGBook_Thai.md v2)
├── Reviewers review improved version
├── Submit additional corrections
├── Expert reviews via SuperTmaster
├── Generate RDGBook_Thai.md v3

ROUND N
└── Continue until quality threshold met
```

**Benefit:** Each iteration improves quality while maintaining human oversight at every decision point.

---

## Key Architectural Principles

### 1. Human Contact Preserved
- Expert reviewers see full submitter context (name, email, bio, notes)
- Can reach out to submitters for clarification
- Community building, not just data processing
- Submitters can be notified when their corrections are reviewed

### 2. Human Guidance at Decision Points
- Accept/Reject/Modify for each correction (not automated)
- Conflict resolution by human review (side-by-side comparison)
- When to generate new lmaster (human triggers, not automatic)
- Whether to do Round 2 review (human decision)

### 3. Database Supports, Doesn't Decide
- Tracks workflow status (submitted → reviewed → accepted → integrated)
- Detects conflicts (flags for human review)
- Stores all versions (original, corrected, final)
- Provides audit trail (who reviewed, when, what decision)
- Enables reporting and metrics

### 4. Clear Separation of Processes
- **Submission:** tmasterThai.html → database
- **Review:** SuperTmaster.html → human decisions → database updates
- **Generation:** Script reads accepted corrections → creates new lmaster
- **Regeneration:** Optional script creates new tmaster from new lmaster

---

## New Container Types Identified

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
   - Filtered view for specific language (e.g., Korean-only, Vietnamese-only)
   - Derived from RDGTranslations structure
   - To be specified before implementation

---

## Open Questions / Decisions Needed

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

## Next Steps

### Before Creating Opus Manifest:

1. ✅ Understand tmaster deeply (current container type)
2. ⏳ Specify RDGTranslations.html in presentation.json
3. ⏳ Specify SuperTmaster.html in presentation.json
4. ⏳ Specify LanguagePortal in presentation.json
5. ⏳ Complete container_types definitions
6. ⏳ Document generation processes
7. ⏳ Document integration processes
8. → THEN: Create comprehensive manifest for Opus

### Implementation Phases (for future Work Orders):

**Phase 1: Infrastructure Setup**
- Set up VPS server
- Install Caddy, PostgreSQL, Python environment
- Configure Caddy for HTTPS
- Create database schema

**Phase 2: Submission Migration**
- Create Python submission endpoint (replaces Netlify)
- Migrate tmaster forms to point to new endpoint
- Test submission flow
- Migrate existing corrections/*.json to database

**Phase 3: SuperTmaster Development**
- Specify SuperTmaster container in presentation.json
- Design SuperTmaster.html interface
- Implement review API endpoints
- Test review workflow

**Phase 4: Generation Process**
- Implement generate_updated_lmaster.py script
- Test integration to language masters
- Implement workmaster.json updates
- Test container regeneration

**Phase 5: Iteration & Refinement**
- Notification system
- Metrics dashboard
- Round 2 workflow
- Performance optimization

---

## Related Documentation

- **Current system:** corrections/README.md (Netlify-based, to be deprecated)
- **Governance:** sharedContext.md, SessionStart.md, SSQS_v2_WorkOrder_Template.md
- **Container specs:** tmaster_container_spec.md
- **Artifact classification:** narrative/ThousandFootView.md
- **Presentation config:** presentation.json (presmaster)

---

**Status:** Architecture design complete, awaiting decisions on open questions before proceeding to specification phase.
