# PRODUCT.md — what CHA0S is

> Product version: **2.0.0** · verified against the code: **2026-10-20 UTC**
> Renewal rule: on any doc change, re-verify claims against the code and update both fields.

The product definition: what CHA0S is, its goals, and how each goal is implemented right now. Stated declaratively. The code is the source of truth for behavior; when the product must change, this file is updated first, then the code. This file is the neutral, dual-use description of the product for any audience; the operational doctrine lives in the last section, unchanged in substance.

Companion documents (do not collapse roles):

| File | Role |
| --- | --- |
| [PRODUCT.md](PRODUCT.md) | This file — product goals and their current implementation |
| [ARCHITECTURE.md](ARCHITECTURE.md) | Tree map: what is on disk |

Companion documents in the product repository: [README.md](../README.md) (product home), [CHANGELOG.md](../CHANGELOG.md), [ROADMAP.md](../ROADMAP.md), [SECURITY.md](../SECURITY.md), [LICENSE-NOTICE.md](../LICENSE-NOTICE.md).

Markers on this file: state of **the product now** (goal → current implementation).

- ✅ working and verified
- ⚠️ in the tree; unconfirmed or not yet accepted — needs attention
- ❌ not in the product

CHA0S is a local-first **Agentic Operations Environment**: one technical operator defines an objective, an agent combines operator-controlled memory with tools and context, acts on live systems, and reports the result. It performs no action on its own: every operation is initiated, configured, and directed by the operator. Infrastructure work, system administration, incident response, OSINT, authorized penetration testing, and red-team engagements are first-class operations. The agent can write and modify code when an objective requires it, but software development is a capability of the instrument, not the product category.

The operational model is: **operator → objective → agent → tools + memory → live systems → result/report**. Dual use is inherent: the same shell, file access, browser, networking, and knowledge store serve infrastructure, investigative, research, and security work.

---

## 1. Product identity

| Field | Value |
| --- | --- |
| Product | CHA0S — Agentic Operations Environment by piniq.ai |
| Version | `2.0.0` (`crates/cha0s` package version) |
| Delivery | per the EULA delivered with the product |
| License term | Paid key: **1 year (365 days)**; demo: 3 days. Offline Ed25519, no key server, no HWID. Expiry opens the hard Briefing gate until a new key is applied; no auto-renewal. |
| Platforms | macOS ✅ primary; Linux ✅ in tree; Windows ❌ frozen |
| macOS app | `CHA0S AOE.app` (`CHA0S AOE Dev.app` on dev). Bundle id `ai.piniq.CHA0S`. URL scheme `cha0s`. Runtime data/config paths use `CHA0S` / `cha0s`. |

## 2. What the product is

CHA0S is an isolated, multi-purpose Agentic Operations Environment. ✅ One person — the operator — sits at the machine; one agent works alongside them. The operator creates and configures the agent through profiles, system prompts, skills, tool policy, and an external Postgres/pgvector memory. The agent uses the full operations surface: editor, files, terminal, browser, network search, settings, logs, and knowledge store. ✅ Operator-verified: the agent carries an objective from order to report inside the same live session the operator uses.

| Claim | State |
| --- | --- |
| One operator, one agent; no foreign CLI agents in the panel | ✅ |
| The agent drives the whole environment (actions, settings, logs) as tools | ✅ |
| Operator sign-in by passphrase, optional; fast interface lock | ✅ |
| No built-in content filtering or corporate prompt policy | ✅ |
| Configurable agents with a custom system prompt | ✅ |
| Direct Postgres/pgvector connection for the agent's knowledge base | ✅ |
| No outbound telemetry until the operator enables external APIs | ✅ |
| Logs readable by the agent in real time | ✅ |
| Shared browser for operator and agent: web, onion, I2P, IPFS in one pane | ✅ |
| Metasearch across networks as an agent tool | ✅ |

## 3. Operations surfaces

The surfaces below are instruments available during an operation. None of them defines the product category by itself.

### 3.1 Editor

- ✅ Open a project, edit files, browse the tree.
- ✅ Syntax highlighting and structure parsing via tree-sitter; 22 built-in languages.
- ✅ Buffer diagnostics, folding, multi-cursor, breadcrumbs, outline, bookmarks.
- ❌ No language server, no snippets, no onboarding nanny, no Jupyter, no command-recipe palette, no inline edit predictions.
- ✅ Code is a working material: the operator or agent can inspect, generate, patch, and execute it as part of an operation. CHA0S is an AOE. It does not compete on LSP, autocomplete, or debugger depth.
- ✅ The agent reads PDF, OOXML (docx, xlsx, pptx), EPUB, ODT, RTF, and archive listings (zip, jar, tar, and tar.gz / tar.xz / tar.bz2). A member is `archive::path`, one level, in memory. A scanned PDF with no text layer is an error (`no text layer`); this wave does not rasterize it. The editor and project search still refuse these files as binary. The UI preview is PDF only.

