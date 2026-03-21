---
name: omail-setup
description: "Set up Officemail CLI — login via OAuth or configure JMAP server connection"
version: 0.2.24
---

# omail setup

## Claude Code Plugin Setup

### Step 1: Check binary

Verify the binary exists:

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

#### Option B: Manual setup (JMAP URL + Bearer token)

Ask the user for their JMAP server domain and Bearer token, then run:

    ${CLAUDE_PLUGIN_DATA}/omail auth setup --url <domain> --token <token>

Example:

    ${CLAUDE_PLUGIN_DATA}/omail auth setup --url jmap.example.com --token eyJhbGci...

### Step 3: Verify connection

    ${CLAUDE_PLUGIN_DATA}/omail doctor

### Step 4: Test

    ${CLAUDE_PLUGIN_DATA}/omail mail +triage

If this returns inbox data, setup is complete.

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
