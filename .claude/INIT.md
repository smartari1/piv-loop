# PIV Loop System - Full Initialization Guide

This document provides comprehensive guidance for setting up and using the PIV (Prime-Implement-Validate) development workflow.

## What is the PIV Loop?

The PIV Loop is a structured development methodology designed for AI-assisted software development. It ensures:

1. **Context Continuity** - Every session builds on previous work
2. **Quality Assurance** - Validation gates at every step
3. **Alignment** - All work traces back to product requirements
4. **Traceability** - Decisions and changes are documented

## System Architecture

```
┌─────────────────────────────────────────────────────────────────────┐
│                         PIV LOOP SYSTEM                             │
├─────────────────────────────────────────────────────────────────────┤
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │                    SOURCE OF TRUTH                            │  │
│  │                                                               │  │
│  │  .claude/PRD.md ◄──────────────────────────────────────────┐ │  │
│  │  - Product vision          - User stories                  │ │  │
│  │  - Features                - Acceptance criteria           │ │  │
│  │  - Sprint focus            - Implementation status         │ │  │
│  └──────────────────────────────────────────────────────────────┘  │
│                          │                                     │    │
│                          ▼                                     │    │
│  ┌────────────┐    ┌────────────┐    ┌────────────┐           │    │
│  │   PRIME    │───▶│    PLAN    │───▶│  EXECUTE   │───────────┘    │
│  │            │    │            │    │            │                 │
│  │ Load PRD   │    │ Create     │    │ Implement  │                 │
│  │ Load hist. │    │ PRD-aligned│    │ Validate   │                 │
│  │ Check plans│    │ plan       │    │ Update PRD │                 │
│  └────────────┘    └────────────┘    └────────────┘                 │
│        │                 │                 │                        │
│        ▼                 ▼                 ▼                        │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │                    HISTORY TRACKING                           │  │
│  │                                                               │  │
│  │  .claude/history/YYYY-MM-DD-session-N.md                     │  │
│  │  - Work completed          - Decisions made                  │  │
│  │  - Issues encountered      - Files modified                  │  │
│  └──────────────────────────────────────────────────────────────┘  │
│                                                                     │
│  ┌──────────────────────────────────────────────────────────────┐  │
│  │                    PLANS STORAGE                              │  │
│  │                                                               │  │
│  │  .agents/plans/feature-name-YYYY-MM-DD.md                    │  │
│  │  - Implementation steps    - Technical decisions             │  │
│  │  - PRD references         - Validation criteria              │  │
│  └──────────────────────────────────────────────────────────────┘  │
│                                                                     │
└─────────────────────────────────────────────────────────────────────┘
```

## Directory Structure

```
project-root/
├── .claude/
│   ├── PRD.md                    # Product Requirements Document
│   ├── INIT.md                   # This file
│   ├── PRD-template.md           # Template for creating PRDs
│   ├── PIVLoopDiagram.png        # Visual workflow diagram
│   │
│   ├── history/                  # Session logs
│   │   ├── .gitkeep
│   │   ├── 2024-01-15-session-1.md
│   │   └── 2024-01-16-session-1.md
│   │
│   ├── reference/                # Methodology documentation
│   │   └── _methodology.md       # PIV Loop methodology guide
│   │
│   └── commands/                 # Slash commands
│       ├── init-project.md       # Initialize PIV system
│       ├── commit.md             # Git commit workflow
│       ├── create-prd.md         # Generate PRD from conversation
│       │
│       ├── core_piv_loop/        # Core workflow commands
│       │   ├── prime.md          # Load context
│       │   ├── plan-feature.md   # Create implementation plan
│       │   └── execute.md        # Execute with validation
│       │
│       ├── validation/           # Quality gates
│       │   ├── validate.md       # Full project validation
│       │   ├── code-review.md    # Pre-commit review
│       │   ├── code-review-fix.md
│       │   ├── execution-report.md
│       │   └── system-review.md
│       │
│       └── github_bug_fix/       # Bug fix workflow
│           ├── rca.md            # Root cause analysis
│           └── implement-fix.md  # Implement from RCA
│
├── .agents/
│   └── plans/                    # Implementation plans
│       ├── .gitkeep
│       └── auth-system-2024-01-15.md
│
├── CLAUDE.md                     # Project instructions
└── [rest of project]
```

