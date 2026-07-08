# IAXT

**AI you can trust.**

A flight recorder for AI coding agents on macOS. IAXT passively records
what Claude Code, Cursor, Aider, Codex, and other CLI agents actually do
on your machine: every command run, file touched, package installed, git
operation, and launch agent. It never blocks or changes anything. You
review it after the session, in a clear log where each action is
attributed to its agent and scored for severity.

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

## What IAXT does not do

An audit tool is only worth the trust it earns, so the limits are
stated plainly:

- **It does not block.** IAXT is a recorder, not a firewall. It never
  intercepts or changes what an agent does; it lets you review after
  the fact.
- **It logs that a file changed, not what changed.** Use `git diff`
  for the contents.
- **It watches writes, not reads.** A silent read of `~/.ssh/id_rsa`
  is invisible unless the agent then uses it (a `curl`, a commit, a
  POST).
- **It cannot see remote-sandbox work.** Agents that run in the cloud
  (Claude Cowork, ChatGPT Code Interpreter, Devin, Replit) leave no
  local trace, so that work is out of scope.

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
