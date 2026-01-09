# ThousandFootView


At the higest level the system consists of entities, processes and artifacts 
## System Motivation
System motavation is interesting  but is left unspecified for now.  It is a dicussion of the "why" of the system. Why we are creating and why someone might want to use it.   

## System Goal
- The purpose of the system is to produce certain arifacts. 

## Entities
- entities produce artifacts via processes and artifacts
## Types of entities
### Humans
- different humans perform different roles. A single human may perform different roles at different times and in different processes 

### Agents
- Agents are usually AI based.  
- Agents exist within Environments  
- Agents are backed by models.  A single agent can utilize different Models 
- Agent's can assume differnt roles. The role is based on the strengths and limitations of both the Agent's model(s) and the environrment the agent functions within. 
#### Current Agents
##### ChatGPT
##### Claude
##### Gemini
 
## Process
- processes are the things we do to produce artifacts.  (And as vague as this seems, fleshing this out is the function I am adressing right now )

## Artifacts

Artifacts are the tangible outputs and inputs of the system. They can be classified by their purpose and role in the system.

### Artifact Classification

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

**Location: projhome/lmasters/**
- \\wsl$\Ubuntu\home\scott\gitrepos\rdgtrans\lmasters\RDGBook_English.md (authoritative English source)
- \\wsl$\Ubuntu\home\scott\gitrepos\rdgtrans\lmasters\RDGBook_Korean.md (Korean translation)

#### Container Artifacts
*Presentation layer - wraps and displays content to end users*

**Location: showoff/docs/**
Showoff path
- C:\Users\scott\Documents\RecoveryDharma\RDGBook\output_V1\docs\

**RDGTranslations.html**
- Portal/Index Container - Entry point for the entire project
- Organizes and presents project overview, audio introductions, and navigation
- Contains links to all translation masters (tmasterThai, tmasterJapanese, etc.)
- Acts as the presentation portal for all other container artifacts

**tmasterThai.html**
- Form Container - Thai translation correction form
- Linked from RDGTranslations.html portal
- 
- Presents Thai translation content (from RDGBook_Thai.md) for human review and correction
-   This is incomplete.  It also presents content from the English version  - this is deeply important  
- Bilingual web form with 45 chapter titles + 351 paragraphs  
- Allows reviewers to submit corrections back to the system
    And we are going to need to look at this very closely  
  
- Specified in presentation.json under container_types.tmaster
  YeS  great catch Becuase I think this is the ONLY container type in presmaster right now 


**rdgJapanesePrint.html**
**rdgVietnamese.html**

**ada3.css (styling)**

#### Configuration Artifacts
*Define structure, track state, configure system behavior*

**Location: projhome/**
- /home/scott/gitrepos/rdgtrans/presentation.json (presmaster - presentation layer config)
- /home/scott/gitrepos/rdgtrans/workmaster.json (jmaster - translation tracking metadata)

#### Governance Artifacts
*Define rules, boundaries, and protocols for system operation*

**Location: dochome/**
- C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations\sharedContext.md (authoritative project context)
- C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations\SSQS\SSQS_v2_WorkOrder_Template.md (work order structure)
- C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations\session_start\cgptStart_docproj.md (session initialization)

#### Specification Artifacts
*Technical requirements, constraints, and transformation rules*

**Location: dochome/**
- C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations\tmaster_container_spec.md (container specifications)
- C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations\t_3_container_reordering_spec_v_1_2_LOCKED.md (transformation spec)

#### Process Artifacts
*Scripts and tools that transform, process, or initialize*

**Location: projhome/scripts/ and projhome/py/**
- \\wsl$\Ubuntu\home\scott\gitrepos\rdgtrans\scripts\read_docs.sh (initialization script)
- \\wsl$\Ubuntu\home\scott\gitrepos\rdgtrans\scripts\fix_inquiry_headings.py (content processing)

#### Operational Artifacts
*Task tracking, work coordination, session management*

**Location: dochome/operations/**
- C:\Users\scott\Documents\AIProjects\Markdown\RDGTranslations\operations\docproj_tasks.md (task tracking)  