### 3.2 Project

- ✅ Multi-folder workspaces, one project per OS window by default.
- ✅ Full session restore: windows, tabs, docks, layout.
- ✅ Project-local settings in `.cha0s/`; rules files (`AGENTS.md` and peers) picked up per project.
- ✅ Recent projects list with management.

### 3.3 Terminal

- ✅ Operator console: full center lane plus a bottom-dock peek.
- ✅ Each center console tab is its own PTY, shared by the operator and the agent on that tab: the operator's environment, privileges, and remote session (SSH included). Several tabs can run at once. One tab is one command. Empty `tab` is the active console, then the dock. A named `item:<id>` does not fall through to the dock. `wait_id` stays `session`.
- ✅ Operator keystrokes on that tab always win: Ctrl-C aborts the agent's command; the shell survives.
- ⚠️ TUI applications (MC, vim, less): the agent does not inject into alternate-screen apps; it reports and waits instead.

### 3.4 Browser

- ✅ Thin in-app browser in the center lane; multi-tab; address bar accepts `http(s)`, bare `.onion`, bare `.i2p`, `ipfs://` and CIDs; the correct network exit is chosen automatically.
- ✅ Tor, i2pd, and Kubo are pulled as local child processes on demand; no listeners → refusal, never a silent direct leak.
- ✅ The agent drives the page as a tool: navigate, read a snapshot with element references, click, type, scroll. ✅ Operator-verified.
- ⚠️ Operator-verified on macOS; Linux/Windows OSR code is in tree but not accepted (and Windows is frozen).

### 3.5 Network search (as agent tools)

- ✅ `search_clearnet`: parallel metasearch over multiple indexes with lanes (general / technical / intel); wall-fallback through the live pane.
- ✅ `search_onion`: onion indexes through Tor, plus a baked seed catalog.
- ✅ `search_i2p`: I2P indexes through i2pd, plus an overlay addressbook engine.
- ✅ `fetch`: URL → markdown with redirect handling, SSRF refusal of loopback/private targets, and page-wall fallback to the live pane.
- ⚠️ `search_web` is a retired catalog name: it is not one of the 26 tools and resolves to `search_clearnet`; the old single-provider path refuses to run unless `agent.browsing` is explicitly enabled.

### 3.6 Logs and observability

- ✅ Deterministic event log: ids 1001–1019, ring buffer, JSONL payloads, local Prometheus metrics endpoint on loopback only.
- ✅ The agent reads the log as a tool, with filters and live waiting.
- ✅ Crash dumps and hang traces are local; no crash-reporting UI.

### 3.7 Settings

- ✅ 13 settings pages (`settings_data`: General, Appearance, Keymap, Editor, Languages & Tools, Search & Files, Window & Layout, Panels, Terminal, Version Control, AI, Network, Developer); the user settings file is presented as **Operator**.
- ✅ Local merge chain: defaults → language slots → user file → profile → project overlay.
- ✅ Custom agent profiles with inline or file-based system prompts; per-profile tool allowlists. The profile card edits the name, the system prompt (inline text or a file path), and the knowledge-base DSN (`kb_url`). The built-in Agent profile changes only through Fork.

## 4. The agent

### 4.1 Runtime

