---
name: omail-setup
description: "Set up Officemail CLI — configure JMAP server connection and verify it works"
version: 0.1.7
---

# omail setup

IMPORTANT: `auth setup` is interactive and requires user input.
Do NOT run it directly. Instead, ask the user to run it in their terminal.

## Step 1: Check binary

Verify the binary exists:

    ${CLAUDE_PLUGIN_DATA}/omail --version

If missing, ask the user to restart the session.

## Step 2: Auth setup

Tell the user to run this command in their terminal (NOT via Claude):

    ${CLAUDE_PLUGIN_DATA}/omail auth setup

They will enter their JMAP server domain and Bearer token interactively.

## Step 3: Verify connection

After the user completes auth setup, verify:

    ${CLAUDE_PLUGIN_DATA}/omail doctor

## Step 4: Test

    ${CLAUDE_PLUGIN_DATA}/omail mail +triage

If this returns inbox data, setup is complete.
