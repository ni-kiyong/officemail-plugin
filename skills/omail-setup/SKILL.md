---
name: omail-setup
description: "Set up Officemail CLI — configure JMAP server connection and verify it works"
version: 0.1.10
---

# omail setup

## Step 1: Check binary

Verify the binary exists:

    ${CLAUDE_PLUGIN_DATA}/omail --version

If missing, ask the user to restart the session.

## Step 2: Auth setup

Ask the user for their JMAP server domain and Bearer token, then run:

    ${CLAUDE_PLUGIN_DATA}/omail auth setup --url <domain> --token <token>

Example:

    ${CLAUDE_PLUGIN_DATA}/omail auth setup --url jmap.example.com --token eyJhbGci...

## Step 3: Verify connection

    ${CLAUDE_PLUGIN_DATA}/omail doctor

## Step 4: Test

    ${CLAUDE_PLUGIN_DATA}/omail mail +triage

If this returns inbox data, setup is complete.