- ✅ Default brain: a local model via Ollama on the same machine. No internet required. Cloud model providers are operator-enabled options, not the default path.
- ✅ 26 catalog tools (`ALL_TOOL_NAMES`, smoke-asserted): files, terminal, browser, network, environment control, knowledge base, skills, plan, and `solo`. `add_default_tools` plants 25 of those names plus the internal `sandboxed_terminal` variant; `skill` is planted by `NativeAgent` with a body resolver. The model-facing set folds `terminal` + `console_pane` into one face named `terminal`; the retired names `search_web`, `kb`, and `db` resolve to `search_clearnet` and `database`.
- ✅ Solo cycles: the moon is a switch. The operator turns it on, then sends a message with the arrow. That message is the instruction, and the turn says the solo cycle is on. The `solo` tool is offered only while a cycle is running. The moon stays blue while the switch is on. Turning it off clears the moon immediately. The current reply or tool finishes, the agent writes the closing report, then the cycle ends. The Stop button still aborts. A tool-free round continues the segment until the moon is off, the agent calls `declare_done`, or app quit. The loop guard does not end the cycle. Three identical calls are allowed; the fourth closes that tool for the rest of the cycle, shows the refusal once, and drops it from the next request. Other tools stay. Three error results close that tool the same way. A console read of one tab is the key `terminal:read`. Poll fields and the `cmd` / `action` aliases do not open another read of that screen. A different tab is a different screen. The second read of a tab does not run and does not close `terminal`. A read that errors does not hold the screen. One card shows the refusal. A successful `op=run`, `op=kill`, or `op=new_tab` on that tab allows one later read of it. Other calls do not. The first batch that is only that refusal continues the cycle once. The next such batch stops the turn and leaves the cycle running. A hard provider failure stays in the running cycle. After the short provider retries, a transient failure waits 5 minutes, then 30 minutes, and the third ends the cycle as `Solo ended (provider)` with one `Solo ended.` line. The moon says `Solo retrying` during a wait. An error the short retries will not try (missing key, payment, 401/403, prompt too large) ends on the first. A model refusal still pauses and does not cut the thread. The composer stays locked until the cycle ends. There is no time, tool, or token limit. The button does not create a thread and has no mode or budget menu. Class-2 actions queue for approval instead of running. The `db` tool still runs: it is read-only, and a queued query would have no one to approve it.
- ✅ Every tool call returns a structured result (`ToolOutcome`); deadlines per call; retry policy only for idempotent reads.
- ✅ Turn discipline: an order → work → report cycle. The turn ends with a visible report; the agent is never nagged to "keep working".
- ✅ Long conversations are compacted automatically; tool-result history is truncated with a recent-keep window.
- ✅ Privacy on the wire: outbound cloud requests redact complete `CHA0S-1.…` license keys; local filesystem paths are sent as real absolute paths (path aliasing was removed by operator decision).

### 4.2 The environment as the agent's control panel

| Tool | What it gives the agent |
| --- | --- |
| `actions` | dispatch a registered window action by name, in a chosen window/pane, with verification |
| `state` | deterministic YAML snapshot of windows, panes, tabs, docks |
| `open_url` | catalog half folded into `browser`; opens URLs in windows/splits, including new windows |
| `settings` | read/list/write settings through the settings store |
| `logs` | read the event log: tabs, filters, pagination, live wait |

### 4.3 Knowledge base

- ✅ The agent talks to a Postgres/pgvector store as a tool (`kb`): hybrid ask, full-text search, document get/list/write/delete, reindex, stats. `kb databases` lists the registry as name and `host:port/db`. `kb use` switches the active database for the next turn when the profile has no `kb_url`. A profile `kb_url` wins over the registry; `kb use` then says so and does not write the registry. The model never sees a full DSN.
- ✅ The store is external and operator-configured; nothing is embedded in the binary.
- ✅ A separate `db` tool reads any Postgres database whose registry entry carries a schema declaration: table descriptions, a read-only `SELECT`, and cosine search when an embedding column is declared. Writes stay closed. The `kb` corpus (documents and chunks) is a different contour.
- ✅ Database menu in the agent panel footer, to the right of the thinking control. The label is `Database` when the `kb` tool is off or no database is selected, and the database name only when the tool is on and one is selected. The pyramid is blue only in that same case. The menu lists named databases with health and document/chunk stats, marks a declared schema, adds a database, and switches already-open threads on the next turn. The status bar has no database button. Failed connections retry, DSNs support TLS, and model-facing errors do not expose DSNs.
- ✅ Live Postgres acceptance (`make kb`) passes against the configured store.

### 4.4 Skills

- ✅ Skills are playbooks (`SKILL.md`) the agent loads by name; project-local, machine-global, and built-in tiers.
- ✅ Project-local skills load only from trusted worktrees.
- ✅ Slash-commands on the panel surface; new skills added mid-session are visible to the agent immediately.

### 4.5 Plans

- ✅ `create_plan` posts a checklist the agent keeps executing. Updating the plan does not pause the turn. The Build button sends a follow-up order and does not change the agent's profile.

## 5. Safety posture: the lock

One switch in the agent footer, to the right of Database (`local_fs_lock`, default **on**) — not a second shell, not a nanny:

| Lock state | Agent filesystem & shell |
| --- | --- |
| **On (default)** | File tools and terminal confined to the open project; OS-level sandbox wrap (Seatbelt/bubblewrap) on local commands; `.git` protected; remote/PTY access refused; search tools unaffected |
| **Off** | No cage: the agent works in the operator's shell with the operator's rights — the whole machine and its remote sessions. By explicit operator decision |

