# Pandas, NumPy, and Data-Processing Rules

Use this module for DataFrame/Series operations, vectorized transformations, grouping, nullable data, dtype changes, and data-pipeline refactoring. The principles of general readability apply here in a domain-specific way. It preserves original §4.

## 4. Pandas, NumPy, and Data-Processing Rules

### 4.1 Give DataFrames and Series understandable names

Not recommended:

```python
d = ...
gb = ...
```

Recommended:

```python
event_data = ...
role_groups = ...
```

If several DataFrames exist in one function, name them by their stage or business entity, such as `raw_events`, `validated_events`, and `aggregated_events`.

### 4.2 Business masks must have semantic names

Not recommended:

```python
target_id = data["other_role_id"].where(
    data["is_kill"] == 1
)
```

Recommended:

```python
is_kill_event = data["is_kill"].eq(1)

kill_target_role_id = data["other_role_id"].where(
    is_kill_event
)
```

A mask name should specify the business event it selects, rather than just `mask`, `condition`, or `flag`, unless it is genuinely generic utility logic.

### 4.3 Understand `where`, index alignment, and missing-value semantics

Before using `where()`, verify:

- What is retained when the condition is true.
- Which value is produced when the condition is false.
- Whether missing values are introduced.
- Whether the original Series and condition Series have aligned indices.
- Whether the resulting dtype changes.
- Whether downstream operations can handle missing values.

Do not choose `where()` merely because it is concise. Choose a clearer `if/else`, `mask`, or explicit assignment if that better communicates the business intent.

### 4.4 Never apply `fillna(0)` indiscriminately

**Missing is not the same as zero.**

Before `.fillna(0)`, verify the business semantics:

- Does an absent field mean its numerical value is zero?
- Does an empty value in one record mean "unknown"?
- Should a failed conversion surface as an exception or data-quality issue?
- Does replacing nulls with zero change a later sum, mean, count, or group result?

Distinguish these five situations:

1. The field does not exist at all.
2. The field exists, but some records contain nulls.
3. The field exists, but its type is unexpected.
4. Data conversion failed.
5. The business value genuinely is zero.

Only fill nulls with zero when the business rule has been confirmed.

### 4.5 Make boolean-to-integer conversion explicit

`.astype(int)` changes the data type and missing-value behavior. Before using it, verify:

- Whether downstream code requires integer `0/1` values.
- Whether nulls are allowed.
- Whether boolean dtype should be preserved.
- Whether a nullable integer dtype should be used.
- Whether `NA` in a nullable Boolean could cause conversion failure.

Do not unconditionally convert all flags just because existing code often uses integer flags.

### 4.6 Respect indices, copies, and assignment semantics

Pay attention to:

- Whether Series operations align on index labels.
- Whether indices are duplicated.
- Whether a DataFrame is a slice or view.
- Whether `.copy()` is needed explicitly.
- Whether chained-assignment problems may occur.
- Whether scalar assignment broadcasts to every row.
- Whether Series assignment aligns by index rather than position.

Do not alter index semantics merely to make code look more orderly.

### 4.7 Make the business meaning of `groupby` explicit

When calling `groupby()`, verify and explicitly address significant parameters as the task requires:

- `sort`
- `dropna`
- `observed`
- `as_index`

These parameters affect group-key ordering, missing-key treatment, grouping of categorical data, and result structure. Do not rely on unclear defaults merely to write fewer arguments.

Group objects should have business-meaningful names such as `role_groups`, not `gb`.

### 4.8 Preserve vectorization without blindly chasing one-liners

Readability refactoring must not casually replace Pandas/NumPy vectorized operations with per-row Python loops.

Meaningful intermediate Series and boolean masks are allowed. For large datasets, account for the memory cost of intermediate objects and use benchmarks to determine whether optimization is needed.

Without measurements, do not claim that a shorter expression is necessarily faster or that decomposing variables necessarily causes a significant performance penalty.
