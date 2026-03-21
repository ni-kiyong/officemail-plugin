---
name: omail
description: "Use when the user asks about email, calendar, or contacts — read/send/triage mail, check agenda, create events, search contacts, or manage their Officemail/JMAP mailbox. CLI for self-hosted Cyrus IMAP via JMAP."
version: 0.2.30
---

# omail — Officemail CLI

Officemail CLI for AI — let your AI agent read, send, and manage email, calendar, and contacts.
Structured JSON output, dry-run safety, and JMAP-native.

## Binary path

When installed as a plugin, the omail binary is at:

    ${CLAUDE_PLUGIN_DATA}/omail

Use this full path for all commands below.

First-time setup:

    ${CLAUDE_PLUGIN_DATA}/omail auth login --email you@company.com  # OAuth login (opens browser)
    ${CLAUDE_PLUGIN_DATA}/omail auth setup    # or manual: JMAP URL + Bearer token
    ${CLAUDE_PLUGIN_DATA}/omail doctor        # verify connection and capabilities

## Quick Reference

### Read & Triage

    ${CLAUDE_PLUGIN_DATA}/omail mail +triage                         # unread inbox summary
    ${CLAUDE_PLUGIN_DATA}/omail mail +triage --mailbox Sent          # sent mail summary
    ${CLAUDE_PLUGIN_DATA}/omail mail +triage --limit 10              # top 10
    ${CLAUDE_PLUGIN_DATA}/omail mail +triage --page-all              # all unread
    ${CLAUDE_PLUGIN_DATA}/omail mail +read --message-id <id>         # full message body
    ${CLAUDE_PLUGIN_DATA}/omail mail +read --message-id <id> --save-attachments       # download attachments to cwd
    ${CLAUDE_PLUGIN_DATA}/omail mail +read --message-id <id> --save-attachments /tmp  # download to specific dir
    ${CLAUDE_PLUGIN_DATA}/omail mail +search --query "from:bob budget" --limit 20
    ${CLAUDE_PLUGIN_DATA}/omail mail +search --query "report" --page-all   # all results

### Send & Reply

    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to alice@example.com --subject "Hello" --body "Hi"
    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to alice@example.com --subject "Report" --body "See attached" -a report.pdf
    ${CLAUDE_PLUGIN_DATA}/omail mail +reply --message-id <id> --body "Thanks!"
    ${CLAUDE_PLUGIN_DATA}/omail mail +reply --message-id <id> --body "See attached" -a notes.pdf
    ${CLAUDE_PLUGIN_DATA}/omail mail +reply-all --message-id <id> --body "Noted."
    ${CLAUDE_PLUGIN_DATA}/omail mail +reply-all --message-id <id> --body "Noted." -a summary.pdf
    ${CLAUDE_PLUGIN_DATA}/omail mail +forward --message-id <id> --to bob@example.com --body "FYI"
    ${CLAUDE_PLUGIN_DATA}/omail mail +forward --message-id <id> --to bob@example.com --include-attachments
    ${CLAUDE_PLUGIN_DATA}/omail mail +forward --message-id <id> --to bob@example.com -a extra.pdf --include-attachments
    ${CLAUDE_PLUGIN_DATA}/omail mail +draft --to alice@example.com --subject "Draft" --body "WIP"

### Organize

    ${CLAUDE_PLUGIN_DATA}/omail mail +move --message-id <id> --to Archive
    ${CLAUDE_PLUGIN_DATA}/omail mail +flag --message-id <id> --set '$flagged'
    ${CLAUDE_PLUGIN_DATA}/omail mail +flag --message-id <id> --unset '$seen'

### Watch

    ${CLAUDE_PLUGIN_DATA}/omail mail +watch                          # stream new emails as NDJSON

### Calendar

    ${CLAUDE_PLUGIN_DATA}/omail calendar +agenda                         # upcoming events (7 days)
    ${CLAUDE_PLUGIN_DATA}/omail calendar +agenda --days 14 --page-all    # next 2 weeks, all pages
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Meeting" --start "2026-03-25T10:00:00" --end "2026-03-25T11:00:00"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +insert --title "Review" --start "2026-03-25T14:00:00" --end "2026-03-25T15:00:00" --invite alice@example.com
    ${CLAUDE_PLUGIN_DATA}/omail calendar +update --event-id <id> --title "New Title"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +delete --event-id <id>
    ${CLAUDE_PLUGIN_DATA}/omail calendar +freebusy --start "2026-03-25T00:00:00" --end "2026-03-26T00:00:00"
    ${CLAUDE_PLUGIN_DATA}/omail calendar +rsvp --event-id <id> --status accepted

### Contacts

    ${CLAUDE_PLUGIN_DATA}/omail contacts +list                           # all contacts
    ${CLAUDE_PLUGIN_DATA}/omail contacts +search --query "alice"         # search by name/email
    ${CLAUDE_PLUGIN_DATA}/omail contacts +add --name "Alice" --email alice@example.com
    ${CLAUDE_PLUGIN_DATA}/omail contacts +update --contact-id <id> --name "Alice Park"
    ${CLAUDE_PLUGIN_DATA}/omail contacts +delete --contact-id <id>

