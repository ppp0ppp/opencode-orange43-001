---
name: simplify
description: Use for behavior-preserving code simplification, readability cleanup, maintainability review, and scoped complexity reduction after behavior is understood.
---

# Code Simplification

Adapted from `oh-my-opencode-slim@1.1.1` as a standalone local skill. This template does not install the slim plugin, MCP servers, model presets, or `.slim` state.

## Overview

Simplify code by reducing complexity while preserving exact behavior. The goal is not fewer lines. The goal is code that is easier to read, understand, modify, and debug.

Use this test for every change: would a new team member understand the result faster than the original?

## When To Use

- After a feature is working and tests pass, but the implementation feels heavier than necessary.
- During code review when readability or complexity issues are flagged.
- When you encounter deeply nested logic, long functions, unclear names, or duplicated conditionals.
- When refactoring code written under time pressure.
- When consolidating related logic scattered across files.

## When Not To Use

- The code is already clean and readable.
- You do not understand what the code does yet.
- The code is performance-critical and the simpler version would be measurably slower.
- The code is about to be replaced entirely.
- The simplification would touch unrelated files or broaden the requested scope.

## Principles

### Preserve Behavior Exactly

Do not change what the code does, only how it expresses it. Preserve inputs, outputs, side effects, ordering, errors, and edge cases.

Before every change, ask:

- Does this produce the same output for every input?
- Does this maintain the same error behavior?
- Does this preserve the same side effects and ordering?
- Do existing tests still pass without modification?

### Follow Project Conventions

Simplification means making code more consistent with the codebase, not imposing external preferences.

Before simplifying:

1. Read `AGENTS.md` and nearby project conventions.
2. Study how neighboring code handles similar patterns.
3. Match the project's style for imports, naming, function style, error handling, and type annotations.

### Prefer Clarity Over Cleverness

Explicit code is better than compact code when the compact version requires a mental pause to parse.

- Replace nested ternaries with readable control flow.
- Replace dense inline transforms with named intermediate values when they clarify intent.
- Keep helpful names even if they cost a few extra lines.

### Maintain Balance

Avoid over-simplification.

- Do not inline away names that carry meaning.
- Do not merge unrelated logic into one larger function.
- Do not remove abstractions that serve testability or extensibility.
- Do not optimize for line count over comprehension.

### Scope To What Changed

Default to simplifying recently modified code. Avoid drive-by refactors unless explicitly asked.

## Process

### 1. Understand Before Touching

Answer these before changing or removing anything:

- What is this code's responsibility?
- What calls it and what does it call?
- What are the edge cases and error paths?
- Are there tests that define expected behavior?
- Why might it have been written this way?

If you cannot answer these, read more context first.

### 2. Look For Opportunities

Common signals:

- Deep nesting
- Long functions with mixed responsibilities
- Nested ternaries
- Boolean flag arguments
- Repeated conditionals
- Generic or misleading names
- Duplicated logic
- Dead code
- Wrappers or abstractions that add no value

### 3. Apply Changes Incrementally

Make one simplification at a time.

For each simplification:

1. Make the change.
2. Run relevant tests or validation.
3. Keep it only if behavior is preserved.

Separate refactoring from feature work whenever possible.

### 4. Verify The Result

Confirm:

- The code is genuinely easier to understand.
- The diff is clean and reviewable.
- Project conventions still match.
- No behavior, error handling, or side effects changed.

## Repository Guidance

- Prefer the smallest correct simplification.
- Keep behavior changes and structural cleanup separate.
- Do not add compatibility layers, broad helpers, or abstractions without a concrete need.
- Preserve existing user changes and unrelated dirty files.
- Run only the relevant tests/build checks when possible.

## Verification Checklist

- [ ] Existing tests pass without modification.
- [ ] Build/typecheck/lint still pass when relevant.
- [ ] No unrelated files were refactored.
- [ ] No error handling was weakened or removed.
- [ ] The result is simpler to review than the original.