## Quick Start

### First-Time Setup

1. **Run initialization:**
   ```
   /init-project
   ```

2. **Create or verify PRD:**
   - If no PRD exists, run `/create-prd` after discussing requirements
   - If PRD exists, review `.claude/PRD.md` for accuracy

3. **Start your first session:**
   ```
   /core_piv_loop:prime
   ```

### Daily Workflow

```
┌─────────────────────────────────────────────────────────────┐
│                    DAILY WORKFLOW                           │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  1. START SESSION                                           │
│     └─▶ /core_piv_loop:prime                               │
│         • Load PRD context                                  │
│         • Review recent history                             │
│         • Check pending plans                               │
│                                                             │
│  2. PLAN (if implementing new feature)                      │
│     └─▶ /core_piv_loop:plan-feature [feature-name]         │
│         • Deep codebase analysis                            │
│         • Create PRD-aligned plan                           │
│         • Document in .agents/plans/                        │
│                                                             │
│  3. EXECUTE                                                 │
│     └─▶ /core_piv_loop:execute [plan-file]                 │
│         • Implement changes                                 │
│         • Run validation                                    │
│         • Update PRD status                                 │
│                                                             │
│  4. VALIDATE                                                │
│     └─▶ /validation:validate                               │
│         • Lint checks                                       │
│         • Type checking                                     │
│         • Tests                                             │
│         • Build verification                                │
│                                                             │
│  5. COMMIT                                                  │
│     └─▶ /commit                                            │
│         • Review changes                                    │
│         • Create commit                                     │
│         • Update session log                                │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Commands Reference

### Core PIV Loop Commands

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/core_piv_loop:prime` | Initialize session with full context | **Every session start** |
| `/core_piv_loop:plan-feature` | Create detailed implementation plan | Before non-trivial features |
| `/core_piv_loop:execute` | Execute plan with validation | When ready to implement |

### Validation Commands

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/validation:validate` | Run full project validation | Before commits, after changes |
| `/validation:code-review` | Technical code review | Pre-commit quality check |
| `/validation:code-review-fix` | Fix issues from review | After code review |
| `/validation:execution-report` | Generate implementation report | After execute phase |
| `/validation:system-review` | Analyze implementation vs plan | Process improvement |

### Bug Fix Commands

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/github_bug_fix:rca [issue-id]` | Root cause analysis | When investigating bugs |
| `/github_bug_fix:implement-fix [issue-id]` | Implement from RCA | After RCA complete |

### Utility Commands

| Command | Description | When to Use |
|---------|-------------|-------------|
| `/init-project` | Initialize PIV system | First-time setup |
| `/create-prd` | Generate PRD from conversation | New project or major pivot |
| `/commit` | Create git commit | After validated changes |

## PRD Management

### PRD Structure

The PRD (`.claude/PRD.md`) is the **single source of truth** for product requirements:

```markdown
# Product Requirements Document: [Project Name]

## Executive Summary
[2-3 paragraphs overview]

## Mission
[Product mission and core principles]

## Target Users
[User personas and needs]

## MVP Scope
### In Scope
- ✅ Feature 1
- ✅ Feature 2

### Out of Scope
- ❌ Deferred feature

## User Stories

### US-001: [Story Title]
**As a** [user type]
**I want to** [action]
**So that** [benefit]

**Acceptance Criteria:**
- [ ] Criterion 1
- [ ] Criterion 2

**Status:** 🟡 In Progress | 🟢 Complete | ⚪ Not Started

## Current Sprint Focus
[What we're working on now]

## Implementation Phases
### Phase 1: [Name]
- Goal: [Description]
- Status: 🟢 Complete

### Phase 2: [Name]
- Goal: [Description]
- Status: 🟡 In Progress
```

