# Change Planning — Task Boundary and Pre-Change Gate

Apply this module when defining scope, deciding what should change, distinguishing fixes from refactoring, or preparing an implementation plan. It contains the original workflow phases A and E.

## 2. Full-Workflow Gates

Every task involving an existing project proceeds through the relevant phases. Simple tasks may shorten their written records, but may not omit necessary evidence checks.

### Phase A: Confirm the task boundary

First establish:

- What actual problem does the user want solved?
- Is the task explanation, investigation, bug fixing, feature addition, or refactoring?
- Which behaviors must remain unchanged?
- Which files, modules, interfaces, or data might be affected?
- Are there performance, compatibility, version, or deployment constraints?

Do not automatically treat the file or function mentioned by the user as the actual change boundary. Confirm that boundary through source code and call relationships.

### Phase E: Plan before editing

Before writing code, establish a sufficiently explicit change plan:

1. The actual behavior of the current implementation.
2. The root cause of the problem, not merely its visible symptoms.
3. Expected behavior and acceptance conditions.
4. The smallest set of files that needs to change.
5. Affected callers, interfaces, and data structures.
6. Behaviors that must remain unchanged.
7. Tests to add or adjust.
8. Performance or compatibility risks, if any.

Distinguish **behavioral changes** from **readability-only refactoring**:

- Pure refactoring should preserve inputs, outputs, side effects, and exception behavior as far as possible.
- When business behavior genuinely needs to change, explicitly state what will change and why.
- Do not modify data semantics, default values, execution order, or interface contracts without authorization under the pretext of improving readability.
- Do not opportunistically refactor large amounts of unrelated code.

Prefer local, verifiable changes that are easy to review.
