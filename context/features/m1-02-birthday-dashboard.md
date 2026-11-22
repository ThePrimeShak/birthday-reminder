# Upcoming birthday dashboard

## Outcome

The dashboard tells a user whose birthday is next and identifies birthdays happening today. This covers F2 and rules R1–R2. [Project overview](../project-overview.md)

## Scope

Calculate the next Solar Hijri birthday occurrence and calendar-day countdown. Use the result to sort the account's friends and render their names, dates, countdowns, and gift idea counts. Expose the birthday occurrence and its year for annual greetings.

## Dependencies

Requires [friend creation](m1-01-add-friends.md). Confirm the day boundary and the rule for Esfand 30 in a non-leap year before implementing and testing recurrence. The overview records `Asia/Tehran` and Esfand 29 as proposals.

## Visual reference

Use the friend-card hierarchy, countdown, gift count, and emphasis for today's birthday. Keep long names and counts readable on phones. [Dashboard](../screenshots/home-page.png)

## Acceptance criteria

- The dashboard orders friends by increasing calendar days to their next birthday. Past birthdays count toward their next occurrence in the following Solar Hijri year.
- Each card shows the friend name, Solar Hijri birthday date under the confirmed calendar policy, and gift idea count. A friend without ideas shows zero. The count reflects saved ideas once the gift feature is available.
- A birthday occurring today appears before future birthdays and shows copy such as «🎂 امروز تولد ساراست». The same calculation supplies the occurrence date and year throughout the flow.
- The cards and relevant empty, loading, and error states fit phone and desktop widths in the light Persian RTL interface.

## Verification cases

- Test today, tomorrow, an already-passed birthday, and a date crossing the Solar Hijri year boundary. Test leap and non-leap Esfand and times on either side of the confirmed day boundary.
- Verify card order, the today message, and the display of name, date, and count. Recheck a nonzero count after gift idea persistence is available.
- Exercise the dashboard with representative phone and desktop widths, including long content and the empty state.