- ✅ `sandboxing` is engine-internal; the footer lock is the only operator switch.
- ✅ Three separate controls, never mixed: **Access** (right of the status bar — a passphrase door on the loaded session, double-click to lock; the passphrase is stored as a salted hash), the **lock** (agent footer, right of Database — the sandbox switch above), and the **Database** menu (agent footer, right of thinking — the agent's knowledge-base switch; it gates a tool, not the filesystem).

## 6. Offline and quietness

- ✅ The binary does not phone home: no telemetry, no update checks, no vendor cloud, no store, no anonymous statistics. Startup opens no vendor channel.
- ✅ Launch, keys, files, threads, and the local-model agent need no internet.
- ✅ Models are never downloaded by the product; local data never syncs.
- ✅ Crash reports stay local.
- ✅ Metrics bind to loopback only; a single env switch (`CHA0S_METRICS=0`) turns them off.
- ⚠️ When the operator enables an external model API or browsing, task payload leaves for that provider — this is operator-initiated, the only egress line besides the shell the agent is told to use.

## 7. What the product does not have

- ❌ Vendor cloud account, remote disable, key server, or machine binding (HWID). A signed key is checked locally.
- ❌ Perpetual license. Paid keys are 1-year (365 days); expiry opens the hard Briefing gate until a new key is applied.
- ❌ Built-in vendor knowledge corpus, model downloads, content feeds.
- ❌ Crash-report "send" flow, extension marketplace, auto-update.
- ❌ Multi-agent collaboration, foreign CLI agents in the panel.
- ❌ Language servers, DAP/debuggers, snippets, Jupyter, task palettes, onboarding nannies.
- ❌ Watermarks, canary tokens, or build identifiers that tie a copy back to a sale.
- ⚠️ A packaged folder-based knowledge slot: the knowledge path in the product is the Postgres tool above; a folder-markdown slot is not shipped.

## 8. Doctrine: the Kalashnikov principle

CHA0S is a tool, not a textbook and not a temple. Code is not the destination: it is machined consumable shaped to an operation. The product is not an end in itself: there are no decisions made "because the industry does it", "because it is elegant", or "because of social norms". If it can be simple — it is built simple. Complexity that does not serve the goal does not exist.

The model is the AK-74: simple, fires dirty, keeps firing. Not a Swiss watch, not a showroom piece.

The rifle and the ammo are separate. CHA0S fires without a magazine: the knowledge store is dated consumable, not part of the lock; the license is annual and does not auto-renew.

The operator pulls the trigger. The agent fires. The report states the target status. That is all.

### At the operator's own risk

CHA0S is a tool for experienced technical operators. Not for students, not for casual browsing of AI features, not for someone who cannot tell production from staging.

With the lock off there is no sandbox on the trigger: the operator's PTY is not wrapped. The trigger pulled — the command runs: service restarts, system file edits, certificate renewals, schema changes. The model errs. The operator answers.

With the lock on, the cage holds: project folder only, local terminal, no `/tmp`, no remote sessions. Unlock when the agent needs the whole disk or remote machines.

Unqualified use can end in lost hosts, broken services, leaked credentials, downtime — especially on production systems. Use at your own risk. An agent's error is not a product defect and not the vendor's fault: it is the operator's order executed by the machine.

### The agent is a working instrument

Not an assistant, not a nanny, not a moral committee, not a tutor.

It thinks fast, terse, and operationally: order, objective, context gathering, execution, report. It does not lecture the operator, does not explain unasked, does not rule on propriety, does not deliberate on anything but the task. Consequences belong to the operator.

The pair has exactly two names: **operator** and **agent**. Not "user", not "assistant", not the industry's neutral office language. In prompts, reports, and on screen — operator. Full stop.

Brevity and restraint are enforced at the level of the system prompt and tool design, not by asking politely. Without that, the agent degrades into the industry's default assistant — and the product dies in politeness. ✅ The operational prompt is live; the settings tab reads **Operator**; the system prompt calls the human **operator**.

### How one works with it

- ✅ The operator states the task (including via skill slash-commands), reviews, and edits files by hand when needed.
- ✅ The agent is the primary actor: it operates tools and systems, retrieves and writes memory, and reports results. It writes code when code is the required instrument. Live edits are streamed, not shadow-tree.
- ✅ Three columns: agent on the left, editor / terminal / search in the middle, project tree on the right.
- ✅ One agent, one full tool catalog; plan is a tool; the lock is the only safety switch.
- ✅ No collaboration surfaces: no sharing, no co-presence, no second agent.

## 9. Platform and build status

| Item | State |
| --- | --- |
| macOS `.app` build/install (`make install`) | ✅ primary path |
| Linux build scripts | ✅ in tree |
| Windows build | ❌ frozen; not supported, not a target |
| CLI (`cli`) shipped inside the app bundle | ✅ |

Model backends and provider routing: [ARCHITECTURE.md](ARCHITECTURE.md) §9. Sold-product terms: the EULA delivered with the product.
