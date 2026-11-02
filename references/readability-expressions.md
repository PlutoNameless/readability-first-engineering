# Readability — Naming, Predicates, Expressions, and Chains

Use this module when writing or reviewing code whose comprehension depends on names, boolean predicates, expression structure, or method chains. It preserves original §3.1–3.4.

## 3. Human-Readable Coding Rules

### 3.1 Names must communicate meaning

Variable, function, class, and field names should express their business role or technical purpose as clearly as practical.

Not recommended:

```python
d = ...
gb = ...
src = ...
tgt = ...
rev = ...
amt = ...
cnt = ...
```

Recommended:

```python
event_data = ...
role_groups = ...
source_role_id = ...
target_role_id = ...
revive_type = ...
payment_amount = ...
event_count = ...
```

Avoid:

- Personal abbreviations whose meaning is known only to the original author.
- Using different names for the same concept in different places.
- Names that do not convey the object's type or purpose.
- Names that conflict with actual behavior.
- Overly general `data`, `result`, `item`, or `value` without adequate context.

Widely understood, unambiguous technical abbreviations may remain, such as `id`, `url`, `api`, `http`, `json`, `sql`, `cpu`, `gpu`, and `uuid`. Domain-specific abbreviations should be used only when the team has clearly established their meanings.

Do not create excessively long, redundant, or awkward names simply to make every variable name maximally explicit. Names should be clear, stable, and distinctive within their context.

### 3.2 Boolean variables must clearly express a predicate

Prefer prefixes such as:

- `is_...`
- `has_...`
- `can_...`
- `should_...`
- `needs_...`

For example:

```python
is_revive_event = ...
has_positive_revive_payment = ...
is_paid_revive = ...
```

Do not make a variable named `paid`, `valid`, or `active` carry multiple meanings at once.

Break complex business conditions into meaningful predicate steps:

```python
is_revive_event = ...
has_positive_revive_payment = ...

is_paid_revive = (
    is_revive_event
    & has_positive_revive_payment
)
```

Do not compress an entire business decision into an argument of a subsequent data operation.

### 3.3 One line should express one primary intention, not mechanically one operator

Not recommended:

```python
result = ((a == 1) & (b > 0) & (c != 0)).astype(int)
```

Clearer:

```python
is_a_valid = a == 1
is_b_positive = b > 0
is_c_valid = c != 0

is_result_valid = (
    is_a_valid
    & is_b_positive
    & is_c_valid
)

result = is_result_valid.astype(int)
```

However, avoid the opposite extreme. Simple, direct, unambiguous expressions need no decomposition:

```python
total_amount = unit_price * quantity
```

Do not create a temporary variable for every parenthesis, operator, or function call. Name an intermediate value when it has a distinct business meaning, reduces cognitive effort, is reused, or helps debugging.

**The goal is semantic layering, not maximizing variable count.**

### 3.4 Control chained calls and nested expressions

Consider decomposing an expression when:

- Multiple transformations are applied in sequence.
- One expression combines business predicates and data cleaning.
- Ternary expressions are nested.
- Multiple levels of conditions and function calls are mixed together.
- A call chain obscures the type or meaning of intermediate data.
- A reader must repeatedly parse backward from right to left to understand the business purpose.

Simple call chains can remain. "Avoid complicated method chaining" does **not** mean "ban all method chaining."

Prefer standard `if/elif/else` for complex conditional branches. Use ternary expressions only for simple, straightforward value selection.
