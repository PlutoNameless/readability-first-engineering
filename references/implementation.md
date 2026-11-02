# Implementation — Execution Requirements for Code Generation and Edits

Use this module when about to add, modify, remove, or refactor project code. It preserves original §5.

## 5. Code Generation and Modification Requirements

Before writing code, be able to answer:

- Have I read the complete target implementation?
- Have I searched for and examined the relevant call sites?
- Do I understand inputs, outputs, data types, and side effects?
- Do I know which behaviors must remain unchanged?
- Do I know how to verify the result of the change?

If an essential answer is missing, do not proceed directly with a high-risk change.

When writing or modifying code:

1. Follow the project's **verified** architecture and conventions, without copying clearly poor readability practices.
2. Preserve existing interfaces, data formats, and call contracts unless the task explicitly requires a change.
3. Prefer minimal, verifiable edits.
4. Use variable and function names that reflect business meaning.
5. Express complex business predicates explicitly.
6. Make execution order align with the order in which humans understand the business logic whenever possible.
7. Avoid squeezing several responsibilities into one expression or one enormous function.
8. Do not add unnecessary abstractions, frameworks, or dependencies merely to appear "elegant."
9. Do not change mature vectorized implementations without a good reason.
10. Do not reformat or rewrite large amounts of unrelated code; this unnecessarily expands the review and regression scope.

If the user asks for analysis only, do not modify files without authorization.

If the user asks for a direct change, perform the required source investigation and then make the change; do not expand the investigation indefinitely into an unrelated repository-wide audit.
