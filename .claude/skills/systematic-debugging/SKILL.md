---
name: systematic-debugging
description: Use when debugging any issue before attempting fixes - mandates root cause investigation first, symptom fixes are failure
---

# Systematic Debugging

## Overview

Find root causes before attempting fixes.

**Core principle:** ALWAYS find root cause before attempting fixes. Symptom fixes are failure.

```
NO FIXES WITHOUT ROOT CAUSE INVESTIGATION FIRST
```

## Four Mandatory Phases

### Phase 1: Root Cause Investigation
- Read error messages thoroughly
- Reproduce the issue consistently
- Check recent changes
- Gather evidence across system boundaries
- Trace data flow backward through call stacks

### Phase 2: Pattern Analysis
- Find working examples in the codebase
- Compare against reference implementations
- Identify differences between working and broken code
- Understand dependencies

### Phase 3: Hypothesis Formation
- Form a specific, single testable theory
- Test minimally — change one variable at a time
- Verify results before proceeding to the next hypothesis

### Phase 4: Implementation
- Create a failing test that reproduces the bug
- Implement the fix addressing the root cause
- Verify the fix resolves the issue
- If 3+ sequential fixes each expose distinct problems, stop — this signals deeper architectural issues

## Red Flags — Return to Phase 1

- Proposing a solution before completing investigation
- Assuming the root cause without evidence
- Attempting multiple fixes simultaneously
- Quick patches that mask the underlying issue

## Rationalizations to Reject

| Rationalization | Reality |
|----------------|---------|
| "It's obvious what's wrong" | Investigate anyway — obvious is often wrong |
| "I'm under time pressure" | Random fixes take 2-3× longer |
| "It's an emergency" | Systematic debugging still faster |
| "I've seen this before" | Context differs — investigate this instance |

## Real-World Impact

- Systematic: 15-30 minutes, 95% first-attempt success rate
- Random fixes: 2-3 hours, 40% success rate

## Integration

**Related skills:**
- **superpowers:test-driven-development** — Create failing tests as part of Phase 4
- **superpowers:verification-before-completion** — Verify the fix actually works before claiming done
