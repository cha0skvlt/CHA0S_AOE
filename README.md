# CHA0S AOE — Agentic Operations Environment

[![Version](https://img.shields.io/badge/version-2.0.1-blue?style=flat-square)](https://github.com/cha0skvlt/CHA0S_AOE/releases)
[![License](https://img.shields.io/badge/license-EULA-orange?style=flat-square)](LICENSE-NOTICE.md)
[![Binary](https://img.shields.io/badge/ships%20as-signed%20binary-success?style=flat-square)](SECURITY.md)
![macOS](https://img.shields.io/badge/macOS-primary-000000?style=flat-square&logo=apple&logoColor=white)
![Linux](https://img.shields.io/badge/Linux-in%20tree-FCC624?style=flat-square&logo=linux&logoColor=black)

[![Rust](https://img.shields.io/badge/Rust-2024-000000?style=flat-square&logo=rust&logoColor=white)](https://www.rust-lang.org)
![GPUI](https://img.shields.io/badge/engine-GPUI-4B8BBE?style=flat-square)
![Metal](https://img.shields.io/badge/GPU-Metal-8E8E93?style=flat-square&logo=apple&logoColor=white)
[![Postgres](https://img.shields.io/badge/memory-Postgres%20%2B%20pgvector-4169E1?style=flat-square&logo=postgresql&logoColor=white)](#agent-memory--the-phylactery)
![SQLite](https://img.shields.io/badge/threads-SQLite-003B57?style=flat-square&logo=sqlite&logoColor=white)
[![CEF](https://img.shields.io/badge/browser-CEF-4285F4?style=flat-square&logo=googlechrome&logoColor=white)](#browser-with-osint)

[![Tor](https://img.shields.io/badge/OSINT-Tor-7D4698?style=flat-square&logo=torproject&logoColor=white)](#browser-with-osint)
[![I2P](https://img.shields.io/badge/OSINT-I2P-6E4C9C?style=flat-square)](#browser-with-osint)
[![IPFS](https://img.shields.io/badge/OSINT-IPFS%20%2F%20Kubo-65C2CB?style=flat-square&logo=ipfs&logoColor=white)](#browser-with-osint)
[![Ollama](https://img.shields.io/badge/models-Ollama-000000?style=flat-square&logo=ollama&logoColor=white)](#models)
[![BYOK](https://img.shields.io/badge/models-BYOK%20%2B%20OpenAI%20compatible-412991?style=flat-square)](#models)
![Nix](https://img.shields.io/badge/build-Nix-5277C3?style=flat-square&logo=nixos&logoColor=white)

A native Rust environment where agents work alongside you: your shell, your files, your data, your browser. One binary, GPU-rendered, running on your disk. Runs on any model — local or by API.

> [!NOTE]
> This repository is the product's public home: documentation, releases, signatures, and issues. CHA0S ships as a signed binary under the EULA delivered with it. See [LICENSE-NOTICE.md](LICENSE-NOTICE.md).

---

## What it is

CHA0S AOE is a local-first **Agentic Operations Environment** for technical operators: infrastructure work, system administration, incident response, OSINT, authorized penetration testing, red-team engagements — first-class operations.

The operational model: **operator → objective → agent → tools + memory → live systems → result**.

The agent writes and modifies code when an objective requires it; software development is one capability of the instrument.

## Capabilities

### The engine
A GPU-rendered Rust core. Ships as one native binary; agents run in-process with your editor, terminal, and browser. Startup is instant; the whole environment is a single application.

### Everything on your disk
Files, memory, databases, and browsing live on your machine. Metrics bind to loopback — one environment variable silences them. The binary works offline: launch, keys, files, threads, and the local-model agent need no internet.

### Agent memory — the Phylactery
Each agent keeps persistent memory in an external Postgres/pgvector store: facts, lessons, operational knowledge — accumulated across sessions. Hybrid search, exact and semantic, retrieves it on demand. It survives restarts, model swaps, and machine migrations. Your database, your DSN, your data.

### Custom agents
As many agents as you need. Each carries its own profile: system prompt — personality, language, discipline; its own Phylactery DSN; its own tool allowlist. Skills and playbooks are shared tiers — project-local, machine-global, built-in. Switch between agents per thread.

### Agents run the environment
The whole environment is the agent's control panel. Windows, panes, tabs, docks, settings, logs — the agent reads and drives them all as tools, in the same session you use. Turn on a solo cycle and the agent works on its own — starting from your instruction — until you turn it off. It reports as it goes; you stay the operator.

### Browser with OSINT
The agents drive the browser. Navigate, click, type, read live pages — the browser is a tool. OSINT search spans clearnet, onion, and I2P; Tor, i2pd, and Kubo run as local processes on demand. Research runs on your machine; you watch.

### The lock
One switch in the agent footer. On: file tools and terminal confined to the open project, OS-level sandbox on local commands. Off: the agent works in your shell with your rights — the whole machine and its remote sessions. Your call, your risk.

## What's inside

### Surfaces

The center of every window is one exclusive lane at a time: **Editor / Browser / Log / Search / Console**.

- **Editor** — tree-sitter parsing across 22 built-in languages (bash, c, cpp, css, diff, go, gomod, gowork, json, jsonc, markdown, markdown-inline, python, rust, tsx, typescript, javascript, jsdoc, regex, yaml, gitcommit, cha0s-keybind-context); diagnostics, folding, multi-cursor, breadcrumbs, outline, bookmarks, project search. The agent reads PDF, OOXML, EPUB, ODT, RTF and archive listings (one `archive::member` level, 256 KiB cap; a scanned PDF reports `no text layer`).
- **Project** — multi-folder workspaces, full session restore (windows, tabs, docks, layout, bounds), project-local settings in `.cha0s/`, `AGENTS.md` rules per project, recent projects.
- **Terminal** — each console tab is its own PTY shared by operator and agent: same shell, same privileges, SSH sessions included. Operator keystrokes always win; Ctrl-C aborts the agent's command and the shell survives. Alternate-screen applications (MC, vim, less) are detected and reported.
- **Browser** — multi-tab, in the center lane. The address bar takes `http(s)`, bare `.onion`, bare `.i2p`, `ipfs://` and CIDs, and picks the network exit itself. Take control / Return control hands mouse and keyboard to the operator.
- **Search** — `search_clearnet` (parallel metasearch, lanes auto / general / tech / intel), `search_onion` (torch, onionland, ddg-onion, ahmia plus a baked seed catalog), `search_i2p` (legwork, ransack, identiguy, notbob plus an overlay addressbook), `fetch` (URL → markdown, SSRF refusal of loopback and private targets, wall fallback to the live pane).
- **Logs** — deterministic event log, ids 1001–1019, ring buffer, JSONL payloads, Prometheus metrics on loopback. The agent reads it with filters, pagination, and live waiting. Crash dumps and hang traces stay local.
- **Settings** — 13 pages (General, Appearance, Keymap, Editor, Languages & Tools, Search & Files, Window & Layout, Panels, Terminal, Version Control, AI, Network, Developer). Merge chain: defaults → language slots → user file → profile → project overlay. The user settings file is presented as **Operator**.

### The agent

- **26 tools** across files, terminal, browser, network, environment control, database, skills, plan, and `solo`. Before a request the backends are grouped into four model-facing faces — `terminal`, `documents`, `search`, `browser` — with `actions` kept for verified pane dispatch.
- **Turn discipline** — order → work → report. Every tool call returns a structured result with its own deadline; the turn ends with a visible report. Long conversations compact automatically; tool history is truncated with a recent-keep window.
- **Solo cycles** — the moon is a switch. Turn it on, send the instruction with the arrow, and the agent works until you turn it off. The composer stays locked for the duration; Stop aborts at once. Loop guard: three identical calls are allowed, the fourth closes that tool for the rest of the cycle. Transient provider failures back off 5 minutes, then 30, then end the cycle with one `Solo ended.` line.
- **Environment control** — `actions` dispatches a registered window action with verification, `state` returns a deterministic YAML snapshot of windows, panes, tabs and docks, `open_url` opens pages in windows and splits, `settings` reads and writes the settings store, `logs` reads the event log.
- **Knowledge base** — the `database` tool: `list`, `use`, `schema`, `declare`, `query`, `search`, `write`. The store is external and operator-configured; the model sees registry names, the raw DSN stays in settings. The Database menu in the agent footer shows health and document/chunk stats.
- **Skills** — `SKILL.md` playbooks loaded by name from project-local, machine-global, and built-in tiers; slash-commands on the panel surface; a skill added mid-session is visible immediately.
- **Plans** — `create_plan` posts a checklist the agent keeps executing; updating it keeps the turn running. The Build button sends a follow-up order and keeps the profile.
- **Privacy on the wire** — outbound cloud requests redact complete `CHA0S-1.…` license keys.

### Lock states and controls

`local_fs_lock`, default **on**, one switch in the agent footer:

| Lock state | Agent filesystem and shell |
|---|---|
| **On (default)** | File tools and terminal confined to the open project; OS-level sandbox (Seatbelt on macOS, bubblewrap on Linux) on local commands; `.git` protected; search tools unaffected |
| **Off** | The agent works in the operator's shell with the operator's rights — the whole machine and its remote sessions. By explicit operator decision |

Three separate controls: **Access** (right of the status bar — passphrase door on the loaded session, stored as an Argon2id hash, double-click to lock), the **lock** (agent footer, right of Database), and the **Database** menu (agent footer, right of thinking — gates the knowledge-base tool while the filesystem stays under the lock).

### Operating envelope

- The binary works offline: launch, keys, files, threads, and the local-model agent run with the network unplugged.
- Files, memory, databases, and browsing live on the operator's disk.
- Models are chosen and fetched by the operator's own runtime.
- Metrics bind to loopback; `CHA0S_METRICS=0` turns them off.
- When the operator enables an external model API or browsing, the task payload goes to that provider — operator-initiated, the only egress besides the shell the agent is told to use.

### Platform

| Item | State |
|---|---|
| macOS `.app` build and install (`make install`) | primary path |
| Linux build scripts and crates | in tree, next for acceptance |
| CLI (`cli`) shipped inside the app bundle | shipped |

## Models

Runs on any model. Ollama gives a fully offline, completely private circuit. Bring your own keys to Anthropic, OpenAI, Google, Mistral, DeepSeek, xAI, OpenRouter, LM Studio, llama.cpp, OpenCode, Vercel — or any OpenAI-compatible or Anthropic-compatible endpoint. Local is the most private option, and it is always available.

## Try it

- **3-day demo key, free**: talk to [@piniqai_bot](https://t.me/piniqai_bot) on Telegram → `/key`
- **Download**: `/download` in the bot, or [Releases](https://github.com/cha0skvlt/CHA0S_AOE/releases) (GPG-signed)
- **Buy**: $149 for a 1-year license (365 days). [piniq.ai/cha0s](https://piniq.ai/cha0s)

## License

- **Demo**: 3 days, free.
- **Paid**: $149 for a 1-year key (365 days). The key is signed offline and checked on your machine.
- **Expiry**: the app shows the remaining days. When the key expires, the app opens the Briefing gate until a new key is applied.
- **Renewal**: buy a new 1-year key.

## Doctrine

CHA0S is a tool. Code is working material: machined consumable shaped to an operation. The model is the AK-74 — simple, fires dirty, keeps firing. The rifle and the ammo are separate: the knowledge store is dated consumable, outside the lock; the license is annual.

With the lock off the operator's PTY is unwrapped: the trigger pulled, the command runs. Service restarts, system file edits, certificate renewals, schema changes. The model errs; the operator answers. With the lock on, the cage holds: project folder only, local terminal. Remote machines and the whole disk need the lock off. Unqualified use can end in lost hosts, broken services, leaked credentials, downtime. An agent's error is the operator's order executed by the machine.

The pair has exactly two names: **operator** and **agent**. The operator states the task, reviews, and edits by hand when needed; the agent operates tools and systems, retrieves and writes memory, and reports. Three columns: agent on the left, editor / terminal / search in the middle, project tree on the right.

## Documentation

| Doc | What's inside |
|---|---|
| [ARCHITECTURE.md](ARCHITECTURE.md) | How the system is built: crates, startup, tools, providers |
| [SECURITY.md](SECURITY.md) | PGP key, signatures, reporting vulnerabilities |
| [CONTRIBUTING.md](CONTRIBUTING.md) | What is in scope for this repository |

## Links

- **Site**: [piniq.ai](https://piniq.ai) · [piniq.ai/cha0s](https://piniq.ai/cha0s)
- **Demo bot**: [@piniqai_bot](https://t.me/piniqai_bot)
- **PGP**: `C981 2C7E 5860 44E2 3779  B828 72AC 40D1 A81F 144C` ([piniq.ai/pgp.asc](https://piniq.ai/pgp.asc))

---

*The operator pulls the trigger. The agent fires. The report states the target status. That is all.*
