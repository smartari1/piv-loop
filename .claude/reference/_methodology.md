# PIV Loop Methodology

## Introduction

The PIV (Prime-Implement-Validate) Loop is a structured methodology for AI-assisted software development that maximizes context utilization, ensures quality, and maintains alignment with product requirements across multiple development sessions.

## Philosophy

### Core Principles

1. **Context is King** - Without proper context, even the best AI assistance produces suboptimal results
2. **PRD as North Star** - All work should trace back to product requirements
3. **Quality Gates** - Validation at every step prevents compound errors
4. **Documented Decisions** - Future sessions depend on past reasoning
5. **Incremental Progress** - Small, validated steps over large, risky leaps

### Why PIV Loop?

Traditional AI-assisted development often suffers from:
- **Context amnesia** - Each session starts from scratch
- **Requirement drift** - Work diverges from actual needs
- **Quality debt** - Errors compound without validation gates
- **Lost decisions** - Rationale forgotten between sessions

PIV Loop addresses these through structured phases and documentation.

## The Three Phases

```
┌─────────────────────────────────────────────────────────────┐
│                                                             │
│     ┌─────────┐     ┌─────────────┐     ┌─────────────┐    │
│     │  PRIME  │────▶│  IMPLEMENT  │────▶│  VALIDATE   │    │
│     │         │     │             │     │             │    │
│     │ Context │     │ Plan &      │     │ Quality     │    │
│     │ Loading │     │ Execute     │     │ Gates       │    │
│     └─────────┘     └─────────────┘     └─────────────┘    │
│          │                                    │             │
│          │                                    │             │
│          └────────────────────────────────────┘             │
│                    Feedback Loop                            │
│                                                             │
└─────────────────────────────────────────────────────────────┘
```

### Phase 1: PRIME

**Purpose:** Load all relevant context to maximize AI effectiveness

**Activities:**
1. Load Product Requirements Document (PRD)
2. Review recent session history
3. Check for pending implementation plans
4. Understand current project state
5. Identify work focus for this session

**Outputs:**
- Loaded PRD context
- Understanding of recent work
- Clear session objectives
- Awareness of pending tasks

**Command:** `/core_piv_loop:prime`

### Phase 2: IMPLEMENT

**Purpose:** Execute work with proper planning and PRD alignment

**Sub-phases:**

#### 2a. Plan (for non-trivial features)

**Activities:**
1. Deep codebase analysis
2. Research patterns and dependencies
3. Create PRD-aligned implementation plan
4. Document technical decisions
5. Define validation criteria

**Outputs:**
- Detailed implementation plan in `.agents/plans/`
- Technical approach documentation
- PRD reference mapping
- Risk assessment

**Command:** `/core_piv_loop:plan-feature`

#### 2b. Execute

**Activities:**
1. Follow implementation plan
2. Write code changes
3. Update affected files
4. Handle edge cases
5. Document inline decisions

**Outputs:**
- Implemented features
- Code changes
- Updated session log

**Command:** `/core_piv_loop:execute`

### Phase 3: VALIDATE

**Purpose:** Ensure quality and update documentation

**Activities:**
1. Run linting and formatting
2. Execute type checking
3. Run test suite
4. Verify build succeeds
5. Check acceptance criteria
6. Update PRD status
7. Create session log entry

**Outputs:**
- Clean validation results
- Updated PRD status
- Session log entry
- Ready-to-commit changes

**Commands:** `/validation:validate`, `/validation:code-review`

## Document Types

### PRD (Product Requirements Document)

**Location:** `.claude/PRD.md`

**Purpose:** Single source of truth for product requirements

**Contents:**
- Product vision and mission
- User personas
- User stories with acceptance criteria
- MVP scope (in/out)
- Implementation phases
- Current sprint focus

**Update Frequency:** After completing features, pivoting, or scope changes

### Session Logs

**Location:** `.claude/history/YYYY-MM-DD-session-N.md`

**Purpose:** Track work and decisions across sessions

**Contents:**
- Session context and focus
- Work completed
- Decisions made with rationale
- Issues encountered
- Next steps
- Files modified

**Update Frequency:** Every session

### Implementation Plans

**Location:** `.agents/plans/feature-name-YYYY-MM-DD.md`

**Purpose:** Detailed roadmap for feature implementation

**Contents:**
- PRD alignment
- Technical approach
- Step-by-step implementation
- Validation criteria
- Risks and mitigations

