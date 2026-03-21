---
name: omail-calendar
description: "Calendar management helpers and raw JMAP calendar methods. Use when the user asks about calendar events, scheduling, agenda, free/busy status, or wants to create/update/delete events."
version: 0.2.29
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
| `+agenda` | Upcoming events (default: 7 days) |
| `+insert` | Create a new calendar event |
| `+update` | Update an existing event (`--series` for recurring) |
| `+delete` | Delete an event (`--series` for recurring) |
| `+freebusy` | Check free/busy status for a time range |

## Usage Examples

    ${CLAUDE_PLUGIN_DATA}/omail calendar +agenda
    ${CLAUDE_PLUGIN_DATA}/omail calendar +agenda --days 14 --timezone Asia/Seoul
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Team Meeting" --start "2026-03-25T10:00:00" --end "2026-03-25T11:00:00"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Lunch" --start "2026-03-25T12:00:00" --end "2026-03-25T13:00:00" --location "Cafe"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +update --event-id <id> --title "New Title"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +update --event-id <id> --start "2026-03-25T14:00:00" --end "2026-03-25T15:00:00"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +delete --event-id <id>
    ${CLAUDE_PLUGIN_DATA}/omail calendar +delete --event-id <id> --series
    ${CLAUDE_PLUGIN_DATA}/omail calendar +freebusy --start "2026-03-25T00:00:00Z" --end "2026-03-26T00:00:00Z"

## Raw methods

    ${CLAUDE_PLUGIN_DATA}/omail calendar calendarevent get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendarevent query --params '{"filter":{"after":"2026-03-25T00:00:00Z"}}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendarevent set --json '{"create":{"e1":{"title":"Test","start":"2026-03-25T10:00:00","duration":"PT1H"}}}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendar get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail calendar calendar query --params '{...}'

## Notes

- Server must support `urn:ietf:params:jmap:calendars` capability (check with `omail doctor`)
- Dates use ISO 8601 format
- Recurring events: use `--series` flag to affect the entire series
- Always use `--dry-run` first when creating or modifying events via AI
