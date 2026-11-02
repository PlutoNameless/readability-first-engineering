---
name: readability-first-engineering
description: >-
  Use for any software-engineering task involving an existing codebase: project
  discovery, source inspection, architecture analysis, call/dependency tracing,
  debugging, change planning, implementation, refactoring, testing, and code
  review. Apply from the first investigation through final validation, not only
  when writing code. Never infer behavior from filenames, function names,
  comments, or variable names: locate and completely read the relevant
  implementation and its call relationships before drawing conclusions.
  Applies to all programming languages, particularly Python, Pandas, and
  data-processing code. Task-specific instructions are loaded selectively from
  references/.
---

# Readability-First Engineering

## 0. Purpose and governing principles

This Skill defines a software-engineering workflow, not merely a code-formatting checklist. Throughout development, the agent must:

1. Obtain actual evidence before drawing conclusions.
2. Understand existing behavior before deciding how to change it.
3. Design clearly expressed logic before writing code.
4. Preserve business correctness, readability, and long-term maintainability.
5. Avoid cognitive overhead created by unnecessary brevity, fewer variables, or superficial efficiency.
6. Protect existing interfaces, data semantics, and implicit constraints from accidental changes.

**Governing principle:** Code must first be correct, then clear and understandable; only then consider maintenance costs and performance optimizations supported by measurements. Readability is part of delivery quality, not optional cosmetic work.

## 1. Invocation and continuous application

Use this Skill **before substantive work begins** whenever the task involves project analysis, source reading, implementation lookup, call/data/event/dependency tracing, debugging, change planning, adding or changing code, refactoring, or tests. Source inspection is itself subject to this Skill; do not wait until writing code.

Keep its applicable rules in force throughout investigation, analysis, planning, implementation, testing, and final review. If the environment has skill discovery or explicit invocation, use that mechanism; do not claim to have loaded material that was not actually opened. If access to source or important dependencies is missing, disclose the evidence gap and do not invent implementation details.

## 2. Non-negotiable gates (always in effect)

- **No name-based assumptions.** Directory trees, filenames, symbol names, comments, type hints, and documentation are navigation clues, not proof of runtime behavior.
- **Verify before relying on code.** Before modifying, calling, reusing, replacing, or depending on an existing function, method, class, module, or configuration, search for its real definition; read its entire behavior-relevant implementation (including relevant wrappers and branches), and inspect pertinent callers, callees, data contracts, and configuration. Do not substitute search snippets or truncated output for source reading.
- **Investigate proportionately.** Build a small factual project map and expand only as needed. An efficient investigation may be narrow, but must not omit decisive evidence.
- **Do not silently change behavior.** Verify expected inputs, outputs, types, missing values, side effects, error behavior, ordering, contracts, and invariants before making changes. Separate behavioral fixes from readability-only refactoring.
- **Be explicit about uncertainty.** If evidence is incomplete or contradictory, investigate further, narrow the change, or state what remains unverified. Do not undertake high-risk changes based on unverified assumptions.
- **Prioritize meaningful readability.** Choose semantic names and clear logic without mechanically splitting every expression, creating excessive helpers, or sacrificing justified vectorization.
- **Validate actual results.** Inspect the final code and diff, run relevant existing checks where possible, and disclose unrun tests or remaining risk. Do not claim success without evidence.

## 3. Task-based module routing

**Progressive disclosure is mandatory:** Read this entry point first. Open only the reference module(s) required by the **current task and phase**. At a phase transition, load newly relevant modules; do not preload every reference merely because a task might eventually involve them. Keep the governing rules above active throughout.

| Task or current phase | Load these modules when needed |
| --- | --- |
| Define requirements, modification boundaries, invariants, or a change plan | [`references/change-planning.md`](references/change-planning.md) |
| Survey repository structure, framework, build system, entry points, or tests | [`references/project-discovery.md`](references/project-discovery.md) |
| Inspect source, explain existing behavior, trace dependencies/calls, or diagnose bugs | [`references/source-verification.md`](references/source-verification.md) |
| Write/refactor expressive names, boolean predicates, complex expressions, or call chains | [`references/readability-expressions.md`](references/readability-expressions.md) |
| Organize code stages, comments, function boundaries, or named constants | [`references/readability-organization.md`](references/readability-organization.md) |
| Work on Pandas, NumPy, DataFrames, Series, missing values, grouping, or data transformations | [`references/data-processing.md`](references/data-processing.md) |
| Prepare or perform code additions, edits, or refactoring | [`references/implementation.md`](references/implementation.md) |
| Inspect the completed change, run tests, review correctness, data semantics, or diffs | [`references/review-validation.md`](references/review-validation.md) |
| Conduct a final audit or report completion and unresolved risks | [`references/delivery-standards.md`](references/delivery-standards.md) |

### Routing rules

1. **Project exploration:** Load `project-discovery.md`; load `source-verification.md` as soon as conclusions depend on real implementation.
2. **Code-reading or bug-analysis task:** Load `source-verification.md`; include `change-planning.md` only when determining a repair/design, not for a purely explanatory reading task.
3. **Change request:** Start with `change-planning.md` and the relevant evidence modules; load `implementation.md` before editing. Load the relevant readability module(s) while designing code, not automatically both for a trivial change.
4. **Data-processing change:** Additionally load `data-processing.md` before making semantic decisions about DataFrame/Series operations.
5. **Validation and handoff:** Load `review-validation.md` when reviewing actual changes; load `delivery-standards.md` for final prohibitions, acceptance standards, and reporting.
6. **Small tasks:** Keep the investigation and report short, but never skip an evidence or verification gate made relevant by the task. Do not load implementation/review modules for a task that only asks for an explanation and makes no change.
7. **Never treat routing as a substitute for reading.** A link, a module filename, or a reference seen in search results does not mean the module was loaded. Open the actual content of each selected module before applying its detailed rules.

The numbered source sections have been relocated without dropping their requirements: original §2 phases A/E → `change-planning`; §2 B → `project-discovery`; §2 C/D → `source-verification`; §3.1–3.4 → `readability-expressions`; §3.5–3.8 → `readability-organization`; §4 → `data-processing`; §5 → `implementation`; §6 → `review-validation`; §7–9 → `delivery-standards`. Original §0–1 and the cross-cutting gates are here.
