---
name: maid-browser-use
description: >-
  Use Maid's browser CLI to drive the browser tabs inside the Maid app on
  Windows: open a tab, navigate to a URL, go back and forward, reload, wait for
  a page to finish loading, list, inspect, switch, create, or close browser tabs,
  read the page — an ARIA snapshot of its elements, an arbitrary JavaScript
  expression, a property of one element, or a yes/no about its state — and act on
  elements: click, double-click, fill, select, check, focus, clear, hover, scroll into
  view, highlight, type, press a key, or insert text — and drive the mouse itself:
  move the pointer to a coordinate, press or release a button, turn the wheel, or
  drag one element onto another. Use for
  "browser use", "maid browser", "open a page in Maid", "navigate the Maid
  browser", "list browser tabs", "what is on this page", "read the page", and
  "check the page I am logged into", "click that button", "fill in the form",
  "drag this onto that", and "click at these coordinates".
  Use maid-computer-use instead for browser windows outside Maid (Chrome, Edge)
  and for any other desktop UI, and use maid-orchestration for coordinating work
  between agent terminals.
version: 1.9.0
---

# Maid Browser Use (Windows)

This file is a discovery stub, not the usage guide. The full, version-matched browser
reference is served by the `maid-cli` binary itself — kept out of this file on purpose so it
can never drift from the binary that will actually run your commands.

```text
maid-cli skills get maid-browser-use
```

Engage Maid's browser surface when the target is a **browser tab inside the Maid app** —
tabs that sit beside the terminal tabs in the same window. Because they are the user's own
tabs, pages opened here keep the logins the user already has in that browser profile.

Use `maid-computer-use` instead for browser *windows* outside Maid (Chrome, Edge, Firefox)
and for any other desktop UI, and `maid-orchestration` for coordinating work between agent
terminals.

This provider is **Windows-only**.

## This surface talks to the running app

Like `maid-orchestration` and unlike `maid-computer-use`, these commands do not act alone —
the tabs live inside the Maid app and the CLI reaches it over a named pipe. **The app must
be running and "Agent 브라우저 사용" must be on** (Settings → Browser). If it is not, every
command answers with a JSON error saying so; the CLI will not launch the app for you,
because that would tie the app's lifetime to a single command.

## Two contracts worth knowing before you read the guide

- **Nothing is created implicitly.** With no browser tab open, commands refuse rather than
  opening one for you, so that choosing `tab create` stays your decision.
- **Element references expire.** Reading the page hands you `[ref=eN]` tags; navigating or
  reloading throws the whole set away and a later use of one answers with a dedicated code
  meaning "take a fresh snapshot" — not "the element is gone".

## Orientation commands

These are stable and safe to run before you have read the guide:

```text
maid-cli browser tab list --json
maid-cli browser tab current --json
maid-cli browser snapshot --json
```

Beyond these, read the guide rather than guessing a command surface. Every command answers
with JSON on stdout — **errors too**, carrying a machine-readable code.

**Drain stdout while the command runs — never wait for exit and read afterwards.** A caller
that blocks on process exit before reading can deadlock: the CLI is blocked on a write
nobody is reading, and neither side moves. Use a call that reads and waits together
(`subprocess.run(..., capture_output=True)`, `Command::output()`, `execFile`).
