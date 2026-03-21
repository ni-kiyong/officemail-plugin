---
name: omail-mail-triage
description: "Triage unread inbox, get email summaries, and follow triage-and-reply recipe"
version: 0.2.33
---

# omail mail +triage — Inbox Summary

PREREQUISITE: Read ../omail-shared/SKILL.md for auth, global flags, and security rules.

## Usage

    ${CLAUDE_PLUGIN_DATA}/omail mail +triage                         # unread INBOX summary
    ${CLAUDE_PLUGIN_DATA}/omail mail +triage --mailbox Sent          # sent mail summary
    ${CLAUDE_PLUGIN_DATA}/omail mail +triage --limit 10              # top 10 only
    ${CLAUDE_PLUGIN_DATA}/omail mail +triage --page-all              # all unread messages

## Flags

| Flag | Required | Default | Description |
|------|----------|---------|-------------|
| `--mailbox` | No | INBOX | Mailbox name or role |
| `--limit` | No | 50 | Max results per page |
| `--page-all` | No | false | Fetch all pages |

## Output (JSON)

    {
      "mailbox": "INBOX",
      "totalEmails": 142,
      "unreadEmails": 5,
      "showing": 5,
      "total": 5,
      "pageAll": false,
      "messages": [
        {
          "id": "msg001",
          "from": "alice@example.com",
          "subject": "Budget Q2",
          "receivedAt": "2026-03-20T09:00:00Z",
          "preview": "Hi, please review...",
          "hasAttachment": true,
          "isRead": false,
          "isFlagged": false
        }
      ]
    }

When `--page-all` is used, `total` reflects the count across all pages.

## Recipe: Triage and Reply

1. Get unread summary: `${CLAUDE_PLUGIN_DATA}/omail mail +triage`
2. Read a message: `${CLAUDE_PLUGIN_DATA}/omail mail +read --message-id <id>`
3. Draft reply (dry-run): `${CLAUDE_PLUGIN_DATA}/omail mail +reply --message-id <id> --body "..." --dry-run`
4. Send after user confirms: `${CLAUDE_PLUGIN_DATA}/omail mail +reply --message-id <id> --body "..."`
