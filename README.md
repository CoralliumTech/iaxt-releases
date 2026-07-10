# IAXT

**AI you can trust.**

A flight recorder for AI coding agents on macOS. IAXT passively records
what Claude Code, Cursor, Aider, Codex, and other coding agents actually
do on your Mac: commands run, files changed, packages installed, git
operations, and launch agents. It never blocks or changes anything, and
it runs entirely in user space with no kernel extension.

IAXT is not a raw log. A custom filter built specifically for AI-agent
activity cuts through the noise, so instead of scrolling a firehose you
review a short list of what actually matters. Every action is attributed
to the agent session responsible and sorted into three tiers:

- **Routine.** Normal development, recorded and kept out of your way.
- **Flagged.** An FYI worth a glance: a download, a package install, a
  new git remote, a permission change.
- **Review.** The 1% or less worth checking just in case: persistence
  (login items, cron), credential access, or unexpected network calls.

You look after the session, not during it, and the answer to "what did
the AI actually do" is one glance.

This repository hosts the release downloads and the issue tracker.
Learn more at [iaxt.com](https://iaxt.com).

---

## Why

AI coding agents are fast, and they run with broad access to your machine.
Two things go wrong. Over a long session, approval fatigue sets in, and it
is easy to wave through an action that read as routine but was a little
different. And prompt injection, where an attacker hides instructions
inside content the agent reads, can turn a helpful agent into one that
installs persistence or sends a key out over the network. The permission
dialog is an illusion of control against both, because both end at a tired
human clicking Approve. IAXT is the record that shows you, calmly and
after the fact, what the agent actually did on your Mac.

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
- **It only sees work that runs on your Mac.** Agents in the cloud
  (Claude Cowork, ChatGPT Code Interpreter, Devin, Replit) run on vendor
  machines, and an agent you drive over SSH runs on the remote host. That
  off-machine work is out of scope; over SSH, IAXT still sees the local
  `ssh` process, just not what the agent does on the far side.

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
