---
name: omail-mcp
description: "Officemail MCP server setup and tool reference. Use when the user asks
  about MCP server configuration, Claude Desktop integration, available MCP tools,
  or wants to run omail as an MCP server."
version: 0.2.35
---

# omail MCP — Model Context Protocol Server

Officemail runs as an MCP server for direct AI integration
(Claude Desktop, Claude Code, or any MCP-compatible client).

## Start

    omail mcp serve

## Claude Desktop Setup

### Step 1: Install via .mcpb

Download the `.mcpb` file for your platform from the
[releases page](https://github.com/ni-kiyong/officemail-plugin/releases)
(`officemail-{platform}.mcpb`). Double-click to install — the binary and
MCP server config are included for one-click setup.

### Step 2: Login

Run in terminal:

    omail auth login --email you@company.com

### Step 3: Restart Claude Desktop

Restart Claude Desktop to load the MCP server. You should see officemail
tools available in the tools menu.

### Manual config

Add to Claude Desktop settings:

    {
      "mcpServers": {
        "officemail": {
          "command": "omail",
          "args": ["mcp", "serve"]
        }
      }
    }

## Available Tools

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

## Resources

- `officemail://mailboxes` — list all mailboxes with counts

## Prompts

- `triage-and-reply` — triage inbox and draft replies
- `draft-for-review` — draft an email for review before sending
