---
name: writing-plans
description: Use when translating a brainstormed and approved design into a detailed step-by-step implementation plan for execution
---

# Writing Plans

## Overview

Generate thorough implementation plans assuming the engineer lacks codebase familiarity. Document essential details: files to modify, code samples, testing approaches, documentation to review, and validation methods. Break work into manageable tasks emphasizing DRY, YAGNI, TDD, and regular commits.

**Announce at start:** "I'm using the writing-plans skill to create the implementation plan."

**Context:** Isolated worktrees should be created via `superpowers:using-git-worktrees` at execution time.

**Save plans to:** `docs/superpowers/plans/YYYY-MM-DD-<feature-name>.md`

## Scope Validation

Multi-subsystem specs warrant separate plans per subsystem, each producing independently testable software. Suggest decomposition if not already done during brainstorming.

## File Structure

Map created/modified files before defining tasks:

- Design focused units with clear boundaries and defined interfaces
- Keep files small enough to reason about completely
- Colocate files that change together; split by responsibility, not technical layers
- Follow existing codebase patterns without unilateral restructuring

File architecture directly informs task decomposition.

## Task Right-Sizing

Each task represents the smallest unit with its own test cycle and reviewer gate. Include setup and documentation within the task needing it; split where reviewers could meaningfully reject one task independently.

## Granular Steps

Each step is atomic (2-5 minutes):
1. Write failing test
2. Verify failure
3. Implement minimal code
4. Verify passing
5. Commit

## Required Plan Header

```markdown
# [Feature Name] Implementation Plan

> **For agentic workers:** REQUIRED SUB-SKILL: Use
> superpowers:subagent-driven-development or
> superpowers:executing-plans.

**Goal:** [One sentence]

**Architecture:** [2-3 sentences on approach]

**Tech Stack:** [Key technologies]

## Global Constraints

[Spec project-wide requirements — version minimums, dependency limits,
naming conventions, platform requirements — exact values from spec]

---
```

## Task Format

Include exact file paths, complete code blocks, precise commands with expected output, and explicit interface definitions between tasks (consumed/produced signatures).

## Quality Standards

- **No placeholders:** Avoid "TBD," "handle edge cases," "similar to Task N"
- **Complete code:** Show full implementation for every code step
- **Exact commands:** Include precise pytest/git invocations and outputs
- **Type consistency:** Verify function names/signatures match across tasks

## Self-Review Checklist

1. **Spec coverage:** Each requirement maps to a task
2. **Placeholder scan:** Remove vague language patterns
3. **Type consistency:** Verify signatures align across tasks

Fix issues inline without re-reviewing.

## Execution Handoff

After saving, offer two options:

**Subagent-Driven (recommended):** Fresh subagent per task + two-stage review via `superpowers:subagent-driven-development`

**Inline Execution:** Batch execution with checkpoints via `superpowers:executing-plans`
