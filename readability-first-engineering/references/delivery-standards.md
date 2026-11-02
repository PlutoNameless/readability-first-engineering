# Delivery Standards — Prohibitions, Reporting, and Acceptance

Use this module for final audits, completion reporting, or checking that a coding task meets the Skill's definitive standards. It preserves original §7–9.

## 7. Prohibited Working Practices

The following practices violate this Skill:

1. Inferring a file's implementation solely from its name.
2. Inferring function behavior solely from its name.
3. Inferring actual execution behavior solely from comments or documentation.
4. Editing a target function after reading only search hits, signatures, or partial source excerpts.
5. Modifying a function that might be used by several modules without finding its call sites.
6. Inferring field meaning without inspecting data structures and data origins.
7. Applying `.fillna(0)` indiscriminately without confirming missing-value semantics.
8. Compressing complex conditions and data handling into one line just to reduce line count.
9. Removing intermediate variables with clear business meaning just to reduce variable count.
10. Equating readability with mechanically splitting every operator or creating many tiny functions.
11. Replacing vectorized operations with unverified per-row loops in the name of code simplicity.
12. Treating code that runs as a substitute for reviewing business correctness and maintainability.
13. Presenting speculation as certainty before verifying critical implementations.
14. Declaring a modification finished without inspecting the final diff.

## 8. Final Delivery Requirements

When the task is complete, briefly report the following as appropriate to its scale:

1. **Verified current state:** The critical implementation and call relationships.
2. **Root cause:** Where the real problem is and what evidence supports it.
3. **Changes made:** Which files and logic changed.
4. **Behavioral impact:** Which behaviors remained unchanged and which changed.
5. **Readability improvements:** Improvements to naming, semantic layering, and responsibility boundaries.
6. **Verification results:** Which checks ran and their results.
7. **Remaining risks:** What could not be verified or confirmed.

For simple tasks, report concisely rather than mechanically repeating every heading. Never conceal unread source, missing verification, or unresolved uncertainty.

## 9. Final Acceptance Criteria

Delivered code should satisfy all of the following:

- Developers need not guess what variable and function names mean.
- Readers can follow the main business flow in code order.
- Complex business predicates are expressed with clear semantics.
- Important data transformations and missing-value handling are not hidden in compressed expressions.
- The behavior and call constraints of critical functions have been verified against the real source.
- The change scope is explicit, and existing interfaces and business behavior are protected.
- Code is neither hard to read merely for brevity nor fragmented merely to increase decomposition.
- Code has been validated to a degree appropriate to its risks.

**Final principle:** Search for evidence and completely understand the implementation first; clarify business semantics before planning modifications; prioritize clear code before optimization. Explicitly mark anything that source and verification cannot establish as unknown rather than filling in gaps using names, intuition, or guesses.