**Update Frequency:** Created for each non-trivial feature

## Workflow Patterns

### Pattern 1: New Feature Development

```
1. /core_piv_loop:prime
   └─▶ Load context, identify feature in PRD

2. /core_piv_loop:plan-feature [feature-name]
   └─▶ Create detailed plan with PRD references

3. /core_piv_loop:execute [plan-file]
   └─▶ Implement following the plan

4. /validation:validate
   └─▶ Verify quality gates pass

5. /commit
   └─▶ Commit with proper message

6. Update PRD status
   └─▶ Mark acceptance criteria complete
```

### Pattern 2: Bug Fix

```
1. /core_piv_loop:prime
   └─▶ Load context

2. /github_bug_fix:rca [issue-id]
   └─▶ Analyze and document root cause

3. /github_bug_fix:implement-fix [issue-id]
   └─▶ Implement fix from RCA

4. /validation:validate
   └─▶ Verify fix and no regression

5. /commit
   └─▶ Commit with issue reference
```

### Pattern 3: Code Review Response

```
1. /core_piv_loop:prime
   └─▶ Load context

2. /validation:code-review-fix [review-file]
   └─▶ Address review feedback

3. /validation:validate
   └─▶ Verify fixes

4. /commit
   └─▶ Commit fixes
```

### Pattern 4: Continuation Session

```
1. /core_piv_loop:prime
   └─▶ Load context, review previous session

2. Check .agents/plans/ for pending plans
   └─▶ Resume or start new work

3. Continue from "Next Steps" in session log
   └─▶ Pick up where previous session ended
```

## Quality Gates

### Gate 1: Plan Review

Before executing a plan:
- [ ] PRD alignment verified
- [ ] Technical approach sound
- [ ] Dependencies identified
- [ ] Risks assessed
- [ ] Validation criteria defined

### Gate 2: Pre-Commit

Before committing changes:
- [ ] Lint passes
- [ ] Type check passes
- [ ] Tests pass
- [ ] Build succeeds
- [ ] Acceptance criteria met

### Gate 3: Post-Implementation

After completing a feature:
- [ ] PRD status updated
- [ ] Session log created
- [ ] Documentation updated
- [ ] Plan marked complete

## Anti-Patterns to Avoid

### 1. Skipping Prime

**Problem:** Starting work without loading context leads to:
- Duplicate work
- Conflicting implementations
- Lost continuity

**Solution:** Always start with `/core_piv_loop:prime`

### 2. PRD Drift

**Problem:** Implementing without checking PRD leads to:
- Features that don't match requirements
- Missing acceptance criteria
- Scope creep

**Solution:** Always reference PRD user stories in plans

### 3. Validation Bypass

**Problem:** Committing without validation leads to:
- Broken builds
- Regression bugs
- Technical debt

**Solution:** Always run `/validation:validate` before commits

### 4. History Neglect

**Problem:** Not logging sessions leads to:
- Lost context
- Repeated decisions
- Forgotten rationale

**Solution:** Create session logs for every meaningful session

### 5. Plan-less Implementation

**Problem:** Coding without a plan leads to:
- Architectural inconsistency
- Missed edge cases
- Rework

**Solution:** Create plans for non-trivial features

## Metrics and Success Criteria

### Process Health Indicators

- **Session Prime Rate:** % of sessions starting with prime (target: 100%)
- **Plan Coverage:** % of features with plans (target: >80% for non-trivial)
- **Validation Pass Rate:** % of commits with clean validation (target: 100%)
- **PRD Currency:** Days since last PRD update (target: <7)

### Quality Indicators

- **First-Time Quality:** % of features completed without rework
- **Acceptance Rate:** % of acceptance criteria met on first attempt
- **Regression Rate:** Bugs introduced per feature

## Evolution and Adaptation

The PIV Loop is designed to evolve:

1. **Retrospective Reviews:** After major milestones, review what worked
2. **Command Refinement:** Update commands based on usage patterns
3. **Template Updates:** Improve document templates from experience
4. **Workflow Optimization:** Streamline based on friction points

## References

- `.claude/INIT.md` - Full initialization guide
- `.claude/PRD-template.md` - PRD creation template
- `.claude/commands/` - All available commands
- `.agents/plans/` - Example implementation plans

---

*PIV Loop Methodology v1.0.0*
