# Add a friend with a Solar Hijri birthday

## Outcome

A signed-in user can save a friend's birthday from the dashboard and see the saved friend after reloading. This covers friend creation in F2 and the ownership boundary in R6. [Project overview](../project-overview.md)

## Scope

Add the friend form, server-side validation, and account-owned persistence through a project migration. Show an entry point on an empty or populated dashboard and surface newly saved friends there.

## Dependencies

Requires [account access](m0-01-account-access.md). Before creating the friend schema, confirm the proposed direct storage of Solar Hijri month and day and whether birth year is optional. Use the confirmed input rules for validation.

## Visual references

Use the name and birthday field grouping and the form's primary save action. Place the dashboard entry point near the friends list. [Add a friend](../screenshots/add-new-friend-page.png) · [Dashboard](../screenshots/home-page.png)

## Acceptance criteria

- A signed-in user can find the add-friend action and submit a name and valid Solar Hijri birthday.
- The server validates the input and associates the friend with the signed-in account. The friend's name and date appear on that user's dashboard and persist after reloading.
- Invalid values are identified in the form, and a failed save retains the submitted fields for retry.
- The Persian RTL form and dashboard entry point remain usable on phones and desktops, including empty, pending, and error states.

## Verification cases

- Add a friend from both the empty and populated dashboard at phone width. Reload and verify the saved name and Solar Hijri date.
- Exercise missing and invalid input and representative month boundaries under the confirmed validation rules. Verify any optional birth-year behavior once confirmed.
- Use a second account and a signed-out session to verify account ownership and the authentication boundary. Check form layout, focus, and error placement at narrow and wide widths.
