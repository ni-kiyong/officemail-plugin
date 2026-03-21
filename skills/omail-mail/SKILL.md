---
name: omail-mail
description: "Email management helpers and raw JMAP mail methods reference"
version: 0.2.33
---

# omail mail — Email Management

PREREQUISITE: Read ../omail-shared/SKILL.md for auth, global flags, and security rules.

## Browse methods

    ${CLAUDE_PLUGIN_DATA}/omail mail --help
    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email get --params '{...}'

## Helpers

| Command | Description |
|---------|-------------|
| `+send` | Send an email (`-a` for attachments, `--cc`, `--bcc`, `--html`, `--from`) |
| `+reply` | Reply with auto-threading (`-a` for attachments) |
| `+reply-all` | Reply-all (`-a` for attachments) |
| `+forward` | Forward (`-a`, `--include-attachments` for originals) |
| `+triage` | Unread inbox summary (`--mailbox`, `--limit`, `--page-all`) |
| `+read` | Read message body (`--raw`, `--save-attachments [dir]`) |
| `+search` | Full-text search (`--query`, `--mailbox`, `--limit`, `--page-all`) |
| `+move` | Move between mailboxes |
| `+flag` | Set/unset keywords |
| `+draft` | Save to Drafts (`--cc`, `--html`) |
| `+watch` | Watch for new emails (NDJSON stream, `--types`) |

## Raw methods

    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox query --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox set --json '{"create":{"m1":{"name":"Archive"}}}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email get --params '{"ids":["<id>"],"properties":["subject","from","bodyValues"]}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email query --params '{"filter":{"inMailbox":"INBOX"}}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email set --json '{"update":{"<id>":{"mailboxIds":{"<mailboxId>":true}}}}'
    ${CLAUDE_PLUGIN_DATA}/omail mail thread get --params '{"ids":["<id>"]}'

## MCP Server

All mail helpers above are also available as MCP tools via `omail mcp serve`.
See the `omail` skill docs for Claude Desktop config and full tool list.
