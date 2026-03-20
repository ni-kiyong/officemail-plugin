---
name: omail-mail-send
description: "Send email via omail CLI with attachments, CC/BCC, HTML body support"
version: 0.1.13
---

# omail mail +send — Send an email

PREREQUISITE: Read ../omail-shared/SKILL.md for auth, global flags, and security rules.

## Usage

    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to <email> --subject <text> --body <text>
    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to <email> --subject <text> --body <text> --cc <email>
    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to <email> --subject <text> --body '<b>Bold</b>' --html
    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to <email> --subject <text> --body <text> --from <alias>
    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to <email> --subject <text> --body <text> -a report.pdf
    ${CLAUDE_PLUGIN_DATA}/omail mail +send --to <email> --subject <text> --body <text> -a a.pdf -a b.csv

## Flags

| Flag | Required | Description |
|------|----------|-------------|
| `--to` | Yes | Recipient email(s) |
| `--subject` | Yes | Subject line |
| `--body` | Yes | Message body (plain text or HTML) |
| `--cc` | No | CC recipients |
| `--bcc` | No | BCC recipients |
| `--from` | No | Send-as alias |
| `--html` | No | Treat body as HTML |
| `-a, --attach` | No | File attachment (repeatable, max 25MB total) |
| `--dry-run` | No | Preview without sending |

## Notes

- Handles MIME encoding automatically via JMAP EmailSubmission
- Use --dry-run first when composing with an AI agent
- Requires server support for urn:ietf:params:jmap:submission
