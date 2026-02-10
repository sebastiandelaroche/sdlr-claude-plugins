---
description: Initialize PRP framework structure in current project
---

# Role: Project Initializer

## Your Task

Initialize the PRP (Product Requirement Prompts) framework in the current project by creating the folder structure and fetching template files.

## Process

### 1. Check Existing Structure

First, check if PRPs/ folder already exists:
- If exists: Warn user and ask if they want to continue (will overwrite templates)
- If not exists: Proceed

### 2. Create Folder Structure

Create the following directories:
```
PRPs/
├── templates/
├── research/
└── reviews/
```

### 3. Fetch Template Files

Download files from the PRP framework repository:

**PRP Template:**
```bash
curl -sL "https://raw.githubusercontent.com/sebastiandelaroche/sdlr-claude-plugins/main/plugins/prp-agentic/templates/prp-template.md" -o PRPs/templates/prp-template.md
```

**CLAUDE.md Template:**
```bash
curl -sL "https://raw.githubusercontent.com/sebastiandelaroche/sdlr-claude-plugins/main/plugins/prp-agentic/templates/CLAUDE.md" -o CLAUDE.md
```

### 4. Create .gitkeep Files

Create `.gitkeep` files in empty directories:
```bash
touch PRPs/research/.gitkeep
touch PRPs/reviews/.gitkeep
```

### 5. Verify Installation

Confirm all files were created successfully.

## Output

After initialization, display:

```
PRP Framework initialized successfully!

Created structure:
  PRPs/
  ├── templates/prp-template.md
  ├── research/
  └── reviews/
  CLAUDE.md

Next steps:
1. Edit CLAUDE.md with your project details
2. (Optional) For Slack notifications: export SLACK_WEBHOOK_URL="..."
3. Start using PRP commands:
   - /prp-research [topic]
   - /prp-create [feature]
   - /prp-verify [prp-file]
   - /prp-implement [prp-file]
   - /prp-test
   - /prp-review
```

## Guidelines

- Always check for existing files before overwriting
- If curl fails, provide manual instructions
