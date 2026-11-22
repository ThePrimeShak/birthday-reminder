# Save a gift idea

## Outcome

A user can open a friend's page, jot down a gift idea, and find it again later. This covers F3 and the title and source portions of R4, the initial status in R5, and ownership in R6. [Project overview](../project-overview.md)

## Scope

Add `/app/friends/[id]`, link to it from the dashboard, and show the friend's birthday and saved ideas. Support adding an idea with a title and optional source. Store the initial purchase status and update the dashboard's idea count from saved records.

## Dependencies

Requires the [birthday dashboard](m1-02-birthday-dashboard.md) and its account-owned friend records. The optional photo and purchase toggle have their own specs.

## Visual references

Use the friend header, idea form, and card grouping. Reflow the preview's columns so the form and list are accessible on a phone. [Friend detail](../screenshots/friend-info-page.png) · [Dashboard](../screenshots/home-page.png)

## Acceptance criteria

- A dashboard card opens the corresponding friend's page with their Solar Hijri birthday, saved ideas, and a clear way to add an idea to an empty list.
- A title such as «ماگ آبی» is sufficient to save an idea. The optional «از کجا؟» accepts a product link or a short note. New ideas start as «نخریدم».
- The saved idea remains on the friend page after reload and increments the dashboard count for that friend.
- The server scopes the friend lookup, idea list, and create operation to the authenticated owner. The layout and form states work at phone and desktop widths.

## Verification cases

- Save title-only, note, and product-link examples. Reload and verify the idea list, initial status, and dashboard count.
- Try a missing title and a failed save. Verify clear feedback, field retention, and retry.
- Use another signed-in account and a signed-out session to request the friend's page or submit an idea. Verify the private records remain inaccessible.
- Check the empty and populated friend page, form controls, and return navigation at narrow and wide widths.
