---
name: omail-contacts
description: "Contacts management helpers and raw JMAP contacts methods. Use when the user asks about contacts, address book, wants to find someone's email, or add/update/delete contacts."
version: 0.2.30
---

# omail contacts — Contacts Management

PREREQUISITE: Read ../omail-shared/SKILL.md for auth, global flags, and security rules.

## Browse methods

    ${CLAUDE_PLUGIN_DATA}/omail contacts --help
    ${CLAUDE_PLUGIN_DATA}/omail contacts contactcard get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail contacts addressbook get --params '{...}'

## Helpers

| Command | Description |
|---------|-------------|
| `+list` | List contacts (`--addressbook`, `--limit`, `--page-all`) |
| `+search` | Search contacts by name or email (`--query`, `--limit`) |
| `+add` | Add a new contact (`--name`, `--email`, `--phone`, `--addressbook`) |
| `+update` | Update a contact (`--contact-id`, `--name`, `--email`, `--phone`) |
| `+delete` | Delete a contact (`--contact-id`) |

## Usage Examples

    ${CLAUDE_PLUGIN_DATA}/omail contacts +list
    ${CLAUDE_PLUGIN_DATA}/omail contacts +list --limit 10
    ${CLAUDE_PLUGIN_DATA}/omail contacts +list --page-all
    ${CLAUDE_PLUGIN_DATA}/omail contacts +list --addressbook <id>
    ${CLAUDE_PLUGIN_DATA}/omail contacts +search --query "alice"
    ${CLAUDE_PLUGIN_DATA}/omail contacts +search --query "kim" --limit 5
    ${CLAUDE_PLUGIN_DATA}/omail contacts +add --name "Alice Kim" --email alice@example.com
    ${CLAUDE_PLUGIN_DATA}/omail contacts +add --name "Bob Lee" --email bob@example.com --phone "+82-10-1234-5678"
    ${CLAUDE_PLUGIN_DATA}/omail contacts +add --name "Carol" --email carol@example.com --addressbook <id>
    ${CLAUDE_PLUGIN_DATA}/omail contacts +update --contact-id <id> --name "Alice Park"
    ${CLAUDE_PLUGIN_DATA}/omail contacts +update --contact-id <id> --email newemail@example.com
    ${CLAUDE_PLUGIN_DATA}/omail contacts +delete --contact-id <id>

## Raw methods

    ${CLAUDE_PLUGIN_DATA}/omail contacts contactcard get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail contacts contactcard query --params '{"filter":{"text":"alice"}}'
    ${CLAUDE_PLUGIN_DATA}/omail contacts contactcard set --json '{"create":{"c1":{"fullName":"Test","emails":{"e1":{"address":"test@example.com"}}}}}'
    ${CLAUDE_PLUGIN_DATA}/omail contacts addressbook get --params '{...}'
    ${CLAUDE_PLUGIN_DATA}/omail contacts addressbook query --params '{...}'

## Notes

- Server must support `urn:ietf:params:jmap:contacts` capability (check with `omail doctor`)
- Contact names use `fullName` (single string field)
- Always use `--dry-run` first when modifying contacts via AI
