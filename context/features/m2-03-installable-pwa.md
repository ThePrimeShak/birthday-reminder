# Install and launch the PWA

## Outcome

A user can add Birthday Reminder to a supported phone's home screen and launch the main flow from its icon. This covers F5 and G3 for the first release. [Project overview](../project-overview.md)

## Scope

Provide the metadata, icons, and browser integration needed for installation and launch. Verify a deployed test build and preserve the normal browser flow and access checks for private pages and photos.

## Dependencies

Use a deployed test build with [account access](m0-01-account-access.md), [friend and gift features](m1-04-private-gift-photos.md), [annual greetings](m2-01-annual-greetings.md), and [purchase tracking](m2-02-gift-purchase-status.md). Verify the current installation requirements for the supported browsers during implementation.

## Visual references

Use the landing and dashboard layouts to check the screens reached from the home-screen icon. [Landing](../screenshots/signin-signup-page.png) · [Dashboard](../screenshots/home-page.png)

## Acceptance criteria

- A supported phone can install or add the deployed app to its home screen. The icon and app name identify Birthday Reminder.
- Opening the icon enters the same session-aware app flow. A signed-out user reaches the public account flow, and a user with a valid session in the launched app can reach the dashboard.
- A user can complete the main friend and gift flow from the installed app on a phone. The same flow remains usable in the browser.
- App launch and caching preserve account isolation for private routes, records, and photos.

## Verification cases

- Install the test build on a supported phone and launch it from the icon. Verify the signed-out and authenticated paths within the installed app.
- Add a friend and a gift idea from the installed app and verify that returning to the app preserves the saved data.
- Check the ordinary browser flow at narrow and wide widths. After the installed app's session ends, verify that previously viewed private data is inaccessible.