### PRD Workflow

1. **Before starting work:** Check PRD for relevant user stories
2. **When planning:** Reference PRD acceptance criteria
3. **When implementing:** Align with PRD specifications
4. **After completing:** Update PRD status checkboxes

## Session History

### Creating Session Logs

Session logs track work across conversations:

```markdown
# Session Log: 2024-01-15 Session 1

## Session Context
- **Focus**: Implementing user authentication
- **PRD Reference**: US-003, US-004
- **Previous Session**: 2024-01-14-session-2.md

## Work Completed
- [x] Set up NextAuth configuration
- [x] Created login page component
- [ ] Add session middleware (blocked)

## Decisions Made
- **JWT vs Session:** Chose JWT for serverless compatibility
- **Provider order:** Google first, then credentials

## Issues Encountered
- **Middleware conflict:** i18n middleware conflicting with auth
  - Resolution: Updated matcher pattern in middleware.ts

## Next Steps
- [ ] Complete session middleware integration
- [ ] Add protected route wrapper
- [ ] Test OAuth flow end-to-end

## Files Modified
- `src/lib/auth/auth-config.ts` - Created auth configuration
- `src/app/[locale]/(auth)/login/page.tsx` - Login page UI
- `middleware.ts` - Updated matcher patterns
```

### Session Log Best Practices

1. **Create at session start** - Document context immediately
2. **Update during work** - Track decisions as they happen
3. **Complete at session end** - Summarize and plan next steps
4. **Link sessions** - Reference previous session for continuity

## Implementation Plans

### Plan Structure

Plans are stored in `.agents/plans/`:

```markdown
# Implementation Plan: [Feature Name]

**Created:** 2024-01-15
**PRD Reference:** US-003, US-004
**Status:** 🟡 In Progress

## Overview
[Brief description of what we're implementing]

## PRD Alignment
- User Story US-003: [Title]
- Acceptance Criteria: [List]

## Technical Approach
[Architecture decisions and rationale]

## Implementation Steps

### Step 1: [Name]
- [ ] Task 1.1
- [ ] Task 1.2
**Files:** `path/to/file.ts`

### Step 2: [Name]
- [ ] Task 2.1
**Files:** `path/to/file.ts`

## Validation Criteria
- [ ] All tests pass
- [ ] Lint clean
- [ ] Build succeeds
- [ ] Acceptance criteria met

## Risks & Mitigations
- **Risk 1:** [Description]
  - Mitigation: [Approach]
```

## Troubleshooting

### "PRD not found"

1. Check if `.claude/PRD.md` exists
2. If not, run `/create-prd` after discussing requirements
3. Or create manually using `.claude/PRD-template.md`

### "Session history empty"

1. Create `.claude/history/` directory if missing
2. Start logging sessions manually or via `/core_piv_loop:prime`

### "Plans directory missing"

1. Create `.agents/plans/` directory
2. Run `mkdir -p .agents/plans && touch .agents/plans/.gitkeep`

### "Context lost between sessions"

1. Always start with `/core_piv_loop:prime`
2. Ensure session logs are being created
3. Check that PRD is up to date

## Best Practices

### Do's

- ✅ Start every session with `/core_piv_loop:prime`
- ✅ Reference PRD user stories in plans
- ✅ Update PRD status after completing features
- ✅ Log significant decisions in session history
- ✅ Validate before committing
- ✅ Create plans for non-trivial features

### Don'ts

- ❌ Skip the prime step
- ❌ Implement without checking PRD alignment
- ❌ Forget to update PRD status
- ❌ Commit without validation
- ❌ Start features without plans
- ❌ Ignore session history

## Version

PIV Loop System v1.0.0

---

*For methodology details, see `.claude/reference/_methodology.md`*
