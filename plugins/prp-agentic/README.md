# PRP Framework

A minimal, language-agnostic framework for AI-assisted development using Product Requirement Prompts (PRPs).

## What is a PRP?

A **Product Requirement Prompt** (PRP) is a structured document that provides an AI assistant with all the context needed to implement a feature correctly on the first pass. Unlike traditional PRDs, PRPs include:

- Specific file paths and code patterns from your codebase
- Implementation steps with pseudocode
- Executable validation commands
- Known gotchas and edge cases
- Progress tracking via Implementation Log

## Installation

```bash
# Step 1: Add the marketplace
/plugin marketplace add sebastiandelaroche/sdlr-claude-plugins

# Step 2: Install the plugin
/plugin install prp-agentic

# Step 3: Initialize project structure
/prp-init
```

This will:
1. Add the PRP marketplace to Claude Code
2. Install all PRP slash commands (`/prp-*`)
3. Create the folder structure (`PRPs/`) and download templates

## Setup

After installation:

1. **Edit `CLAUDE.md`** - Fill in your project's specific details:
   - Project name and description
   - Language and framework
   - Commands for dev, test, lint
   - Code conventions
   - Directory structure

2. **Configure Slack Notifications** (optional):
   ```bash
   export SLACK_WEBHOOK_URL="https://hooks.slack.com/services/YOUR/WEBHOOK/URL"
   ```

3. **Add to `.gitignore`** (optional):
   ```
   # If you don't want to track research/reviews
   PRPs/research/
   PRPs/reviews/
   ```

## Commands

| Command | Description |
|---------|-------------|
| `/prp-init` | Initialize PRP framework in current project |
| `/prp-research [topic]` | Research a topic, documentation, or codebase area |
| `/prp-create [feature]` | Create a PRP for a new feature |
| `/prp-verify [prp-file]` | Verify a PRP is complete and ready for implementation |
| `/prp-implement [prp-file]` | Implement a feature following an approved PRP |
| `/prp-test [target]` | Run validation and tests |
| `/prp-review [scope]` | Review code changes |

## Workflow

### Standard Flow

```
┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐     ┌─────────────┐
│  Research   │ ──▶ │   Create    │ ──▶ │   Verify    │ ──▶ │  Implement  │ ──▶ │    Test     │ ──▶ │   Review    │
│  (optional) │     │    PRP      │     │    PRP      │     │             │     │             │     │             │
└─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘     └─────────────┘
```

### PRP Status Lifecycle

```
Draft  →  Approved  →  In Progress  →  Implemented
  ↑          ↑              ↑              ↑
  │          │              │              │
create    verify       implement      implement
                        (start)       (complete)
```

### Example: Adding User Authentication

**1. Research (optional)**
```
/prp-research OAuth 2.0 best practices for Node.js
```
Creates `PRPs/research/oauth-2-best-practices.md` with findings.

**2. Create PRP**
```
/prp-create user authentication with OAuth
```
Creates `PRPs/user-authentication.md` with Status: `Draft`.

**3. Verify PRP**
```
/prp-verify user-authentication.md
```
Validates the PRP is complete. Updates Status to: `Approved`.

**4. Implement**
```
/prp-implement user-authentication.md
```
Builds the feature. Updates Status to: `In Progress` then `Implemented`.

**5. Test**
```
/prp-test user-authentication.md
```
Runs all validation commands from the PRP.

**6. Review**
```
/prp-review staged
```
Reviews the implementation for quality and security.

## Directory Structure

After running `/prp-init`, your project will have:

```
your-project/
├── PRPs/
│   ├── templates/
│   │   └── prp-template.md   # PRP template
│   ├── research/             # Research outputs
│   ├── reviews/              # Code review reports
│   └── feature-a.md          # Your PRPs go here
└── CLAUDE.md                 # Project context (edit this!)
```

> **Note:** Slack notifications are handled automatically by the plugin - no scripts are copied to your project.

## Features

### Automatic Status Updates

Commands automatically update the PRP's Status field:
- `/prp-create` sets Status to `Draft`
- `/prp-verify` (on pass) sets Status to `Approved`
- `/prp-implement` (on start) sets Status to `In Progress`
- `/prp-implement` (on complete) sets Status to `Implemented`

### Progress Tracking

Each PRP includes an Implementation Log that tracks:
- When implementation started
- Steps completed
- When implementation finished

### ACTION REQUIRED Notifications

Every command ends with an "ACTION REQUIRED" section that tells you:
- What the command accomplished
- What you need to do next
- Which command to run next

### Slack Notifications

Get notified when:
- Research is complete
- PRP is created or updated
- Code review is finished

**Setup:**
```bash
# Create a Slack Incoming Webhook at https://api.slack.com/messaging/webhooks
export SLACK_WEBHOOK_URL="https://hooks.slack.com/services/YOUR/WEBHOOK/URL"
```

### Optional Research Linking

PRPs can optionally reference research files:
- If research files are listed, `/prp-verify` validates they exist
- `/prp-implement` only reads the specific research files listed
- If no research listed, that's fine - the section is optional

## Customization

### Modify Template

Edit `PRPs/templates/prp-template.md` to add:
- Project-specific sections
- Required fields for your team
- Custom validation requirements

### Project Context

`CLAUDE.md` is a **template** that you fill in for each project. It provides AI with:
- Project structure and conventions
- Available commands (test, lint, build)
- Code style guidelines
- Common gotchas

Example:
```markdown
## Commands Reference

### Testing
npm test           # Run all tests
npm run test:cov   # Run with coverage

### Linting
npm run lint       # ESLint
npm run typecheck  # TypeScript
```

## Best Practices

1. **Always fill in CLAUDE.md** - The more context, the better the AI output
2. **Verify before implementing** - Run `/prp-verify` to catch issues early
3. **Keep PRPs focused** - One feature per PRP
4. **Use research for unknowns** - When you're not sure how to approach something
5. **Run tests after implementation** - Don't skip validation
6. **Track progress** - The Implementation Log helps resume interrupted work

## Requirements

- [Claude Code](https://claude.ai/code) CLI with slash command support
- Git (for review commands)

## License

MIT
