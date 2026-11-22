# Birthday Reminder — Project overview

Birthday Reminder is a lightweight Persian web app for people who want to track friends' Solar Hijri birthdays and keep gift ideas for each friend.

## Problem, audience, and success

- People can spot a good gift months before a birthday and forget the idea or where they saw it.
- The app is for Persian-speaking users who primarily use a phone and want to save a gift idea quickly.
- A user spots a blue mug while shopping and saves «ماگ آبی» on Sara's page, optionally adding a photo and where they found it. Near Sara's birthday, they can revisit their ideas and mark the gift they bought.

| Goal | Outcome | How and when to measure it |
| --- | --- | --- |
| G1 | Reach the first gift idea on a phone | Create an account as a new visitor, sign in, add a friend with a Solar Hijri birthday, see the countdown, and save an idea. Repeat with an optional photo and confirm the saved ideas remain visible after reloading. |
| G2 | Track upcoming birthdays and gifts | Verify countdown order, birthday-day copy, annual greeting status, and the order of gift ideas by purchase status. |
| G3 | Open the first release from a phone's home screen | Install the PWA on a supported phone and open the sign-in page or dashboard from its icon. |

## Scope and roadmap

- **MVP** includes a landing page with public sign-up and sign-in, a private birthday dashboard, friend creation, Solar Hijri countdowns, annual greeting status, per-friend gift ideas, and PWA installation.
- **After the MVP**, evaluate the proposed reminder one week before a birthday, using a daily server check and Web Push.
- **Product non-goals.** N/A.

| Milestone | Outcome and completion criteria | Feature specs |
| --- | --- | --- |
| M0 | Any visitor can create a personal account or sign in to an existing account with email and password from `/`. Signed-in users reach `/app` and access protected routes with a valid session. | Pending |
| M1 | On a phone, the user can add a friend, see the Solar Hijri countdown, and save a gift idea with or without a private photo. A second account cannot access the first account's records or photos. | Pending |
| M2 | The first release supports annual greeting status, purchase toggling with unpurchased ideas first, and installation and launch from a phone's home screen. | Pending |
| M3 | If the reminder proposal is approved, verify a reminder seven calendar days before a birthday in a test environment for a user who opted in. | Pending |

## Pages, user flows, and UI references

| Flow | Starting point and user | Steps and expected outcome | Alternate or failure path |
| --- | --- | --- | --- |
| F1 | A visitor opens the landing page at `/` | Read a short introduction and choose sign-up or sign-in. A new user creates a personal account with email and password. A returning user signs in with their existing credentials. After authentication, the user lands on `/app`. | If sign-up or sign-in fails, show an actionable error and allow another attempt. |
| F2 | A signed-in user opens an empty or populated dashboard at `/app` | Add a friend with a name and Solar Hijri birthday. The new card shows the date, countdown, and gift idea count in upcoming birthday order. | Identify invalid fields and retain entered data so the user can correct it. |
| F3 | A signed-in user opens `/app/friends/[id]` from a friend card | See the birthday and gift cards. Add a title with an optional photo and «از کجا؟». Toggle the purchase status on a saved card. | An empty list offers a way to add the first idea. A failed save or upload offers a retry and keeps the entered fields. |
| F4 | A signed-in user sees a friend card on the friend's birthday | See «🎂 امروز تولد ساراست» and use «تبریک گفتم». The status persists for that Solar Hijri birthday year. | Repeating the request preserves the recorded status for that year. |
| F5 | A phone user opens the app in a browser that supports installation | Install it or add it to the home screen through the browser, then open it from the icon and enter the main flow. | The user can continue the main flow in the browser. |

- **Main routes.** `/` provides the introduction and access to sign-up and sign-in. `/app` lists friends and lets the user add one. `/app/friends/[id]` shows a friend's birthday and gift ideas.
- **Design direction and responsive priorities.** Use a light theme for the first release and its visual references, regardless of the device's color preference. Build a mobile-first Persian RTL interface with accessible touch and keyboard controls. Keep forms, cards, and navigation usable at narrow and wide widths, including relevant empty, loading, and error states.

**Visual references**

The supplied desktop screenshots use a warm light background, white cards, and plum primary actions. Use their hierarchy and spacing as a starting point when reflowing layouts and repositioning actions for phones. The overview and approved feature specs define product behavior.

