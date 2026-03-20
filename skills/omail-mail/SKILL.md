---
name: omail-mail
description: "Email management helpers and raw JMAP mail methods reference"
version: 0.1.7
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
| `+send` | Send an email |
| `+reply` | Reply (auto-threading) |
| `+reply-all` | Reply-all |
| `+forward` | Forward a message |
| `+triage` | Unread inbox summary |
| `+read` | Read message body |
| `+search` | Full-text search |
| `+move` | Move between mailboxes |
| `+flag` | Set/unset keywords |
| `+draft` | Save to Drafts |
| `+watch` | Watch for new emails (NDJSON stream) |

## Raw methods

    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox query --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email get --params '{"ids":["<id>"],"properties":["subject","from","bodyValues"]}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email query --params '{"filter":{"inMailbox":"INBOX"}}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email set --json '{"update":{"<id>":{"mailboxIds":{"<mailboxId>":true}}}}'
    ${CLAUDE_PLUGIN_DATA}/omail mail thread get --params '{"ids":["<id>"]}'
