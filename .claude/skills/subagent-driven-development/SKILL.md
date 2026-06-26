---
name: subagent-driven-development
description: Use when executing implementation plans with independent tasks in the current session
---

# Subagent-Driven Development

Execute plan by dispatching a fresh implementer subagent per task, a task review (spec compliance + code quality) after each, and a broad whole-branch review at the end.

**Why subagents:** You delegate tasks to specialized agents with isolated context. By precisely crafting their instructions and context, you ensure they stay focused and succeed at their task. They should never inherit your session's context or history — you construct exactly what they need. This also preserves your own context for coordination work.

**Core principle:** Fresh subagent per task + task review (spec + quality) + broad final review = high quality, fast iteration

**Continuous execution:** Do not pause to check in with your human partner between tasks. Execute all tasks from the plan without stopping. The only reasons to stop are: BLOCKED status you cannot resolve, ambiguity that genuinely prevents progress, or all tasks complete.

## When to Use

**Use when:**
- You have an implementation plan
- Tasks are mostly independent
- You want to stay in the current session

**vs. Executing Plans (parallel session):**
- Same session (no context switch)
- Fresh subagent per task (no context pollution)
- Review after each task (spec compliance + code quality), broad review at the end
- Faster iteration (no human-in-loop between tasks)

## The Process

1. **Pre-flight review** — Scan plan for conflicts or contradictions before starting; batch any questions for the human partner upfront
2. **Per-task loop:**
   - Dispatch implementer subagent with task brief + report path + context
   - Answer any questions the implementer asks
   - Implementer implements, tests, commits, self-reviews
   - Generate diff, dispatch task reviewer (spec compliance + code quality)
   - Dispatch fix subagent for Critical/Important findings
   - Re-review until approved
   - Mark task complete in todo list and progress ledger
3. **Final review** — Dispatch whole-branch code reviewer
4. **Finish** — Use `superpowers:finishing-a-development-branch`

## Model Selection

Use the least powerful model that can handle each role to conserve cost and increase speed.

- **Mechanical implementation** (isolated functions, clear specs, 1-2 files): cheap model
- **Integration and judgment tasks** (multi-file, pattern matching, debugging): standard model
- **Architecture and design / final review**: most capable available model

Always specify the model explicitly when dispatching a subagent.

## Handling Implementer Status

- **DONE:** Generate review package, dispatch task reviewer
- **DONE_WITH_CONCERNS:** Read concerns before proceeding; address correctness/scope concerns before review
- **NEEDS_CONTEXT:** Provide missing info and re-dispatch
- **BLOCKED:** Assess blocker — provide context, upgrade model, break task, or escalate to human

## Durable Progress

Track progress in a ledger file, not only in todos. Conversation memory does not survive compaction.

- Check for ledger at start: `cat "$(git rev-parse --show-toplevel)/.superpowers/sdd/progress.md"`
- Tasks listed there as complete are DONE — do not re-dispatch
- When task review comes back clean, append to ledger: `Task N: complete (commits <base7>..<head7>, review clean)`

## File Handoffs

Hand artifacts over as files, not pasted text:
- **Task brief:** extract with `scripts/task-brief PLAN_FILE N`
- **Report file:** implementer writes full report here, returns only status + one-line summary
- **Reviewer inputs:** brief file + report file + review package + global constraints

## Red Flags

**Never:**
- Start implementation on main/master without explicit user consent
- Skip task review
- Proceed with unfixed Critical/Important issues
- Dispatch multiple implementation subagents in parallel (conflicts)
- Tell a reviewer what not to flag or pre-rate finding severity
- Re-dispatch a task the progress ledger already marks complete

## Integration

**Required workflow skills:**
- **superpowers:using-git-worktrees** — Ensures isolated workspace
- **superpowers:writing-plans** — Creates the plan this skill executes
- **superpowers:requesting-code-review** — Final whole-branch review
- **superpowers:finishing-a-development-branch** — Complete development after all tasks

**Subagents should use:**
- **superpowers:test-driven-development** — Subagents follow TDD for each task