- Landing page (`/`). Reference for the centered introduction and the sign-in form. Adapt the same layout for sign-up. [signin-signup-page.png](screenshots/signin-signup-page.png)
- Dashboard (`/app`). Reference for the birthday-today banner, greeting action, and the countdown and idea count on each friend card. [home-page.png](screenshots/home-page.png)
- Add a friend (F2). Reference for grouping the name and Solar Hijri birthday fields and placing the save action below them. [add-new-friend-page.png](screenshots/add-new-friend-page.png)
- Friend detail (`/app/friends/[id]`). Reference for the birthday summary, gift idea form, and the visual distinction between unpurchased and purchased ideas. [friend-info-page.png](screenshots/friend-info-page.png)
- Friend edit state. Reference for the placement of an inline form and its save and cancel actions if friend editing enters scope. [edit-friend-state.png](screenshots/edit-friend-state.png)

## Domain rules

- Birthdays are entered and displayed in the Solar Hijri calendar and repeat annually in that calendar. The countdown is the difference in calendar days between today and the next occurrence. The difference is zero on the birthday itself. The day boundary and Esfand 30 policy are open.

| Rule | Condition and expected result | Example and boundary case |
| --- | --- | --- |
| R1 | Sort friends by ascending days to their next birthday. Show each friend's name, Solar Hijri birthday, countdown, and gift idea count. | «سارا · ۶ روز مونده · ۲ ایده‌ی کادو». Once the birthday passes, count toward the following Solar Hijri year's occurrence. |
| R2 | On the birthday, replace the countdown text with a birthday message. | Show «🎂 امروز تولد ساراست» on the day. |
| R3 | Offer «تبریک گفتم» on the birthday and record it for that friend's Solar Hijri birthday year. | Repeated marking in the same year keeps one recorded state. The following year can be marked independently. |
| R4 | A gift idea requires a title. A photo and «از کجا؟» are optional. The source field accepts a product link or a short note. | «ماگ آبی» is a valid idea on its own. «ویترین کتاب‌فروشی نزدیک خونه» is a valid source note. |
| R5 | Start each idea as «نخریدم». One action toggles between «نخریدم» and «خریدم». Display unpurchased ideas first. | Marking an idea as purchased moves it below the unpurchased ideas. |
| R6 | Each account can access its own friends, gift ideas, and photos. Enforce ownership on the server for reads and writes. | A request from another account is denied even when it contains a valid friend, idea, or photo identifier. |
| R7 | If M3 is approved, the proposed reminder is seven calendar days before the birthday and requires notification permission. | The iPhone flow also requires installation on the home screen. |

## Data, permissions, and interfaces

| Entity or interface | Purpose | Ownership, permissions, or contract |
| --- | --- | --- |
| Account and session | Email and password sign-up and sign-in, and access to private routes | Visitors can create their own accounts. The server derives the signed-in account identity from a valid Better Auth session. |
| Friend | Name and annual Solar Hijri birthday | Belongs to one account. Reads and writes are scoped to that account. |
| Annual greeting | Record that the user greeted a friend for a birthday | One status per friend and Solar Hijri occurrence year. Repeated submissions for the same year are safe. |
| Gift idea | Title, optional source, purchase status, and optional photo reference | Belongs to a friend and inherits the account's access restriction. |
| Gift photo | Store image bytes in private Vercel Blob | Neon stores the file identifier. The server checks the session and ownership of the related idea before serving the photo. |
| Push subscription and daily check | Deliver proposed reminders after the first release | Associate subscriptions with the signed-in account and respect the user's notification permission. |

- **Sign-in, roles, and ownership.** Signed-in users manage their own records. Validate form data and enforce ownership at server entry points, including direct requests for photos.
- **Sensitive data and lifecycle.** Keep sessions, friend data, and gift photos private. Photo limits and data deletion and retention rules are open.

## Stack and architecture

| Area | Technology or path | Responsibility or reason |
| --- | --- | --- |
| App runtime and package manager | Next.js App Router, TypeScript, npm | Keep routes and server logic in one project. Use [package.json](../package.json) and [package-lock.json](../package-lock.json) for installed dependency versions. |
| UI and routes | Tailwind CSS and planned shadcn/ui | Render the Persian RTL interface and support the main mobile flows. |
| Authentication | Planned Better Auth | Handle email and password sign-up, sign-in, and sessions. |
| Server and domain logic | Next.js server code and Solar Hijri calendar logic | Authorize and validate requests. Keep recurrence and date calculations independently testable. |
| Database | Planned Neon PostgreSQL and Prisma | Persist application records. Prisma 7 remains a candidate pending compatibility checks with the runtime and Better Auth. |
| Photo storage | Planned private Vercel Blob | Store the photo bytes and allow access through an ownership-checked server path. |
| Deployment and PWA | Planned Vercel hosting and browser installation | Serve the first release and support launch from a phone's home screen. |

