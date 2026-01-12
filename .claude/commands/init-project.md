---
description: Initialize Project
---

# Initialize PIV Loop System

Set up the PIV (Prime-Implement-Validate) development workflow infrastructure with **fully populated reference files** for fast, consistent development.

## Overview

This command does NOT just check if files exist - it **generates and validates content** to ensure:
- Reference files contain actual, useful context from the codebase
- Architecture documentation reflects the real project structure
- Component and hook libraries are documented for reuse
- API patterns are captured from existing code
- All templates are ready for immediate use

---

## STEP 1: Create Directory Structure

Create all required directories:

```bash
mkdir -p .claude/history .claude/reference .agents/plans
touch .claude/history/.gitkeep .agents/plans/.gitkeep
```

Required structure:
```
.claude/
├── PRD.md                    # Product Requirements Document (Source of Truth)
├── INIT.md                   # Initialization guide
├── PRD-template.md           # Template for creating PRDs
├── history/                  # Session logs for continuity
│   └── .gitkeep
├── reference/                # **AUTO-GENERATED** context files
│   ├── _methodology.md       # PIV Loop methodology
│   ├── _architecture.md      # Project architecture (auto-generated)
│   ├── _components.md        # Component library reference (auto-generated)
│   ├── _hooks.md             # Hooks reference (auto-generated)
│   ├── _api-patterns.md      # API patterns reference (auto-generated)
│   └── _tech-stack.md        # Technology stack (auto-generated)
└── commands/                 # Slash commands

.agents/
└── plans/                    # Implementation plans storage
    └── .gitkeep
```

---

## STEP 2: Generate Reference Files

**CRITICAL**: Do not skip this step. Each reference file must contain ACTUAL content from the codebase.

### 2.1 Generate `_architecture.md`

Scan the codebase and create `.claude/reference/_architecture.md` with:

```markdown
# Project Architecture Reference

> Auto-generated on [DATE]. Re-run `/init-project` to update.

## Directory Structure

[Scan and document the actual src/ or app/ directory structure]

## Key Directories

| Directory | Purpose | Key Files |
|-----------|---------|-----------|
| [path] | [description] | [important files] |

## Architecture Patterns

### Routing
[Document the routing approach - Next.js App Router, Pages Router, etc.]

### Data Flow
[Document how data flows - API routes, server actions, etc.]

### State Management
[Document state management approach - React Query, Zustand, Redux, etc.]

## Module Dependencies

[Key module relationships and import patterns]
```

**To generate**:
1. Run `find src -type d -maxdepth 3` or equivalent
2. Identify key patterns from file structure
3. Document actual architecture decisions visible in code

### 2.2 Generate `_components.md`

Scan components directory and create `.claude/reference/_components.md`:

```markdown
# Component Library Reference

> Auto-generated on [DATE]. Re-run `/init-project` to update.

## UI Components (Base/Atomic)

| Component | Path | Props | Usage |
|-----------|------|-------|-------|
| [Name] | [path] | [key props] | [when to use] |

## Feature Components

| Component | Path | Purpose |
|-----------|------|---------|
| [Name] | [path] | [description] |

## Layout Components

| Component | Path | Purpose |
|-----------|------|---------|
| [Name] | [path] | [description] |

## Component Patterns

### Standard Props Pattern
[Document common prop patterns used across components]

### Composition Pattern
[Document how components are composed]

## Reusable Component Examples

[Include 2-3 examples of well-structured components from the codebase]
```

**To generate**:
1. Glob for `components/**/*.tsx` or similar
2. Extract component names and categorize
3. Document key props from interfaces

### 2.3 Generate `_hooks.md`

Scan hooks directory and create `.claude/reference/_hooks.md`:

```markdown
# Hooks Reference

> Auto-generated on [DATE]. Re-run `/init-project` to update.

## Data Fetching Hooks

| Hook | Purpose | Returns | Example |
|------|---------|---------|---------|
| [name] | [description] | [return type] | [usage example] |

## UI/State Hooks

| Hook | Purpose | Returns |
|------|---------|---------|
| [name] | [description] | [return type] |

## Utility Hooks

| Hook | Purpose | Returns |
|------|---------|---------|
| [name] | [description] | [return type] |

## Hook Patterns

### Query Hook Pattern
[Document the standard pattern for data fetching hooks]

### Mutation Hook Pattern
[Document the standard pattern for mutation hooks]

## Creating New Hooks

[Guidelines based on existing patterns in the codebase]
```

**To generate**:
1. Glob for `hooks/**/*.ts` or `**/use*.ts`
2. Extract hook names and signatures
3. Document return types and usage patterns

### 2.4 Generate `_api-patterns.md`

Scan API routes and create `.claude/reference/_api-patterns.md`:

```markdown
# API Patterns Reference

> Auto-generated on [DATE]. Re-run `/init-project` to update.

## API Route Structure

[Document the API directory structure]

## Standard API Route Template

\`\`\`typescript
// Standard pattern extracted from existing routes
[Include actual code pattern from the codebase]
\`\`\`

## Authentication Pattern

[Document how auth is handled in API routes]

## Validation Pattern

[Document how request validation is done - Zod schemas, etc.]

## Error Handling Pattern

[Document standard error handling approach]

## Response Format

\`\`\`typescript
// Standard response format
[Document actual response patterns]
\`\`\`

## Existing Endpoints

| Method | Endpoint | Purpose |
|--------|----------|---------|
| [GET/POST/etc] | [path] | [description] |
```

