# Toggle gift purchase status

## Outcome

A user can mark a gift as purchased or move it back to the unpurchased list. This completes purchase tracking in F3 and R5 and uses the ownership boundary in R6. [Project overview](../project-overview.md)

## Scope

Add a one-action purchase control to each idea card. Persist the selected status and present unpurchased ideas before purchased ideas.

## Dependencies

Requires the account-owned idea list and initial status from [gift idea creation](m1-03-gift-ideas.md). The layout also accommodates the optional photos shipped in M1.

## Visual reference

Use the labeled purchase controls and the visual grouping of purchased and unpurchased cards. Keep the state readable from its text and accessible to touch and keyboard users. [Friend detail](../screenshots/friend-info-page.png)

## Acceptance criteria

- The owner can change «نخریدم» to «خریدم» and back with one action per change. The saved state persists after reloading.
- Unpurchased ideas appear above purchased ideas after both changes. Updating status preserves the other idea fields.
- The server updates only an idea owned by the signed-in account. A failed update provides a retry and leaves the visible status consistent with the saved one.
- The control and its pending and error feedback work on phones and desktops.

## Verification cases

- Toggle an idea in each direction in a list with mixed purchase statuses. Check the displayed order and reload to verify persistence.
- Force a failed save and verify the displayed status and retry behavior. Attempt to update the same idea from another account.
- Check one-action operation with touch and keyboard at narrow and wide widths.
