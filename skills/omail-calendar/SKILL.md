---
name: omail-calendar
description: "Calendar management helpers and raw JMAP calendar methods. Use when the user asks about calendar events, scheduling, agenda, free/busy status, or wants to create/update/delete events."
version: 0.2.34
---

# omail calendar — Calendar Management

PREREQUISITE: Read ../omail-shared/SKILL.md for auth, global flags, and security rules.

## Browse methods

    ${CLAUDE_PLUGIN_DATA}/omail calendar --help
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendarevent get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendar get --params '{...}'

## Helpers

| Command | Description |
|---------|-------------|
| `+agenda` | Upcoming events (default: 7 days, `--page-all`) |
| `+insert` | Create a new calendar event (`--invite` for attendees) |
| `+update` | Update an existing event (`--series` for recurring) |
| `+delete` | Delete an event (`--series` for recurring) |
| `+freebusy` | Check free/busy status for a time range |
| `+rsvp` | Accept, decline, or tentative an invitation |

## Usage Examples

    ${CLAUDE_PLUGIN_DATA}/omail calendar +agenda
    ${CLAUDE_PLUGIN_DATA}/omail calendar +agenda --days 14 --timezone Asia/Seoul
    ${CLAUDE_PLUGIN_DATA}/omail calendar +agenda --page-all --limit 100
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Team Meeting" --start "2026-03-25T10:00:00" --end "2026-03-25T11:00:00"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Lunch" --start "2026-03-25T12:00:00" --end "2026-03-25T13:00:00" --location "Cafe"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Review" --start "2026-03-25T14:00:00" --end "2026-03-25T15:00:00" --invite alice@example.com bob@example.com
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Sprint" --start "2026-03-25T09:00:00" --end "2026-03-25T10:00:00" --description "Weekly sprint review" --calendar <calendarId>
    ${CLAUDE_PLUGIN_DATA}/omail calendar +rsvp --event-id <id> --status accepted
    ${CLAUDE_PLUGIN_DATA}/omail calendar +rsvp --event-id <id> --status declined
    ${CLAUDE_PLUGIN_DATA}/omail calendar +rsvp --event-id <id> --status tentative
    ${CLAUDE_PLUGIN_DATA}/omail calendar +update --event-id <id> --title "New Title"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +update --event-id <id> --start "2026-03-25T14:00:00" --end "2026-03-25T15:00:00"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +update --event-id <id> --location "Room 302" --description "Updated agenda"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +update --event-id <id> --series --title "Weekly Standup"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +delete --event-id <id>
    ${CLAUDE_PLUGIN_DATA}/omail calendar +delete --event-id <id> --series
    ${CLAUDE_PLUGIN_DATA}/omail calendar +freebusy --start "2026-03-25T00:00:00" --end "2026-03-26T00:00:00"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +freebusy --start "2026-03-25T00:00:00" --end "2026-03-26T00:00:00" --email alice@example.com

## Raw methods

    ${CLAUDE_PLUGIN_DATA}/omail calendar calendarevent get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendarevent query --params '{"filter":{}}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendarevent set --json '{"create":{"e1":{"title":"Test","start":"2026-03-25T10:00:00","duration":"PT1H","calendarIds":{"<calId>":true}}}}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendar get --params '{}'

## Notes

- Server must support `urn:ietf:params:jmap:calendars` capability (check with `omail doctor`)
- Dates use ISO 8601 local time, no milliseconds: `2026-03-25T10:00:00` (not `.000Z`)
- Recurring events: use `--series` flag on `+update` and `+delete`
- `--invite` adds participants with iMIP `sendTo` (server sends invitations automatically)
- `+rsvp` updates your `participationStatus` on an invited event
- `+agenda` and `+freebusy` use client-side date filtering
  (server does not support `after`/`before` filters)
- `+agenda` supports `--days`, `--timezone`, `--limit`, `--page-all`
- `+insert` auto-resolves default calendar via `Calendar/get` when `--calendar` is omitted
- JSCalendar uses `locations` (plural, keyed object) — not `location`
- `Calendar/query` is not supported; use `Calendar/get` to list calendars
- Always use `--dry-run` first when creating or modifying events via AI
