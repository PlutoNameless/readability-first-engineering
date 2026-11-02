# Readability-First Engineering Skill

This project-level engineering workflow Skill for AI agents enforces a **human-readability-first** approach throughout project-structure discovery, source inspection, call-relationship tracing, change planning, code generation, testing, and review.

The original requirements are preserved in English, but the large monolithic instruction file is split into **task-specific reference modules**. The small `SKILL.md` entry point provides always-on rules and routes the agent to the material needed for its current task and phase. This avoids loading the entire Skill for a lightweight request.

## Files

- `SKILL.md`: Skill definition, discovery frontmatter (`name` and `description`), mandatory common rules, and selective-loading instructions.
- `references/change-planning.md`: Task scope, behavior preservation, root cause, acceptance criteria, and change planning (original §2 A/E).
- `references/project-discovery.md`: Evidence-based project and repository discovery (original §2 B).
- `references/source-verification.md`: Complete implementation reading, call tracing, data contracts, and runtime behavior (original §2 C/D).
- `references/readability-expressions.md`: Semantic names, boolean logic, expression complexity, and chaining (original §3.1–3.4).
- `references/readability-organization.md`: Code stages, comments, function responsibilities, and constants (original §3.5–3.8).
- `references/data-processing.md`: Pandas, NumPy, and data-processing correctness and readability (original §4).
- `references/implementation.md`: Code creation and change-execution gates (original §5).
- `references/review-validation.md`: Correctness, readability, data semantics, change scope, and verification (original §6).
- `references/delivery-standards.md`: Prohibited practices, delivery reporting, and final acceptance criteria (original §7–9).

## Installation

Copy the **entire** `readability-first-engineering` folder, including its `references/` subfolder, into a local Skill directory supported by your agent.

Common project-level locations (verify against the current documentation for your agent):

- Codex: `.agents/skills/readability-first-engineering/`
- Claude Code: `.claude/skills/readability-first-engineering/`

After installation, verify that the agent discovers the Skill. Discovery systems commonly use `name` and `description` from the `SKILL.md` frontmatter to identify relevant Skills. If your agent supports explicit invocation, invoke it when starting a task involving project code.

## Selective loading

The entry point is designed to be light. The agent must always apply its evidence, correctness, and honesty gates, but should **open detailed modules only at the corresponding phase**.

| Example request | Initial detailed modules | Load later only if needed |
| --- | --- | --- |
| Explain project architecture | `project-discovery` | `source-verification` when behavior must be established |
| Explain or trace a function | `source-verification` | None if no change is proposed |
| Find why a bug occurs | `source-verification` | `change-planning`, then `implementation` if fixing it |
| Add a new feature | `change-planning`, relevant evidence modules | `implementation`, relevant readability modules, `review-validation`, `delivery-standards` |
| Refactor a complex Pandas transformation | `source-verification`, `data-processing`, `change-planning` | `readability-expressions`, `implementation`, then validation/delivery modules |
| Review an existing patch | `source-verification` as needed, `review-validation` | `data-processing` for relevant operations; `delivery-standards` at handoff |

Do not treat filenames, symbol names, short excerpts, or comments as evidence of implementation. Before touching or calling existing code, search and fully read the behavior-relevant implementation and the relevant use sites. A selective module scheme reduces **instruction-loading cost**, not the necessary source verification.

## Important notes

Installing a Skill cannot override the host agent's own Skill discovery, invocation, file-reading, or context-management mechanisms. Automatic invocation and whether reference modules are actually opened depend on the agent and its configuration. The trigger description covers project analysis, source inspection, change planning, code changes, testing, and review, but cannot itself guarantee invocation on every turn.

In particular, this design is a **single discoverable Skill with on-demand reference files**, not nine separately registered Skills. An agent must support reading referenced files during execution for selective loading to work. If the agent cannot access the files, it must report the limitation rather than claim that it followed unseen rules.
