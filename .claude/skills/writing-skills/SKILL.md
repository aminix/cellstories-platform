---
name: writing-skills
description: Use when creating new skills, editing existing skills, or verifying skills work before deployment
---

# Writing Skills

## Overview

**Writing skills IS Test-Driven Development applied to process documentation.**

You write test cases (pressure scenarios with subagents), watch them fail (baseline behavior), write the skill (documentation), watch tests pass (agents comply), and refactor (close loopholes).

**Core principle:** If you didn't watch an agent fail without the skill, you don't know if the skill teaches the right thing.

**REQUIRED BACKGROUND:** You MUST understand `superpowers:test-driven-development` before using this skill.

## What is a Skill?

A **skill** is a reference guide for proven techniques, patterns, or tools. Skills help future agents find and apply effective approaches.

**Skills are:** Reusable techniques, patterns, tools, reference guides

**Skills are NOT:** Narratives about how you solved a problem once

## When to Create a Skill

**Create when:**
- Technique wasn't intuitively obvious to you
- You'd reference this again across projects
- Pattern applies broadly (not project-specific)
- Others would benefit

**Don't create for:**
- One-off solutions
- Standard practices well-documented elsewhere
- Project-specific conventions (put in instructions file)

## Skill Types

- **Technique** — Concrete method with steps to follow
- **Pattern** — Way of thinking about problems
- **Reference** — API docs, syntax guides, tool documentation

## Directory Structure

```
skills/
  skill-name/
    SKILL.md              # Main reference (required)
    supporting-file.*     # Only if needed
```

## SKILL.md Structure

**Frontmatter (YAML):**
- `name`: Letters, numbers, and hyphens only (no special chars)
- `description`: Third-person, starts with "Use when..." — describes ONLY triggering conditions, never the workflow

```markdown
---
name: skill-name
description: Use when [specific triggering conditions and symptoms]
---

# Skill Name

## Overview
Core principle in 1-2 sentences.

## When to Use
Bullet list with symptoms and use cases / when NOT to use

## Core Pattern
Before/after code comparison (for techniques/patterns)

## Quick Reference
Table or bullets for scanning common operations

## Common Mistakes
What goes wrong + fixes
```

## Skill Discovery Optimization (SDO)

**Critical:** The description should ONLY describe triggering conditions. Do NOT summarize the skill's process or workflow.

**Why this matters:** When a description summarizes the skill's workflow, agents may follow the description instead of reading the full skill content.

```yaml
# BAD: Summarizes workflow
description: Use when executing plans - dispatches subagent per task with code review between tasks

# GOOD: Just triggering conditions
description: Use when executing implementation plans with independent tasks in the current session
```

## Token Efficiency

Target word counts:
- Frequently-loaded skills: <200 words total
- Other skills: <500 words

Techniques: move details to tool help, use cross-references, compress examples, eliminate redundancy.

## The Iron Law (Same as TDD)

```
NO SKILL WITHOUT A FAILING TEST FIRST
```

Write skill before testing? Delete it. Start over.

This applies to NEW skills AND EDITS to existing skills.

## TDD Mapping for Skills

| TDD Concept | Skill Creation |
|-------------|----------------|
| Test case | Pressure scenario with subagent |
| Production code | Skill document (SKILL.md) |
| Test fails (RED) | Agent violates rule without skill |
| Test passes (GREEN) | Agent complies with skill present |
| Refactor | Close loopholes while maintaining compliance |

## Bulletproofing Against Rationalization

For discipline-enforcing skills:

1. **Close every loophole explicitly** — don't just state the rule, forbid specific workarounds
2. **Address "spirit vs letter" arguments** — add "Violating the letter of the rules is violating the spirit of the rules"
3. **Build rationalization table** — capture every excuse agents make and counter it
4. **Create red flags list** — make it easy for agents to self-check

## Flowchart Usage

Use flowcharts ONLY for:
- Non-obvious decision points
- Process loops where you might stop too early
- "When to use A vs B" decisions

Never use for reference material, linear instructions, or code examples.

## Skill Creation Checklist

**RED Phase:**
- [ ] Create pressure scenarios (3+ combined pressures for discipline skills)
- [ ] Run WITHOUT skill — document baseline behavior verbatim
- [ ] Identify rationalization patterns

**GREEN Phase:**
- [ ] Name uses only letters, numbers, hyphens
- [ ] YAML frontmatter with `name` and `description`
- [ ] Description starts with "Use when..." — no workflow summary
- [ ] Run WITH skill — verify compliance

**REFACTOR Phase:**
- [ ] Identify new rationalizations
- [ ] Add explicit counters
- [ ] Build rationalization table
- [ ] Re-test until bulletproof

## The Bottom Line

**Creating skills IS TDD for process documentation.**

Same Iron Law: No skill without failing test first.
Same cycle: RED (baseline) → GREEN (write skill) → REFACTOR (close loopholes).
