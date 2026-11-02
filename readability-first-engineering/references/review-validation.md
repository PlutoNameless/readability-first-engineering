# Review and Validation — Required Checks After a Change

Use this module once code has been edited or when reviewing another change. Verify **the final resulting code**, not merely the excerpt just written. It preserves original §6.

## 6. Mandatory Post-Change Review

### 6.1 Correctness review

- Does the result satisfy the user's request?
- Is existing business behavior preserved?
- Did inputs, outputs, types, or error behavior change unintentionally?
- Were boundary conditions missed?
- Were new side effects introduced?
- Are any callers now incompatible?

### 6.2 Readability review

Check each of the following:

- Do variable names communicate their actual purpose?
- Are there unnecessary abbreviations?
- Are complex business predicates independently named?
- Are expressions over-compressed?
- Are there complicated ternaries or difficult method chains?
- Are unrelated responsibilities mixed in one code block?
- Are any temporary variables devoid of independent meaning?
- Do comments explain reasons rather than repeat code?
- Does execution order follow the order in which a reader understands the business process?

### 6.3 Data-semantics review

Pay particular attention to:

- Missing values incorrectly converted to defaults.
- Unintended dtype changes.
- Incorrect Series index alignment.
- Changed grouping or sorting semantics.
- Handling of empty data, duplicate indices, and anomalous data.
- Correctness of scalar broadcasting, boolean masks, and conditional assignments.

### 6.4 Change-scope review

Inspect the final diff:

- Were files outside the task scope modified?
- Were any existing uncommitted user changes overwritten or discarded?
- Was irrelevant renaming or formatting introduced?
- Were debugging code, temporary variables, or useless comments left behind?
- Were unnecessary dependencies or abstractions added?

### 6.5 Verification review

Run the checks that are applicable to the actual project:

- Relevant unit tests.
- Integration or end-to-end tests.
- Type checking.
- Static analysis and format checks.
- Builds or essential runtime verification.

Prefer validation methods already present in the project; do not fabricate commands or claim to have executed them.

If tests cannot be run, identify why, which aspects remain unverified, and the remaining risks. "No error was displayed" or "the code looks correct" is not equivalent to having passed tests.
