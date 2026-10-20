# Changelog

All notable changes to CHA0S AOE are documented here. Dates are UTC. Each release tag is GPG-signed; signatures live next to the binaries in [Releases](releases).

## 2.0.0 — 2026-10-13

First public release of CHA0S AOE — Agentic Operations Environment.

### The environment
- Native binary with a GPU-rendered Rust core; agents run in-process with the editor, terminal, and browser.
- Five exclusive center lanes: Editor / Browser / Log / Search / Console. Multi-tab live browser in the middle lane.
- Full session restore: windows, tabs, docks, layout.
- 22 built-in languages via tree-sitter; buffer diagnostics, folding, multi-cursor, outline, bookmarks.

### The agent
- 26 catalog tools: files, terminal, browser, network search, environment control, knowledge base, skills, plan, solo.
- Operator session PTY: each console tab is a live PTY shared by operator and agent — same shell, same environment, SSH sessions included.
- Solo cycles: turn the moon on, send the instruction — the agent works on its own until you turn it off.
- Custom agents: any number of profiles, each with its own system prompt, Phylactery DSN, tool allowlist, and skills.
- Agent memory (the Phylactery): external Postgres/pgvector store with hybrid exact + semantic search; survives restarts and migrations.
- Cloud privacy: local filesystem paths are rewritten to generic aliases in outbound model requests.

### OSINT
- Metasearch across clearnet (lanes: general / technical / intel), onion (Tor), and I2P (i2pd); IPFS via Kubo.
- Built-in browser the agent drives as a tool: navigate, click, type, read live pages with element references.
- `fetch`: URL → markdown with SSRF refusal of loopback/private targets and wall-fallback to the live pane.
- Tor, i2pd, and Kubo pulled as local processes on demand; no listeners → refusal, never a silent direct leak.

### Models
- Any model: Ollama (fully offline), Anthropic, OpenAI, Google, Mistral, DeepSeek, xAI, OpenRouter, LM Studio, llama.cpp, OpenCode, Vercel — plus OpenAI-compatible and Anthropic-compatible endpoints.

### Privacy
- Zero telemetry. No analytics, no crash-report send flow, no update checks, no vendor cloud.
- Metrics bind to loopback only; `CHA0S_METRICS=0` silences them entirely.
- Offline Ed25519 license keys — no key server, no HWID, no account. Paid keys are 1-year (365 days); the demo is 3 days. Expiry opens the hard Briefing gate; no auto-renewal.

### Access
- Passphrase door (Argon2id) on the loaded session; fast interface lock.
- Filesystem lock: one switch — project-only sandbox (Seatbelt/bubblewrap) or the operator's full machine and remote sessions.
