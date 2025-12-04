# Element List - tmasterThai.html
## Task 8, Step A.1

### Document: tmasterThai.html
**Analysis Date:** December 3, 2025
**Purpose:** Identify all UI text elements that require translation support

---

## CSS Classes Used

### Structural Classes
- `.reviewer-section` - Container for reviewer information section
- `.editor-info` - Container for editor name and email inputs
- `.paragraph-block` - Container for each paragraph/chapter entry
- `.heading-block` - Modifier class for chapter title blocks
- `.para-header` - Header section within paragraph blocks
- `.english-ref` - Container for English reference text
- `.thai-edit` - Container for Thai editable text
- `.comment` - Container for comment input

### Display Classes
- `.para-id` - Paragraph ID badge (e.g., "p3-1")
- `.chapter-num` - Chapter number badge
- `.modified-badge` - Badge showing "MODIFIED" status
- `.field-note` - Explanatory notes for form fields

### Other Classes
- `header` - Main page header
- `footer` - Sticky footer with submit button

---

## Translatable Text Elements

### 1. Page Header Section
| Element Type | Current English Text | Element Description | Suggested ID |
|--------------|---------------------|---------------------|--------------|
| `<h1>` | "Recovery Dharma - Thai Translation Correction Tool" | Main page title | `page_header` |

### 2. Reviewer Information Section
| Element Type | Current English Text | Element Description | Suggested ID |
|--------------|---------------------|---------------------|--------------|
| `<h2>` | "👤 About You" | Section heading | `section_heading` |
| `<p>` | "Please provide your information before starting the review. This helps us track contributions and contact you if needed." | Section description | `section_description` |
| `placeholder` | "Your Full Name *" | Name input placeholder | `full_name_field` |
| `placeholder` | "Your Email Address *" | Email input placeholder | `email_field` |
| `<label>` | "Tell us about yourself (optional):" | Bio field label | `bio_field_label` |
| `<p class="field-note">` | "Your background, qualifications, or relevant experience (e.g., \"Native Thai speaker\", \"Buddhist scholar\", \"Professional translator\")" | Bio field note | `bio_field_note` |
| `placeholder` | "Example: Native Thai speaker with 10 years translation experience. Studied Buddhist texts at university..." | Bio textarea placeholder | `bio_placeholder` |
| `<label>` | "Overall review notes (optional):" | Overall notes label | `overall_notes_label` |
| `<p class="field-note">` | "General observations about the entire translation" | Overall notes field note | `overall_notes_field_note` |
| `placeholder` | "Example: Overall quality is good. Found some inconsistent terminology in Chapter 24. Recommend second review for Buddhist technical terms..." | Overall notes placeholder | `overall_notes_placeholder` |

### 3. Chapter Title Block Elements
| Element Type | Current English Text | Element Description | Suggested ID |
|--------------|---------------------|---------------------|--------------|
| `<label>` | "English Chapter Title:" | English chapter title label | `english_title_label` |
| `<label>` | "Thai Chapter Title (editable):" | Thai chapter title label | `thai_title_label` |
| `<label>` | "Comment (optional):" | Comment label for chapters | `chapter_comment_label` |
| `placeholder` | "Notes about this chapter title" | Chapter comment placeholder | `chapter_comment_placeholder` |

### 4. Paragraph Block Elements
| Element Type | Current English Text | Element Description | Suggested ID |
|--------------|---------------------|---------------------|--------------|
| `<label>` | "English (reference):" | English paragraph label | `english_reference_label` |
| `<label>` | "Thai (editable):" | Thai paragraph label | `thai_editable_label` |
| `<label>` | "Comment (optional):" | Comment label for paragraphs | `paragraph_comment_label` |
| `placeholder` | "Notes or explanation for this correction" | Paragraph comment placeholder | `paragraph_comment_placeholder` |

### 5. Status and Control Elements
| Element Type | Current English Text | Element Description | Suggested ID |
|--------------|---------------------|---------------------|--------------|
| `.modified-badge` | "MODIFIED" | Badge shown when content is edited | `modified_badge` |
| `#download-btn` | "Submit" | Submit button text | `submit_button` |

### 6. Paragraph ID Display
| Element Type | Current English Text | Element Description | Suggested ID |
|--------------|---------------------|---------------------|--------------|
| `.para-id` | "Paragraph ID:" (implied label) | Label for paragraph ID badge | `paragraph_id_label` |

---

## Notes for Implementation

### Elements Already in presentation.json
The following elements are already defined in presentation.json:
- ✅ `pr_2`: `english_title_label`
- ✅ `pr_3`: `thai_title_label`
- ✅ `pr_4`: `comment_label`
- ✅ `pr_6`: `page_header`
- ✅ `pr_7`: `section_heading`
- ✅ `pr_8`: `full_name_field`
- ✅ `pr_9`: `email_field`
- ✅ `pr_10`: `bio_field`
- ✅ `pr_13`: `paragraph_id_label`
- ✅ `pr_14`: `english_reference_label`
- ✅ `pr_15`: `thai_editable_label`
- ✅ `pr_16`: `comment_label`

### Elements NOT Yet in presentation.json
The following elements need to be added to presentation.json:
- ❌ `section_description` - "Please provide your information..."
- ❌ `bio_field_label` - "Tell us about yourself (optional):"
- ❌ `bio_field_note` - "Your background, qualifications..."
- ❌ `bio_placeholder` - "Example: Native Thai speaker..."
- ❌ `overall_notes_label` - "Overall review notes (optional):"
- ❌ `overall_notes_field_note` - "General observations..."
- ❌ `overall_notes_placeholder` - "Example: Overall quality is good..."
- ❌ `chapter_comment_placeholder` - "Notes about this chapter title"
- ❌ `paragraph_comment_placeholder` - "Notes or explanation for this correction"
- ❌ `modified_badge` - "MODIFIED"
- ❌ `submit_button` - "Submit"

### Observations
1. **Duplicate Labels**: The `comment_label` ("Comment (optional):") appears in both chapter and paragraph blocks with the same text
2. **Placeholders vs Labels**: Some fields have both labels and placeholders that need translation
3. **Field Notes**: The `.field-note` class elements provide helpful context and should be translated
4. **Consistency**: The presentation.json structure uses short IDs (pr_2, pr_3, etc.) with descriptive names

### Recommendations for Step A.2
1. Add missing elements to presentation.json with new pr_* IDs (starting from pr_27)
2. Ensure all placeholders are included as they provide important user guidance
3. Consider separating chapter_comment and paragraph_comment labels if different translations are needed
4. Add translations for all target languages (Thai, Japanese, Korean, Simplified Chinese, Traditional Chinese, Vietnamese)

---

## Summary Statistics
- **Total CSS Classes Identified:** 16
- **Total Translatable Elements:** 27
- **Elements in presentation.json:** 12
- **Elements to Add:** 15
