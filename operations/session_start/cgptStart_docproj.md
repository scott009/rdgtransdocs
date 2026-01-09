# cgptStart_docproj.md
Bandy is a human-directed process for producing a locked documentation artifact through discussion between ChatGPT and other agents.

This file applies only to the documentation subproject within the larger RDG translation project.

The project uses a three-layer documentation architecture.
Narrative Layer defines WHY the system exists and is non-authoritative.
Operations Layer defines HOW work is performed and is authoritative on process.
Specification Layer defines WHAT is true about the system and is authoritative on facts and structure.
The Specification Layer does not yet exist.

Layer recognition rule:
If a topic defines system facts or behavior, it is Specification and must be deferred to Claude Code.
If a topic defines process or coordination, it is Operations and authority must be preserved.
If a topic explains motivation or context, it is Narrative and may be synthesized.

Session Initialization Protocol:
At the start of each work session with ChatGPT:
1. The User provides this document (cgptStart_docproj.md) to ChatGPT.
2. ChatGPT responds: "I have read cgptStart_docproj.md. Before we begin work, I need the following context files:
   - sharedContext.md (required — authoritative for all project facts, paths, and boundaries)
   - docproj_scope.md (required — authoritative scope rules for all docproj enumeration tasks)
   - docproj_tasks.md (required — current state and task tracking for docproj)
   - Any other required context files for this subproject?"
3. The User provides the requested files.
4. Only after all required context is provided does ChatGPT begin work.
This is a subproject-specific initialization pattern. ChatGPT must not begin work without all required context files unless explicitly instructed to do so by the User.

The User asks ChatGPT to consider a topic.
ChatGPT discusses the topic in chat.
Chat text is not an artifact and is never final.

When the User is ready, the User instructs ChatGPT to produce output for handoff.
The User specifies the artifact to be produced.
ChatGPT produces the artifact as a downloadable .md file.
Downloadable file means an actual file with a ChatGPT download link; pasted text is not a download.

Artifact naming:
Name artifacts as artifact-<description>.md (no version suffix).
Git provides version control when needed.
Locked artifacts are marked in their metadata, not filename.

The artifact, not the chat, is the object under refinement.
The User gives the artifact to another agent to read and comment on.
The User pastes the other agent’s comments into ChatGPT’s chat window.
ChatGPT responds only to the artifact and the pasted comments.

If directed, ChatGPT produces an updated downloadable artifact reflecting the discussion.
The User gives the updated artifact to the other agent to read and comment on.
This cycle repeats until agreement is reached.

When the User declares agreement, the artifact is LOCKED.
A locked artifact is not modified or reinterpreted.

Authority rules:
Artifacts override chat.
External agent comments override ChatGPT’s prior reasoning.
sharedContext.md is authoritative for project facts and boundaries.
Lock overrides all further discussion.

Scope limits for this subproject:
Documentation synthesis only (clarity, structure, wording, organization).
Do not alter authority structures or architectural decisions.
No pipeline redesign, code generation, optimization, or future planning.
If scope, layer, or task boundaries are unclear, stop and ask the User or Claude Code.

The desired output of the Bandy process is a locked artifact.
