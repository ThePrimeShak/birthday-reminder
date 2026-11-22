# Record an annual birthday greeting

## Outcome

On a friend's birthday, the user can mark that they greeted the friend and see the result later. This covers F4, R2–R3, and the ownership boundary in R6. [Project overview](../project-overview.md)

## Scope

Add «تبریک گفتم» to the dashboard's birthday-today state. Store one greeting status per friend and Solar Hijri occurrence year.

## Dependencies

Use the [birthday dashboard's](m1-02-birthday-dashboard.md) occurrence date and year, including the confirmed day boundary and Esfand policy.

## Visual reference

Use the greeting action and birthday-today panel to guide the placement and hierarchy of the control and its recorded state. [Dashboard](../screenshots/home-page.png)

## Acceptance criteria

- The action is available on the birthday, and the server verifies both the applicable occurrence and ownership before recording it.
- Once marked, the dashboard shows the recorded state for that occurrence after reload. Repeated submissions for the same occurrence preserve one record.
- The following Solar Hijri birthday can be marked independently.
- The action and its pending, recorded, and retryable error states stay clear at phone and desktop widths.

## Verification cases

- Mark a birthday today and reload. Repeat the submission and verify that the same occurrence has one recorded state.
- Test a later occurrence for that friend, a day on which the action is unavailable, and a birthday whose observed date depends on the confirmed Esfand policy.
- Attempt a marking operation from a different account and verify that it produces no change.
- Check action placement and feedback at narrow and wide widths.
