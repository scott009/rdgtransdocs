# RDG Translation Project - Progress Log

## Session: 2025-11-26

### Completed

1. **Reorganization Planning**
   - Established new project home: `/home/scott/gitrepos/rdgtrans/`
   - Defined new folder structure with `lmasters/` for language files
   - Identified dochome for documentation: `C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations`

2. **Path Updates**
   - Updated all 7 language local paths in `workmaster.json`
   - Changed from: `/home/scott/gitrepos/RDGAsianMD/workmasters`
   - Changed to: `/home/scott/gitrepos/rdgtrans/lmasters`
   - Languages updated: English, Thai, Vietnamese, Japanese, Korean, Simplified Chinese, Traditional Chinese

3. **Documentation Created**
   - `projspec.md` - Comprehensive project specification
   - `PROGRESS.md` - This file
   - Covers: structure, data flow, status tracking system, path references

4. **Utilities Created**
   - `read_docs.sh` - Script to list and prompt reading documentation files
   - Location: `/home/scott/gitrepos/rdgtrans/read_docs.sh`

5. **Understanding Established**
   - workmaster.json role as central tracking/metadata file (does NOT contain translations)
   - Language .md files in lmasters/ contain actual translation text
   - Status tracking system with codes 0-4 (empty → exists → suspect → corrected → accepted)
   - English master as authoritative source of truth

6. **Git Repository Setup**
   - Initialized and configured three git repositories:
     - **rdgtrans**: Main translation project at `/home/scott/gitrepos/rdgtrans/`
       - Remote: https://github.com/scott009/rdgtrans
       - Contains: workmaster.json, lmasters/, utility scripts
       - Added archive/ to .gitignore
       - Updated read_docs.sh to cd into project directory
     - **rdgtransdocs**: Documentation at dochome
       - Remote: https://github.com/scott009/rdgtransdocs
       - Contains: Opguide.md, PROGRESS.md, projspec.md, functions.md
     - **showoff**: Output files at winoutput
       - Remote: https://github.com/scott009/showoff
       - Contains: HTML/PDF translations, audio files
   - All repositories initialized, committed, and pushed to GitHub
   - All repositories on master branch with tracking configured

7. **GitHub Pages Setup**
   - Configured showoff repository to serve static HTML/CSS files via GitHub Pages
   - Renamed `Web/` folder to `docs/` to enable GitHub Pages hosting
   - Configured Pages to deploy from master branch `/docs` folder
   - Site successfully deployed and accessible at: https://scott009.github.io/showoff/
   - All translation HTML files (Thai, Vietnamese, Japanese, Korean, Chinese) now publicly accessible
   - CSS stylesheet (ada3.css) properly served with HTML files

### Postponed for Later

- Custom domain configuration for GitHub Pages (optional enhancement)

- Remote URI updates in workmaster.json data_sources
- Python utility scripts adaptation for new structure
- Translation workflow automation
- Status update workflows

### Current State

- **workmaster.json**: Updated with correct local paths, ready to use
- **lmasters/**: Contains 7 language .md files in correct location
- **Documentation**: Up to date with current structure
- **Old location**: `/home/scott/gitrepos/RDGAsianMD/workmasters` - still exists but not in use

### Notes

- User has broader context not yet shared
- Keeping files small and focused
- inquirycircle directory is separate project - do not modify

### Next Session

Ready to continue with next phase of reorganization when additional context is provided.

---

## Session: 2025-11-27

### Completed - Task 1: HTML Semantic Structure Optimization

1. **English Version (rdgBook2.html)**
   - Created semantic HTML version with proper heading hierarchy
   - Changed book title to `<h1>` (was `<h2>`)
   - Removed 225 misused `<h3 class="id-tag">` elements
   - Added proper `id` attributes to all 225 paragraphs
   - Converted 5 inquiry headings from `<p>` to `<h4>` (Five Precepts)
   - Final structure: 1 H1, 30 H2, 14 H3, 5 H4
   - Committed to showoff repository: https://scott009.github.io/showoff/rdgBook2.html

2. **Thai Version (rdgThai2.html)**
   - Applied same semantic improvements as English version
   - Removed 351 misused `<h3 class="id-tag">` elements
   - Added proper `id` attributes to all 351 paragraphs
   - Converted 5 inquiry headings to `<h4>`
   - Final structure: 1 H1, 44 H2, 5 H4
   - **Fixed Table of Contents Navigation**
     - Converted TOC entries from `<p>` tags to `<a>` links
     - Created mapping from TOC text to chapter IDs (27 entries)
     - TOC navigation now fully functional
   - Committed to showoff repository: https://scott009.github.io/showoff/rdgThai2.html

3. **Python Utilities Created**
   - `fix_html_hierarchy.py` - Initial hierarchy fix for English
   - `fix_inquiry_headings.py` - Fix inquiry precept headings
   - `fix_html_semantic.py` - **Reusable script for all languages**
     - Fixes H1 hierarchy
     - Removes misused H3 id-tags
     - Adds proper paragraph IDs
     - Converts inquiry headings to H4
   - `fix_thai_toc.py` - Convert TOC paragraphs to links
   - `fix_thai_toc_mapping.py` - Map TOC links to chapter IDs
   - Location: `/home/scott/gitrepos/rdgtrans/py/`

4. **Accessibility Improvements**
   - Proper semantic HTML hierarchy: H1 → H2 → H3 → H4
   - Screen readers now see correct document outline
   - IDs properly associated with content elements
   - WAVE compliance testing performed
   - Confirmed subtitles using `role="doc-subtitle"` is semantically correct

### In Progress - Task 2: Translation Master Creation

**Next:** Create tmasterThai.html - bilingual Thai/English master document for translation review

### Notes

- WAVE accessibility checker works best with English documents
- TOC navigation required manual mapping due to text/ID mismatches in Thai
- Semantic structure improvements ready to apply to remaining languages (Vietnamese, Japanese, Korean, Chinese)
- All Python scripts are reusable for future language processing

---

**Last Updated:** 2025-11-27
