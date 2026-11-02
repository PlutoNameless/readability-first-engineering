# Readability — Code Organization, Comments, Functions, and Constants

Use this module when changing code structure, arranging data-processing stages, deciding whether to extract functions, writing comments, or replacing magic numbers. It preserves original §3.5–3.8.

## 3. Human-Readable Coding Rules

### 3.5 Separate business rules, data transformations, and result writes

Where code is complex, organize it approximately in this order:

1. Input preparation and validation.
2. Business-condition evaluation.
3. Data extraction.
4. Data transformations and missing-value handling.
5. Result assembly or assignment.
6. Aggregation, grouping, or computation.
7. Output and downstream calls.

Do not combine business decisions, type conversion, default-value handling, and result assignment into one expression.

### 3.6 Comments explain why rather than repeating code

Not recommended:

```python
# Check whether the revival was paid for.
is_paid = (is_revive & has_money)
```

If variable names already explain the meaning, this comment adds no information.

More useful comments explain:

- Why a particular treatment is necessary.
- Why a seemingly simpler approach cannot be used.
- Which historical requirement necessitates a compatibility branch.
- Which business rule motivates a boundary condition.
- Why an apparently unusual execution order must not change.

When comments conflict with the implementation, verify and correct the discrepancy; do not simply trust the comment.

### 3.7 Control function responsibilities without excessive fragmentation

Consider splitting a function when it handles several independent responsibilities, contains several complex phases, or contains reusable business logic.

Each extracted function should have a clear responsibility, inputs, outputs, and side effects.

Do not create a large number of one-line helpers with no independent meaning solely to make functions shorter. Do not introduce excessive jumps merely to conform superficially to "single responsibility."

### 3.8 Constants and magic numbers

Values with stable business meanings, repeated uses, or a high risk of misunderstanding should be expressed as meaningful constants or enums.

Do not mechanically turn every `0` and `1` into a constant. Extraction is genuinely useful when the value represents a business state, protocol value, unit, threshold, or configuration setting.

For example, where event states form a defined enum system, use that shared definition rather than scattering unexplained numeric values across modules.
