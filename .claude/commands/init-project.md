---
description: Initialize Project
---

# Initialize PIV Loop System

Set up the PIV (Prime-Implement-Validate) development workflow infrastructure for structured, context-aware development.

## Overview

The PIV Loop is a systematic approach to software development that ensures:
- **Continuity** across sessions via PRD and history tracking
- **Quality** through validation at every step
- **Alignment** with product requirements and user stories
- **Traceability** of decisions and implementations

## Initialization Steps

### Step 1: Create Directory Structure

Ensure the following directories exist:

```
.claude/
├── PRD.md                 # Product Requirements Document (Source of Truth)
├── INIT.md                # This initialization guide
├── history/               # Session logs for continuity
│   └── .gitkeep
├── reference/             # Methodology and reference docs
│   └── _methodology.md    # PIV Loop methodology guide
└── commands/              # Slash commands
    ├── core_piv_loop/     # PIV workflow commands
    │   ├── prime.md
    │   ├── plan-feature.md
    │   └── execute.md
    ├── validation/        # Validation commands
    │   ├── validate.md
    │   ├── code-review.md
    │   ├── code-review-fix.md
    │   ├── execution-report.md
    │   └── system-review.md
    └── github_bug_fix/    # Bug fix workflow
        ├── rca.md
        └── implement-fix.md

.agents/
└── plans/                 # Implementation plans storage
    └── .gitkeep
```

Create missing directories:
```bash
mkdir -p .claude/history .claude/reference .agents/plans
touch .claude/history/.gitkeep .agents/plans/.gitkeep
```

### Step 2: Initialize PRD (if needed)

Check if `.claude/PRD.md` exists. If not, create it from the template or run `/create-prd` to generate one from conversation context.

**PRD is the Source of Truth** - It contains:
- Product vision and mission
- User stories with acceptance criteria
- Feature specifications
- Implementation phases
- Current sprint focus

### Step 3: Create Session Log

Create a new session log entry in `.claude/history/`:

```
.claude/history/YYYY-MM-DD-session-N.md
```

Template:
```markdown
# Session Log: [DATE]

## Session Context
- **Focus**: [What we're working on]
- **PRD Reference**: [Relevant user stories or features]
- **Previous Session**: [Link if applicable]

## Work Completed
- [ ] Task 1
- [ ] Task 2

## Decisions Made
- Decision 1: [Rationale]

## Issues Encountered
- Issue 1: [Resolution or status]

## Next Steps
- [ ] Follow-up task 1
- [ ] Follow-up task 2

## Files Modified
- `path/to/file.ts` - [Description of change]
```

### Step 4: Verify Reference Documentation

Ensure `.claude/reference/_methodology.md` exists with PIV Loop methodology documentation.

## Quick Reference

### PIV Loop Commands

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/core_piv_loop:prime` | Load context and prepare for work | Start of every session |
| `/core_piv_loop:plan-feature` | Create implementation plan | Before non-trivial features |
| `/core_piv_loop:execute` | Execute plan with validation | When ready to implement |

### Validation Commands

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/validation:validate` | Full project validation | Before commits, after changes |
| `/validation:code-review` | Technical code review | Pre-commit quality check |
| `/validation:code-review-fix` | Fix review findings | After code review |
| `/validation:execution-report` | Generate implementation report | After execution phase |
| `/validation:system-review` | Analyze implementation vs plan | Process improvement |

### Bug Fix Workflow

| Command | Purpose | When to Use |
|---------|---------|-------------|
| `/github_bug_fix:rca` | Root cause analysis | When investigating bugs |
| `/github_bug_fix:implement-fix` | Implement RCA fix | After RCA is complete |

## Post-Initialization Checklist

After running this command, verify:

- [ ] `.claude/PRD.md` exists and is current
- [ ] `.claude/history/` directory exists
- [ ] `.claude/reference/_methodology.md` exists
- [ ] `.agents/plans/` directory exists
- [ ] CLAUDE.md references PIV workflow correctly

## Starting Your First Session

After initialization, run:

```
/core_piv_loop:prime
```

This will:
1. Load the PRD context
2. Review recent session history
3. Check for pending plans
4. Prepare you for productive work

## Workflow Summary

```
┌─────────────────────────────────────────────────────────────┐
│                    PIV LOOP WORKFLOW                        │
├─────────────────────────────────────────────────────────────┤
│                                                             │
│  ┌─────────┐    ┌───────────┐    ┌──────────┐              │
│  │  PRIME  │───▶│   PLAN    │───▶│ EXECUTE  │              │
│  └─────────┘    └───────────┘    └──────────┘              │
│       │              │                │                     │
│       ▼              ▼                ▼                     │
│  Load PRD &     Create PRD-      Implement &               │
│  History        aligned plan     Validate                   │
│                                                             │
│                      │                                      │
│                      ▼                                      │
│               ┌──────────┐                                  │
│               │ VALIDATE │                                  │
│               └──────────┘                                  │
│                      │                                      │
│                      ▼                                      │
│               Update PRD &                                  │
│               Log Session                                   │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

## Notes

- **Always check PRD before starting work** - Features may have existing user stories
- **Update PRD when completing features** - Keep it current with reality
- **Log significant decisions** - Future sessions depend on history
- **Validate before committing** - Quality gates prevent regression
