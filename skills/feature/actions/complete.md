# Complete the feature

If a previous completion already cleared the active fields, follow [Resume an interrupted completion](#resume-an-interrupted-completion).

1. On the owner's `complete` request, verify that the current branch matches the active work branch in `context/current-feature.md`. The work branch must be separate from `dev` and `main`. Confirm local `dev` exists and check for in-progress Git operations. Review all commits to be merged and staged, unstaged, and untracked changes. Stop if completion would include or interfere with unrelated work.
2. Resolve any pending owner review in `Notes` before recording completion. Verify the active spec's acceptance criteria and run the relevant configured checks as described in `context/coding-standards.md`. If a required check fails or cannot run, continue once it passes or the owner explicitly accepts that gap.
3. On the work branch, append one entry with the spec ID and outcome to `History`. Return the heading to `# Current Feature`, set `Status` to `Not Started`, and clear the entries from `Spec`, `Branch`, `Goals`, and `Notes`. Keep all headings and their comments. Stage only the reviewed feature changes and this record. Follow the repository's commit conventions and note the work branch tip.
4. With a clean checkout, switch to local `dev`. Confirm it is checked out, then merge the work branch using its local ref, for example `git merge --no-edit refs/heads/feature/m0-01-baseline-check`. If the checkout or merge fails, report the failure and preserve the work branch. If there is a merge conflict, report the files and wait for direction before resolving or aborting the merge.
5. Verify that the recorded work tip is an ancestor of local `dev`. Report the result, commit, and checks. Pushes and branch cleanup are separate actions.

## Resume an interrupted completion

Inspect the Git state and the pending or committed completion entry before retrying. Ask for the exact branch if it is ambiguous. If the active fields were already cleared but completion was not committed, compare the pending record with `HEAD`. Use the work branch, its spec file, and the new `History` entry to verify that the record belongs to this completion. Check that only the reviewed changes will be committed. Resume from staging or committing as needed and keep the existing history entry.

If the completion commit already exists, resume from the merge step after confirming the checkout is clean and no Git operation is active. If `dev` already contains the recorded tip, report success. If a merge is still in progress, report its status and follow the owner's direction.
