---
name: dispatching-parallel-agents
description: Use when facing 2+ independent tasks that can be worked on without shared state or sequential dependencies
---

# Dispatching Parallel Agents

## Overview

You delegate tasks to specialized agents with isolated context. By precisely crafting their instructions and context, you ensure they stay focused and succeed at their task. They should never inherit your session's context or history — you construct exactly what they need. This also preserves your own context for coordination work.

When you have multiple unrelated failures (different test files, different subsystems, different bugs), investigating them sequentially wastes time. Each investigation is independent and can happen in parallel.

**Core principle:** Dispatch one agent per independent problem domain. Let them work concurrently.

## When to Use

**Use when:**
- 3+ test files failing with different root causes
- Multiple subsystems broken independently
- Each problem can be understood without context from others
- No shared state between investigations

**Don't use when:**
- Failures are related (fix one might fix others)
- Need to understand full system state
- Agents would interfere with each other

## The Pattern

### 1. Identify Independent Domains

Group failures by what's broken — each domain is independent, so fixing one doesn't affect the others.

### 2. Create Focused Agent Tasks

Each agent gets:
- **Specific scope:** One test file or subsystem
- **Clear goal:** Make these tests pass
- **Constraints:** Don't change other code
- **Expected output:** Summary of findings and fixes

### 3. Dispatch in Parallel

Multiple dispatch calls in one response = parallel execution. One per response = sequential.

### 4. Review and Integrate

When agents return:
- Read each summary
- Verify fixes don't conflict
- Run full test suite
- Integrate all changes

## Agent Prompt Structure

Good agent prompts are focused, self-contained, and specify expected output.

| Bad | Good |
|-----|------|
| Too broad scope | Specific scope (one file/subsystem) |
| No context | Include error messages |
| No constraints | Clear boundaries ("don't change other code") |
| Vague output | Detailed output requirements |

## When NOT to Use

Avoid this pattern with:
- Related failures (fix one might fix others)
- Exploratory debugging (need full context)
- Agents that share state

## Verification

After agents return: review summaries, check for conflicts, run full suite, and spot-check for systematic errors.

## Real-World Impact

Six test failures across three files dispatched to three agents simultaneously: all investigations completed concurrently with zero conflicts.
