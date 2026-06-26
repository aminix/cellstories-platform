---
name: finishing-a-development-branch
description: Use when implementation is complete, all tests pass, and you need to decide how to integrate the work - guides completion of development work by presenting structured options for merge, PR, or cleanup
---

# Finishing a Development Branch

## Overview

Guide completion of development work by presenting clear options and handling chosen workflow.

**Core principle:** Verify tests → Detect environment → Present options → Execute choice → Clean up.

**Announce at start:** "I'm using the finishing-a-development-branch skill to complete this work."

## The Process

### Step 1: Verify Tests

Before presenting options, verify tests pass using the project's test suite (npm test / cargo test / pytest / go test ./...).

If tests fail, stop and display failures. Do not proceed to Step 2.

If tests pass, continue to Step 2.

### Step 2: Detect Environment

Determine workspace state using git directory detection commands to identify whether this is a normal repo, named-branch worktree, or detached HEAD state.

### Step 3: Determine Base Branch

Use `git merge-base HEAD main` or `git merge-base HEAD master` to identify the base branch, or ask for confirmation.

### Step 4: Present Options

**For normal repos and named-branch worktrees, present 4 options:**

1. Merge back to base-branch locally
2. Push and create a Pull Request
3. Keep the branch as-is
4. Discard this work

**For detached HEAD, present 3 options** (no merge option).

### Step 5: Execute Choice

- **Option 1:** Merge locally, verify tests, cleanup, delete branch
- **Option 2:** Push branch without cleanup
- **Option 3:** Keep branch and preserve worktree
- **Option 4:** Require typed "discard" confirmation, then cleanup and force-delete

### Step 6: Cleanup Workspace

Only execute for Options 1 and 4. For worktrees under `.worktrees/` or `worktrees/` directories, use `git worktree remove` and `git worktree prune`. Otherwise, preserve the workspace.

## Key Rules

- Always verify tests before offering options
- Present exactly 4 options (3 for detached HEAD)
- Require typed confirmation for Option 4
- Only cleanup worktrees for Options 1 and 4
- Change to main repo root before removing worktrees
- Never delete branches before removing worktrees
- Only cleanup worktrees your system created
