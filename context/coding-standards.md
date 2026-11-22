# Shared coding standards

These rules apply across projects. Use [the project overview](project-overview.md) for product requirements and chosen technologies. Use the repository's manifests, lockfile, scripts, and CI for installed versions and runnable checks.

## Code organization

- Follow existing naming, formatting, and module boundaries. Reuse nearby components, helpers, and patterns before introducing new ones.
- Keep business rules separate from rendering, routing, and storage when the behavior can be tested independently. Keep HTTP handling and persistence details at their boundaries.
- Use the project's type system and configuration. Narrow uncertain input at its boundary and keep interface contracts explicit.
- Prefer small changes with clear names and one responsibility per function or component. Add a dependency or abstraction when the task has a concrete need for it.
- For a fix, trace the cause, test the corrected behavior, and keep unrelated cleanup outside the change.

## Version control and generated files

- Track `AGENTS.md`, the shared feature instructions in `skills/feature/`, and team context under `context/`. This includes the overview, coding guides, active feature record, specs, and screenshots selected as design references. Narrow conflicting ignore rules or add a targeted exception when an existing rule hides these files, such as a blanket `context/` rule or a global image extension rule.
- Keep the existing `.gitignore` rules and add entries for local files and generated output used by the actual stack. Common examples include `node_modules/`, `.next/`, `dist/`, `__pycache__/`, `.venv/`, `coverage/`, and browser test output such as `playwright-report/` or `test-results/`. Keep temporary captures and tool logs out of `context/screenshots/`.
- Ignore private environment files, credentials, and machine-local editor or agent state. If you use `.env` and `.env.*` rules, add exceptions for sanitized examples such as `!.env.example`. Keep dependency lockfiles and intentionally shared tooling configuration tracked. When `.codex/` or `.agents/` contains both shared files and local state, ignore the local files or subdirectories specifically. A project-approved `.codex/config.toml` or `.agents/skills/` can be shared when it contains no secrets.
- Use `git check-ignore --no-index` on representative local artifacts and team paths to verify the rules. If a private file is already tracked, report the path without opening it or changing Git history.

## UI

- Follow the existing design system and tokens. Consult [the screenshot references](screenshots/) for relevant ideas about visual hierarchy, composition, and density. Adapt those ideas to the product. Use the spec for interactions.
- Use controls suited to the target platform. Provide accessible names and support the expected input methods with visible focus where applicable. Keep content usable at the supported screen sizes and text directions.
- Cover relevant loading, empty, success, and failure states. Make errors actionable and keep user input when a failed action can be retried.
- For UI changes, run the app and verify the affected flow when the environment permits. Check representative screen sizes and applicable states from the spec. Verify the input and focus behavior of changed controls.

## Data and server boundaries

- Validate external input and enforce authentication and resource-level authorization on the server wherever access is required. Apply ownership constraints in data access.
- Return useful client-facing errors and keep sensitive values out of responses, logs, source, and docs. Use placeholders in example configuration.
- Change persistent schemas through the repository's migration process. Account for existing data and safe retry behavior when a request or job can run again.

## Verification

- Discover commands in the project README, manifests, and CI. Use the package manager indicated by the repo. Follow the Context7 and version checks in [AGENTS.md](../AGENTS.md) when writing code, including tests and scripts, or installing packages.
- Link tests to the acceptance criteria and [domain rules](project-overview.md#domain-rules). Cover relevant success, boundary, failure, and permission cases. Use test data and configured test environments.
- Before `complete`, run the checks required by the spec and the project's relevant configured checks, such as lint, type check, test, and build. Execute a check only when the repo defines it or a documented equivalent.
- Report the commands and actual results. Call out unavailable checks and what remains for manual verification.
