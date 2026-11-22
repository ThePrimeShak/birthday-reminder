# Email and password account access

## Outcome

Any visitor can create an account or sign in from the landing page and reach their private dashboard. This covers F1 in the [project overview](../project-overview.md#pages-user-flows-and-ui-references).

## Scope

Create the Persian landing page at `/`, the public sign-up and sign-in flows, and the initial protected `/app` route. Use Better Auth for email and password authentication and Neon PostgreSQL with Prisma for persistence. Set up the migrations and document the required configuration with safe placeholders.

## Dependencies

Confirm the runtime, Prisma, and Better Auth compatibility before installing dependencies. Prisma 7 is a candidate. Use a Neon test database for migrations and account verification.

## Visual reference

Adapt the centered introduction and sign-in form for both account actions. Use the dashboard header as a reference for the protected app layout. [Landing](../screenshots/signin-signup-page.png) · [Dashboard](../screenshots/home-page.png)

## Acceptance criteria

- A visitor can choose sign-up or sign-in from `/` and authenticate with email and password. A successful authentication lands on `/app`.
- The account persists and the user can sign in again with the same credentials from a fresh browser session.
- The server checks for a valid session before serving the private dashboard. Unauthenticated visitors can reach the public sign-in flow.
- The Persian RTL forms use the light theme and stay usable at phone and desktop widths. Pending submissions and errors have clear feedback, and users can correct inputs and retry.

## Verification cases

- Register a new account on a narrow viewport, reach `/app`, reload, and sign in again in a fresh browser session.
- Submit invalid fields and incorrect credentials, then correct them and retry. Open `/app` directly without a valid session and verify the response.
- Check both forms at narrow and wide widths, including touch targets, keyboard focus, and error placement.