### Schema

    ${CLAUDE_PLUGIN_DATA}/omail schema                                   # list all resources + server support
    ${CLAUDE_PLUGIN_DATA}/omail schema CalendarEvent/get                 # specific method info
    ${CLAUDE_PLUGIN_DATA}/omail schema calendar.calendarevent.get        # dot notation also works

### Raw JMAP Methods

    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox get
    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox query --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail mail mailbox set --json '{"create":{"m1":{"name":"Archive"}}}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email get --params '{"ids":["<id>"]}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email query --params '{"filter":{"inMailbox":"INBOX"}}'
    ${CLAUDE_PLUGIN_DATA}/omail mail email set --json '{"update":{"<id>":{"keywords/$seen":true}}}'

## Global Flags

| Flag | Description |
|------|-------------|
| `--output json\|table\|text` | Output format (default: json) |
| `--dry-run` | Preview JMAP request without sending |
| `--account <email>` | Override default account |
| `--verbose` | Print JMAP request/response to stderr |

## Exit Codes

| Code | Meaning |
|------|---------|
| 0 | Success |
| 1 | JMAP API error |
| 2 | Auth error |
| 3 | Validation error |
| 4 | Connection error |
| 5 | Internal error |

## Auth

    ${CLAUDE_PLUGIN_DATA}/omail auth login         # OAuth login (opens browser)
    ${CLAUDE_PLUGIN_DATA}/omail auth setup         # manual: JMAP URL + Bearer token
    ${CLAUDE_PLUGIN_DATA}/omail auth logout        # clear stored credentials
    ${CLAUDE_PLUGIN_DATA}/omail auth token <t>     # update Bearer token
    ${CLAUDE_PLUGIN_DATA}/omail auth whoami        # show session info
    ${CLAUDE_PLUGIN_DATA}/omail auth refresh       # force refresh session cache
    ${CLAUDE_PLUGIN_DATA}/omail doctor             # diagnose connection, auth, capabilities

Environment variables (override config file):

| Variable | Description |
|----------|-------------|
| `OMAIL_TOKEN` | Bearer token |
| `OMAIL_JMAP_URL` | JMAP endpoint URL |
| `OMAIL_CONFIG_DIR` | Config directory |
| `OMAIL_LOG` | Log level (debug/info/warn/error) |
| `OMAIL_LOG_FILE` | JSON log directory |

## Security Rules

- NEVER send email without explicit user confirmation (use --dry-run first)
- NEVER delete messages permanently without confirmation
- Always use --dry-run for destructive operations

## Recipes

### Triage and Reply

1. `${CLAUDE_PLUGIN_DATA}/omail mail +triage` — get unread summary
2. `${CLAUDE_PLUGIN_DATA}/omail mail +read --message-id <id>` — read full message
3. `${CLAUDE_PLUGIN_DATA}/omail mail +reply --message-id <id> --body "..." --dry-run` — preview
4. `${CLAUDE_PLUGIN_DATA}/omail mail +reply --message-id <id> --body "..."` — send after confirm

### Draft for Review

1. `${CLAUDE_PLUGIN_DATA}/omail mail +draft --to <email> --subject "..." --body "..."` — save to Drafts
2. User reviews in webmail/mobile
3. User sends manually when ready

## MCP Server

Officemail also runs as an MCP (Model Context Protocol) server for direct AI integration.
For detailed setup instructions (Claude Code plugin or Claude Desktop), see the
**omail-setup** skill.

### Start

    omail mcp serve

### Claude Desktop config

    {
      "mcpServers": {
        "officemail": {
          "command": "omail",
          "args": ["mcp", "serve"]
        }
      }
    }

### Available Tools

| Tool | Description |
|------|-------------|
| `omail_triage` | Get unread inbox summary with message previews |
| `omail_read` | Read full message body, headers, and attachment info |
| `omail_send` | Send a new email |
| `omail_reply` | Reply to a message |
| `omail_reply_all` | Reply-all to a message |
| `omail_forward` | Forward a message to new recipients |
| `omail_search` | Full-text email search with snippets |
| `omail_move` | Move messages to a different mailbox |
| `omail_flag` | Set or unset keywords (flags) on messages |
| `omail_draft` | Save an email draft without sending |
| `omail_mailbox_set` | Create, update, or delete mailboxes (raw Mailbox/set) |
| `omail_mailboxes` | List all mailboxes with unread/total counts |
| `omail_download` | Download an attachment by blobId (returns base64) |
| `omail_whoami` | Show current auth status and account info |
| `omail_jmap` | Execute a raw JMAP method (accountId auto-injected) |

### Resources

- `officemail://mailboxes` — list all mailboxes with counts

### Prompts

- `triage-and-reply` — triage inbox and draft replies
- `draft-for-review` — draft an email for review before sending
