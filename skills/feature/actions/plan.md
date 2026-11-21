# Plan features from the overview

1. Use the owner's requested scope and read `context/project-overview.md`. Read existing specs and the active record to avoid duplicating or replacing work. For planning before implementation, use local `dev` as the base and preserve any existing edits.
2. Turn the agreed outcomes into independently verifiable pieces of work. Respect milestones, dependencies, and product non-goals. Assign each feature to an agreed milestone. If the milestone or required behavior is unclear, report the open decision and continue with specs whose scope and milestone are clear.
3. Write one Markdown spec per feature in `context/features/`. Use the filename format `m<milestone>-<sequence>-<slug>.md`, for example `m0-01-baseline-check.md` or `m1-02-date-only-conversion.md`.
   - Use the lowercase milestone ID from the overview, such as `m0` for `M0`.
   - Number specs in the intended implementation order within each milestone. Start at `01` for each new milestone and pad numbers below `10` with a leading zero. When adding to an existing milestone, continue after its highest assigned sequence and keep existing IDs stable.
   - Use a short, descriptive kebab-case slug. Use the full filename stem as the spec ID in workflow requests.
   - Give each spec an outcome, scope, dependencies, acceptance criteria, and verification cases. Refer to relevant domain rule IDs, flows, and screenshot filenames. For an explicitly requested fix spec, use a short kebab-case ID in `context/fixes/` and include reproduction steps and the expected result.
4. Link each feature spec to its Markdown file from the corresponding roadmap entry. Report the files, recommended order, and open decisions. Planning changes documentation only and leaves the active feature record alone.
