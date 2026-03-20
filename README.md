# Officemail Plugin

Officemail plugin for Claude Code — let your AI agent read, send, and manage email.

## Install

### Claude Code (CLI)

```bash
claude plugin add ni-kiyong/officemail-plugin
```

### Inside Claude Code

```text
/plugin marketplace add ni-kiyong/officemail-plugin
/plugin install officemail@officemail
```

After installing, run the setup skill:

```text
/officemail:omail-setup
```

## What's included

- **Skills** — AI agent instructions for email management
- **Hooks** — auto-installs the `omail` binary on first session
- **Binary** — prebuilt for macOS, Linux, Windows (arm64, x64)

## Manual binary install

Download from the
[releases page](https://github.com/ni-kiyong/officemail-plugin/releases):

```bash
curl -L -o omail https://github.com/ni-kiyong/officemail-plugin/releases/latest/download/omail-darwin-arm64
chmod +x omail
sudo mv omail /usr/local/bin/
```