- **Example data flow.** When adding an idea, the server verifies the session and the friend's ownership, validates the fields, writes an optional photo to private storage, and records the idea and its photo reference in Neon.
- **Architecture boundary to protect.** Keep account and resource authorization on the server and apply it to both database records and photo delivery.
- **Additional coding standards.** Use the [web UI coding standards](web-ui-standards.md) for routes and components that render browser UI.

## Integrations and operations

| Service | Purpose | What happens when it fails | Recovery |
| --- | --- | --- | --- |
| Neon | Persist sessions and application records | The dependent operation reports an error. | Restore the connection and retry the failed operation. |
| Vercel Blob | Store and serve private gift photos | The affected upload or image shows a failure state. | Retry the upload or save the idea without the optional photo. |
| Vercel | Host the web app | A deployment can fail or the app can become unavailable. | Inspect the deployment and runtime logs. |
| Web Push | Deliver proposed post-MVP reminders | A missing permission or inactive subscription prevents delivery. | Define how to renew subscriptions when specifying M3. |

- **Setup, environments, and configuration references.** See the [project README](../README.md) for the current starter commands and the [MCP configuration example](codex-mcp.toml) for development tools. Document service environment variables with safe placeholders when the integrations are added.
- **Deployment, migrations, and rollback.** Use project migrations for schema changes. Define the deployment, migration, and rollback procedure when the services are connected.

## Quality and review priorities

| Rule or quality area | Required behavior or threshold | How to verify |
| --- | --- | --- |
| Account access, F1 | A new visitor can create a personal account and reach the private dashboard after authentication. A returning user can sign in with their existing credentials. | Start as a visitor at `/`, register a new account, verify access to `/app`, and sign back in from a fresh browser session. |
| Solar Hijri calendar, R1–R3 | Countdown, ordering, birthday message, and annual greeting all follow the same occurrence date. | Test today, tomorrow, a birthday already passed, the Solar Hijri year boundary, the confirmed day boundary, and leap and non-leap Esfand. |
| Gift ideas, R4–R5 | Save an idea with only a title or with a photo and source. Purchase toggles persist and keep unpurchased items first. | Exercise the friend page on a phone and confirm the resulting cards after a reload. |
| Ownership, R6 | A signed-in user cannot read or change another account's records or fetch its private photos. | Use two accounts and make direct requests to the other account's page, update operation, and photo path. |
| Responsive Persian UI and accessibility | Every in-scope screen and UI state stays readable and operable at phone and desktop widths. | Exercise each screen and its relevant states at representative narrow and wide browser widths. Check RTL layout, horizontal overflow, touch and keyboard controls, focus, and visible errors. |
| Installation | A user can install and launch the first release using its home-screen icon. | Run the main flow from an installed build on a supported phone in the test environment. |

- **Project-specific review question.** Can a user sign in on a phone, add Sara's Solar Hijri birthday, see the countdown, and quickly save «ماگ آبی» so they can find it later in their account?

## Open questions, decisions, and references

| Topic | Status | Decision or question | Reason or next step |
| --- | --- | --- | --- |
| First account | Decided | Public self-service sign-up with email and password. | Include sign-up and returning-user sign-in in M0. |
| Day boundary | Proposed | Use `Asia/Tehran` as the default boundary for the calendar day. | Confirm before implementing and testing F2 countdowns, F4 birthday messages and greeting status, or the M3 reminder. |
| Esfand 30 in a non-leap year | Proposed | Treat Esfand 29 as that year's birthday occurrence and display date. | Confirm before implementing or testing recurrence in F2 and F4. |
| Birthday data model | Proposed | Store Solar Hijri day and month directly, with optional birth year. | Confirm validation and persistence before creating the M1 schema. |
| Prisma version | Proposed | Evaluate Prisma 7 with Better Auth. | Verify compatibility before installing dependencies for M0. |
| Photo and data lifecycle | Open | What file limits and data deletion and retention rules should apply? | Set upload limits and handling of failed saves for F3 before connecting private photo storage. |
| Theme | Decided | Use the light theme for the first release. Dark mode is deferred to a later release. | Use the light theme in the reference screens. |
| Visual direction | Decided | The implementing agent uses the linked screenshots as visual references and designs, builds, and verifies responsive layouts for every in-scope screen and UI state. | Include responsive behavior and verification in each applicable feature spec. |
| Reminder behavior | Proposed after MVP | Check daily and send Web Push one week before the birthday. | In M3, confirm job timing, permission flow, subscription renewal, and duplicate prevention. |

- **Glossary and references.** A birthday occurrence is the date on which a friend's birthday falls in a given Solar Hijri year. The [agent workflow](agent-workflow.md) describes how to turn this overview into reviewed specs.
