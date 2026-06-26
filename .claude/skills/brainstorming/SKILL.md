---
name: brainstorming
description: Use when starting any project, feature, or task before implementation begins - enforces a design-before-code gate requiring explicit approval before any code is written
---

# Brainstorming

## Overview

Turn ideas into approved designs before any implementation begins.

**Core principle:** Do NOT invoke any implementation skill, write any code, scaffold any project, or take any implementation action until you have presented a design and the user has approved it. This applies to EVERY project regardless of perceived simplicity.

## The Process

Work through these tasks in order:

1. **Explore** — Review project files and documentation to understand existing context
2. **Visual tools** — Offer visual companion tools only when genuinely needed (just-in-time, not upfront)
3. **Questions** — Ask clarifying questions one at a time about purpose, constraints, and success criteria
4. **Approaches** — Present 2-3 alternative approaches with trade-offs and a recommendation
5. **Design presentation** — Present the design section by section, securing approval for each
6. **Documentation** — Write the spec to `docs/superpowers/specs/YYYY-MM-DD-<topic>-design.md`
7. **Self-review** — Check spec for placeholders, contradictions, and ambiguity
8. **User review** — Have the user review the written specification
9. **Handoff** — Invoke `superpowers:writing-plans` to create the implementation roadmap

## Important Constraints

- Every project goes through this process — including todo lists, single-function utilities, and config changes
- Large projects should be decomposed into independent sub-projects rather than bundled into one spec
- The **only** skill invoked after brainstorming is `superpowers:writing-plans`
- No frontend-design, mcp-builder, or other implementation tools until design is approved

## Red Flags

- Jumping to implementation before design is approved
- Skipping the spec document
- Treating a task as "too simple" to need this process
- Invoking any implementation skill before completing Step 9
