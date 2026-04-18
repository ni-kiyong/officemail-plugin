---
name: omail
description:
  "Overview and quick reference for OfficeMail CLI (omail). Use when the
  user asks general questions about omail capabilities, available commands, schema
  introspection, or environment configuration."
---

# omail — OfficeMail CLI

OfficeMail CLI for AI — let your AI agent read, send, and manage email and calendar
on the OfficeMail service (Cyrus IMAP + Postfix based). This tool works only with
OfficeMail and does not support other email services or generic JMAP servers.

## Binary path

When installed as a plugin, the omail binary is at:

    ${CLAUDE_PLUGIN_DATA}/omail

## Skill guide

| Need                                                               | Skill          |
| ------------------------------------------------------------------ | -------------- |
| First-time setup, login, auth, doctor                              | omail-setup    |
| Email: send, reply, triage, read, search, move, flag, draft, watch | omail-mail     |
| Calendar: agenda, events, free/busy, RSVP, sharing                 | omail-calendar |
| Contacts: list, search, add, update, delete, address books         | omail-contacts |

## Global flags

| Flag                         | Description                           |
| ---------------------------- | ------------------------------------- |
| `--output json\|table\|text` | Output format (default: json)         |
| `--dry-run`                  | Preview JMAP request without sending  |
| `--profile <name>`           | Use a named auth profile              |
| `--account <email>`          | Override default JMAP account         |
| `--verbose`                  | Print JMAP request/response to stderr |

## Exit codes

| Code | Meaning          |
| ---- | ---------------- |
| 0    | Success          |
| 1    | JMAP API error   |
| 2    | Auth error       |
| 3    | Validation error |
| 4    | Connection error |
| 5    | Internal error   |

## Security rules

- NEVER send email without explicit user confirmation (use --dry-run first)
- NEVER delete messages permanently without confirmation
- Always use --dry-run for destructive operations

## Schema

    ${CLAUDE_PLUGIN_DATA}/omail schema                              # list all resources
    ${CLAUDE_PLUGIN_DATA}/omail schema CalendarEvent/get            # specific method
    ${CLAUDE_PLUGIN_DATA}/omail schema calendar.calendarevent.get   # dot notation

## Environment variables

| Variable           | Description                       |
| ------------------ | --------------------------------- |
| `OMAIL_TOKEN`      | Bearer token                      |
| `OMAIL_JMAP_URL`   | JMAP endpoint URL                 |
| `OMAIL_CONFIG_DIR` | Config directory                  |
| `OMAIL_LOG`        | Log level (debug/info/warn/error) |
| `OMAIL_LOG_FILE`   | JSON log directory                |
