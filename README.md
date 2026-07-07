# IAXT

**AI you can trust.**

A flight recorder for AI coding agents on macOS. IAXT observes what
Claude Code, Cursor, Aider, and every other CLI agent actually does
on your machine: every command run, every file touched. You get a
post-session review in one click.

This repository hosts the release downloads and the issue tracker.
Learn more at [iaxt.com](https://iaxt.com).

---

## Download

**[Download the latest release](https://github.com/CoralliumTech/iaxt-releases/releases/latest)**

Requires macOS 13 Ventura or later. Apple Silicon and Intel.
Signed and notarized by Apple.

### Install

1. Open the DMG and drag **IAXT** into **Applications**.
2. Launch IAXT. It appears as an eye icon in your menu bar.
3. Grant **Full Disk Access** when prompted (System Settings,
   Privacy & Security, Full Disk Access) so IAXT can observe file
   activity across your home folder.

### Uninstall

Quit IAXT, drag the app to the Trash, and optionally remove your
local logs with `rm -rf ~/Library/Logs/IAXT`. That is everything;
the app installs nothing else.

---

## Privacy

- **No telemetry, no analytics, no account.** IAXT makes zero
  network calls unless you explicitly click *Check for Updates*.
- All data stays on your machine, in a local SQLite database and
  daily JSONL logs at `~/Library/Logs/IAXT/`, openable with
  `sqlite3` and deletable with `rm -rf`.

---

## Supported AI agents

Claude Code · Cursor · Aider · Codex · Windsurf · Kilo Code ·
OpenCode · Copilot · Cody

### Missing your agent?

[Open an issue](https://github.com/CoralliumTech/iaxt-releases/issues)
with the output of this command **while the agent is running**:

```bash
ps -axo pid,ppid,comm,args | grep -i <your-tool-name>
```

We need the process basename and the first few argv tokens to add
the right detection patterns.

---

© Corallium Tech SL · [iaxt.com](https://iaxt.com)
