---
name: "CodeGrow"
description: "AI Engineering Asset & Growth System. Documents requirements, decisions, skills, and generates growth reports. MUST invoke for summarizing work, extracting skills, or recording progress."
---

# CodeGrow: AI Engineering Asset & Growth System

CodeGrow transforms your development process into engineering assets and personal growth records. It analyzes your work to extract reusable skills, document decisions, and track your engineering journey.

**IMPORTANT: All generated content (records, skills, reports, context summaries) MUST be written in the same language as the user's input.**

## Core Functions

1.  **Capture Development Records**: Document requirements, technical solutions, architecture, and pitfalls locally.
2.  **Abstract Reusable Skills**: Identify and extract reusable patterns (algorithms, strategies, patterns) into standalone skill documents.
3.  **Generate Growth Reports**: Assess developer growth and write reports to Lark Cloud Docs (Preferred) or local files.
4.  **Maintain AI Context**: Summarize AI conversations in `.codegrow/context/` to provide historical context for future AI development sessions.
5.  **Enforce Quality via Git Hooks**: Ensure daily growth reports are generated before pushing code.

## Workflow

When you invoke this skill, follow these steps sequentially:

### 1. Initialize & Verify (MANDATORY FIRST STEP)
Check if `.codegrow/` structure exists and is fully configured.

- **Directory Check**: Ensure the following exist:
  - `.codegrow/records/` (Development logs)
  - `.codegrow/skills/` (Reusable engineering skills)
  - `.codegrow/context/` (AI conversation summaries)
  - `.codegrow/reports/` (Local backup for growth reports)
  - `.codegrow/hooks/` (Git hooks scripts)
  - `.codegrow/scripts/` (Utility scripts)

- **Git Hook Installation (CRITICAL)**:
  1.  **Check**: Verify if `.git/hooks/pre-push` exists and contains CodeGrow logic.
  2.  **Create Script**: If missing, create `.codegrow/hooks/pre-push.js` to check for today's report.
  3.  **Create Installer**: Create `.codegrow/scripts/install_hooks.js` to symlink/copy the hook.
  4.  **Install**: **IMMEDIATELY RUN** `node .codegrow/scripts/install_hooks.js`.
  5.  **Configure package.json**: If `package.json` exists, check for `"postinstall": "node .codegrow/scripts/install_hooks.js"`. If missing, add it to ensure future team members get the hook automatically.

### 2. Analyze Context
Review the current session, recent file changes, and any `git diff`. Identify:
- What feature was developed?
- What technical decisions were made?
- Are there reusable patterns?

### 3. Generate Record (Local)
Create a new file in `.codegrow/records/YYYY-MM-DD_<feature_name>.md`.
- **Content**: Requirement, Implementation, Technical Solution (Mermaid supported), Pitfalls, Skills.

### 4. Save AI Context (Local)
Create or append to `.codegrow/context/YYYY-MM-DD_AI_Summary.md`.
- **Content**: Summary, Key Decisions, Future Context.

### 5. Extract/Update Skills (Local)
If a reusable pattern is identified:
- Create or update `.codegrow/skills/<skill-name>.md`.
- **Content**: Goal, Core Strategy, Implementation, Usage, Evolution.

### 6. Generate Growth Report (Mandatory)
1.  **Analyze Growth**: Evaluate complexity, decisions, and new skills.
2.  **Prepare Content**: Engineering Growth, Skill Acquisition, Suggestions.
3.  **Cloud Integration (Lark/Feishu)**:
    - Check if `feishu-mcp` is available.
    - **IF AVAILABLE**: Ask for Folder Token/Doc ID -> Create/Update Doc.
    - **IF NOT**: Fallback to local file `.codegrow/reports/YYYY-MM-DD_Growth_Report.md` and remind user to connect Lark.

## Commands
- `Summarize`: Perform the full workflow.
- `Finalize`: Aggregate records into a final project report.
- `Extract`: Focus only on extracting reusable skills.
- `Install`: Force re-installation of Git hooks.