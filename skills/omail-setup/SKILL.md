---
name: omail-setup
description: "Set up Officemail CLI — OAuth login, manual JMAP configuration, token
  refresh, auth troubleshooting, and connection diagnostics (doctor). Use when the
  user asks to log in, configure auth, fix connection issues, or set up omail for
  the first time."
version: 0.2.46
---

# omail setup — Officemail Auth & Diagnostics

> This tool connects only to the Officemail service (Cyrus IMAP + Postfix based).

## Binary path

    ${CLAUDE_PLUGIN_DATA}/omail

## Claude Code Plugin Setup

### Step 1: Check binary

    ${CLAUDE_PLUGIN_DATA}/omail --version

If missing, ask the user to restart the session.

### Step 2: Login

#### Option A: OAuth login (recommended for OfficeNEXT users)

Ask the user for their email address, then run:

    ${CLAUDE_PLUGIN_DATA}/omail auth login --email <email>

For dev environment:

    ${CLAUDE_PLUGIN_DATA}/omail auth login --email <email> --env dev

A browser window will open for authentication. The user clicks "Sign in",
completes OAuth login in the popup, and tokens are saved automatically.

#### Option B: Manual setup (Officemail JMAP URL + Bearer token)

    ${CLAUDE_PLUGIN_DATA}/omail auth setup --url <officemail-domain> --token <token>

Example:

    ${CLAUDE_PLUGIN_DATA}/omail auth setup --url jmap.officemail.example.com --token eyJhbGci...

### Step 3: Verify connection

    ${CLAUDE_PLUGIN_DATA}/omail doctor

### Step 4: Test

    ${CLAUDE_PLUGIN_DATA}/omail mail +triage

If this returns inbox data, setup is complete.

## Auth commands

    ${CLAUDE_PLUGIN_DATA}/omail auth login         # OAuth login (opens browser)
    ${CLAUDE_PLUGIN_DATA}/omail auth setup         # manual: server URL + Bearer token
    ${CLAUDE_PLUGIN_DATA}/omail auth logout        # clear stored credentials
    ${CLAUDE_PLUGIN_DATA}/omail auth token <t>     # update Bearer token
    ${CLAUDE_PLUGIN_DATA}/omail auth whoami        # verify current session
    ${CLAUDE_PLUGIN_DATA}/omail auth refresh       # force refresh session cache
    ${CLAUDE_PLUGIN_DATA}/omail doctor             # diagnose connection, auth, capabilities

## Notes

- Config stored at `~/.config/officemail/config.json` (chmod 600)
- Claude Code plugin, Claude Desktop MCP, and CLI all share the same config
- Session uses lazy refresh (refresh on 401, retry once)
