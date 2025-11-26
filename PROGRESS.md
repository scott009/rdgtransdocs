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

### Postponed for Later

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

**Last Updated:** 2025-11-26