**To generate**:
1. Glob for `api/**/*.ts` or `app/api/**/route.ts`
2. Extract common patterns from routes
3. Document authentication, validation, error handling approaches

### 2.5 Generate `_tech-stack.md`

Analyze package.json and create `.claude/reference/_tech-stack.md`:

```markdown
# Technology Stack Reference

> Auto-generated on [DATE]. Re-run `/init-project` to update.

## Core Framework

| Technology | Version | Purpose |
|------------|---------|---------|
| [name] | [version] | [purpose] |

## Frontend Libraries

| Library | Version | Usage |
|---------|---------|-------|
| [name] | [version] | [how it's used] |

## Backend Libraries

| Library | Version | Usage |
|---------|---------|-------|
| [name] | [version] | [how it's used] |

## Development Tools

| Tool | Version | Purpose |
|------|---------|---------|
| [name] | [version] | [purpose] |

## Key Configurations

### TypeScript Config
[Key tsconfig settings]

### Build Config
[Key build/bundler settings]

### Linting/Formatting
[ESLint, Prettier configs]

## Environment Variables

| Variable | Required | Purpose |
|----------|----------|---------|
| [name] | [yes/no] | [description] |
```

**To generate**:
1. Parse package.json dependencies
2. Check for config files (tsconfig.json, etc.)
3. Document environment variables from .env.example

---

## STEP 3: Verify `_methodology.md` Content

Ensure `.claude/reference/_methodology.md` exists with complete PIV Loop documentation.

**Required sections**:
- Introduction and Philosophy
- The Three Phases (Prime, Implement, Validate)
- Document Types (PRD, Session Logs, Plans)
- Workflow Patterns
- Quality Gates
- Anti-Patterns to Avoid

If missing or incomplete, create with full methodology content.

---

## STEP 4: Initialize PRD

Check if `.claude/PRD.md` exists:

**If missing**:
- Inform user that PRD is required
- Suggest running `/create-prd` after discussing requirements
- Or manually create from `.claude/PRD-template.md`

**If exists**:
- Verify it has required sections (Executive Summary, User Stories, etc.)
- Check for stale content (last updated date)
- Report status to user

---

## STEP 5: Create Session Log

Create initial session log at `.claude/history/[DATE]-session-1.md`:

```markdown
# Session Log: [DATE] Session 1

## Session Context
- **Focus**: PIV Loop System Initialization
- **PRD Reference**: [Status of PRD]
- **Previous Session**: None (first tracked session)

## Initialization Results

### Directory Structure
- [x] .claude/history/ created
- [x] .claude/reference/ created
- [x] .agents/plans/ created

### Reference Files Generated
- [x] _architecture.md - [status]
- [x] _components.md - [status]
- [x] _hooks.md - [status]
- [x] _api-patterns.md - [status]
- [x] _tech-stack.md - [status]
- [x] _methodology.md - [status]

### PRD Status
- [PRD status and any actions needed]

## Next Steps
- [ ] Review generated reference files for accuracy
- [ ] Create/update PRD if needed
- [ ] Run `/core_piv_loop:prime` to start first development session
```

---

## STEP 6: Update CLAUDE.md Reference

Ensure CLAUDE.md references the new reference files:

```markdown
### Key Reference Files
| File | Purpose |
|------|---------|
| `.claude/PRD.md` | Product Requirements Document |
| `.claude/reference/_architecture.md` | Project architecture |
| `.claude/reference/_components.md` | Component library |
| `.claude/reference/_hooks.md` | Hooks reference |
| `.claude/reference/_api-patterns.md` | API patterns |
| `.claude/reference/_tech-stack.md` | Technology stack |
```

---

## Output Summary

After initialization, display:

```
## PIV Loop Initialization Complete

### Reference Files Generated
| File | Status | Content |
|------|--------|---------|
| _architecture.md | [Created/Updated] | [X directories, Y patterns documented] |
| _components.md | [Created/Updated] | [X components documented] |
| _hooks.md | [Created/Updated] | [X hooks documented] |
| _api-patterns.md | [Created/Updated] | [X endpoints, Y patterns documented] |
| _tech-stack.md | [Created/Updated] | [X dependencies documented] |
| _methodology.md | [Verified] | PIV Loop methodology |

### PRD Status
[PRD status - exists/missing, sections verified]

### Next Steps
1. Review generated reference files for accuracy
2. [Create PRD if missing]
3. Run `/core_piv_loop:prime` to start development

### Quick Commands
- `/core_piv_loop:prime` - Start session with full context
- `/core_piv_loop:plan-feature` - Plan a new feature
- `/validation:validate` - Run project validation
```

---

## Maintenance

Re-run `/init-project` periodically to:
- Update reference files with new components/hooks/patterns
- Refresh architecture documentation after major changes
- Ensure all reference files stay current

---

## Notes

- Reference files are **context for Claude**, not user documentation
- They should be concise and actionable
- Focus on patterns and reusability
- Include actual code examples from the codebase
- Keep files under 500 lines for optimal context usage
