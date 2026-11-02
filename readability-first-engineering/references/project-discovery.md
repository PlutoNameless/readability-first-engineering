# Project Discovery — Verify the Actual Repository Structure

Use this module when surveying an existing repository, architecture, dependencies, execution paths, project entry points, or test setup. This corresponds to original Phase B.

## 2. Full-Workflow Gates

### Phase B: Investigate the real project structure

Project-structure investigation must rely on actual file contents and configuration. Never infer responsibility solely from directory names, filenames, or function names.

Verify as needed for the task:

1. The current working directory and the actual project root.
2. The languages, frameworks, build system, and execution methods in use.
3. Dependency manifests, version constraints, environment settings, and build configuration.
4. Actual entry points, startup sequence, route registration, or job-scheduling entry points.
5. Real import and call relationships among relevant modules.
6. Test directories, how tests are run, and existing test coverage.
7. Current version-control status and any uncommitted user changes.

Directory trees and filenames are useful **navigation clues**, never proof of implementation.

Examples:

- A file named `auth.py` does not prove that it implements the complete authentication flow.
- A function named `validate_user()` does not prove that it performs every user validation.
- A file named `cache.py` does not prove that it uses caching or that its caching strategy is correct.
- A comment saying "asynchronous processing" does not prove that the actual call chain is asynchronous.

Open files, inspect configuration, search references, and confirm the actual implementation.

Do not indiscriminately read the whole repository merely to appear thorough. Build a project map first, then expand the investigation around the task objective. The investigation scope can be minimal, but the evidence chain must be complete.
