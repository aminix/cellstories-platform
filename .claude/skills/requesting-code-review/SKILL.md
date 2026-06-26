---
name: requesting-code-review
description: Use when implementation is complete or between major tasks to dispatch a code reviewer subagent and act on findings before proceeding
---

# Requesting Code Review

## Overview

Dispatch a focused code reviewer subagent to evaluate completed work. Review early and often to catch problems before they compound.

**Core principle:** Review early, review often. Catch problems before they compound.

## When to Request a Review

**Mandatory:**
- After completing each task in subagent-driven development
- After completing a major feature
- Before merging to main

**Also valuable:**
- When stuck on a problem
- Before refactoring
- After fixing a complex bug

## The Process

### Step 1: Get Git SHAs
Obtain the base commit SHA (where your work branched from) and the head commit SHA (your latest commit).

```bash
git merge-base HEAD main   # base
git rev-parse HEAD         # head
```

### Step 2: Dispatch Code Reviewer Subagent

Dispatch a general-purpose subagent with:
- Description of the work completed
- Requirements the implementation should satisfy
- Base and head commit SHAs
- Any known concerns or areas of focus

The subagent receives focused context, not your full session history, allowing concentrated evaluation.

### Step 3: Act on Findings

| Severity | Action |
|----------|--------|
| Critical | Fix immediately before proceeding |
| Important | Fix before moving to next task |
| Minor | Log for later consideration |

You may respectfully challenge reviewer findings you believe are technically incorrect — support your position with code examples and test results.

## Key Rules

- Never skip reviews for seemingly simple changes
- Never ignore critical findings
- Never proceed with unresolved important issues
- When disagreeing with a reviewer, provide technical reasoning

## Integration

**Required workflow skills:**
- **superpowers:subagent-driven-development** — Uses this skill after each task and for final review
- **superpowers:receiving-code-review** — Use when acting on feedback received
