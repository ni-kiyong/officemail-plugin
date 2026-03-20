---
name: omail-shared
description: "Shared auth, global flags, exit codes, and security rules for all omail commands"
version: 0.1.13
---

# omail — Officemail CLI

Officemail CLI for AI — let your AI agent read, send, and manage email.

## Binary path

When installed as a plugin, the omail binary is at:

    ${CLAUDE_PLUGIN_DATA}/omail

Use this full path for all omail commands below.

## Auth

    ${CLAUDE_PLUGIN_DATA}/omail auth login         # OAuth login (opens browser)
    ${CLAUDE_PLUGIN_DATA}/omail auth setup         # manual: server URL + Bearer token
    ${CLAUDE_PLUGIN_DATA}/omail auth logout        # clear stored credentials
    ${CLAUDE_PLUGIN_DATA}/omail auth token <t>     # update Bearer token
    ${CLAUDE_PLUGIN_DATA}/omail auth whoami        # verify current session
    ${CLAUDE_PLUGIN_DATA}/omail auth refresh       # force refresh session cache
    ${CLAUDE_PLUGIN_DATA}/omail doctor             # diagnose connection, auth, capabilities

## Global flags

| Flag | Description |
|------|-------------|
| `--output json\|table\|text` | Output format (default: json) |
| `--dry-run` | Preview the JMAP request without sending |
| `--account <email>` | Override default account |
| `--verbose` | Print JMAP request/response to stderr |

## Exit codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | JMAP API error |
| 2 | Auth error |
| 3 | Validation error |
| 4 | Connection error |
| 5 | Internal error |

## Security rules

- NEVER send email without explicit user confirmation (use --dry-run first)
- NEVER delete messages permanently without confirmation
- Always use --dry-run for destructive operations during development
