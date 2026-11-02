# Source Verification — Complete Reading and Behavioral Reconstruction

Use this module before claiming how existing code works, invoking or modifying existing implementation, tracing calls, investigating bugs, or assessing compatibility. It corresponds to original Phases C and D.

## 2. Full-Workflow Gates

### Phase C: Search for and completely read source code

**This is a mandatory gate of the Skill.**

**For every existing function, method, class, module, or configuration that will be modified, called, reused, replaced, or relied upon, first locate its real definition and read the complete implementation necessary to establish its actual behavior.**

#### C.1 Find the actual definitions

Use code search, symbol search, reference lookup, or language services to determine:

- Where the definition actually resides.
- Whether identically named definitions exist.
- Whether overloads, overrides, inheritance, or polymorphic implementations exist.
- Whether decorators, wrappers, proxies, dependency injection, or dynamic registration affect behavior.
- Whether conditional imports, platform branches, or runtime-specific implementations exist.

Do not conclude anything from a one-line signature or a search-result snippet alone.

#### C.2 Read the complete target implementation

Read the entire function or method relevant to the target behavior, including:

- Its signature and parameter defaults.
- Its complete body and every branch.
- Preconditions, postconditions, and exception handling.
- Return values and their actual types, structures, and meanings.
- Side effects on object state, files, databases, networks, caches, or global variables.
- Relevant constants, configuration, helper functions, and data structures.
- Decorators, context managers, parent-class implementations, and applicable protocols.

For a long function, read successive **contiguous ranges** until its implementation is completely covered. Truncated tool output, collapsed sections, and search summaries do not count as the complete source.

"Complete reading" means completely reading the implementation and context necessary to establish the behavior at issue; it does **not** require reading every file in the entire repository.

#### C.3 Search for and examine call relationships

Before changing or calling a function, search its call sites and usage patterns. Examine, as relevant:

- Direct callers.
- Downstream functions it calls.
- References from other modules.
- Subclass overrides, interface implementations, and polymorphic dispatch.
- Callbacks, event listeners, task queues, and registries.
- Dynamic calls through strings, reflection, configuration, or dependency injection.
- Tests, mocks, and test fixtures.
- Serialization, deserialization, and usage by external interfaces.

Do not inspect only the definition and ignore callers. The constraints at the call site may differ from what names or comments suggest.

When there are many call sites, count and categorize them first, then inspect **all usage patterns relevant to this change**. A sample alone is not evidence that every usage pattern is compatible.

#### C.4 Read relevant data structures and configuration

When code relies on a data structure, model, schema, enum, database field, protocol, configuration value, or third-party library, trace and verify:

- Actual meaning and permitted values of fields.
- Types, nullability, and defaults.
- Whether fields can be missing.
- Where data is created, transformed, and written.
- Version-compatibility and migration constraints.
- Configuration loading and environment-specific differences.
- Actual third-party dependency versions and the semantics of their corresponding APIs.

Do not infer a field's meaning from its name, or assume runtime values always comply with type annotations.

#### C.5 Stop inferring when evidence is insufficient

If the complete implementation is inaccessible, a dynamic caller cannot be located, a critical dependency is unavailable, or sources contradict one another:

- Identify specifically what evidence is missing.
- Do not invent implementation details.
- Do not present guesses as confirmed facts.
- Prefer further searching or reading.
- If uncertainty remains, narrow the change scope, add verification, or ask one necessary clarifying question.

Do not make high-risk changes when essential behavior is unknown.

### Phase D: Reconstruct actual behavior rather than restating names

Before proposing a change, form a source-grounded understanding of the current behavior. At minimum, establish what is relevant to the task:

| Dimension | Question to resolve |
| --- | --- |
| Input | Where does input originate? What are its actual types and structure? |
| Output | What is returned? How do callers use it? |
| Data flow | Which transformations and branches does the data follow? |
| Conditions | Which predicates choose different execution paths? |
| State | Is object state, global state, or external storage read or written? |
| Side effects | Are files written, networks accessed, databases updated, or events emitted? |
| Errors | Which exceptions can occur, and who handles them? |
| Boundaries | How are nulls, absent fields, empty collections, and extreme values handled? |
| Ordering | Does correctness depend on execution order, sorting, time, or transactions? |
| Compatibility | Does the code rely on existing APIs, data formats, or historical behavior? |
| Performance | What are the data sizes, complexity, and known performance constraints? |

For critical logic, verify your understanding using a short execution trace or an input-to-output example when necessary.

Comments, documentation, and tests can provide clues, but cannot replace verification against source. Where comments conflict with code, use the actual execution path as evidence and report the discrepancy.
