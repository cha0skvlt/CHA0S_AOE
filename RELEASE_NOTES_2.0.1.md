Bug-fix release of CHA0S AOE — Agentic Operations Environment.

**Your machine. Your agents. Your rules.**

- Native binary, GPU-rendered Rust core, universal (x86_64 + arm64)
- 26 agent tools: files, terminal, browser, OSINT metasearch, environment control, knowledge base, skills, plan, solo cycles
- Agent memory (the Phylactery): external Postgres/pgvector, hybrid exact + semantic search
- Browser the agents drive: navigate, click, type, read live pages; clearnet / onion / I2P
- Runs on any model: Ollama fully offline, or bring your own keys (Anthropic, OpenAI, Google, Mistral, DeepSeek, xAI, OpenRouter, LM Studio, llama.cpp, OpenCode, Vercel, and OpenAI/Anthropic-compatible endpoints)
- Zero telemetry; metrics bind to loopback only
- Offline Ed25519 license keys — no key server, no HWID, no account

## Fixed in 2.0.1

- License terms stated consistently: paid keys are 1 year (365 days), demo 3 days; expiry opens the hard Briefing gate; no auto-renewal.
- Tool catalog corrected to the shipped 26 names: `database` and `wait` are in; `search_web`, `kb`, and `db` are retired names that resolve to `search_clearnet` and `database`.
- Loop guard: read-only calls bypass it; a repeated mutating call is skipped, not a turn kill. Lookup progress replaces the old read-guard.
- Cloud privacy: path aliasing removed; cloud models see real absolute paths. Complete `CHA0S-1.…` license keys are still redacted.
- Documentation aligned with the code.

## Download

- **macOS (universal)**: [CHA0S-AOE-2.0.1-macos.dmg](https://github.com/cha0skvlt/CHA0S_AOE/releases/download/v2.0.1/CHA0S-AOE-2.0.1-macos.dmg) — attached below
- Checksums: [checksums.txt](https://github.com/cha0skvlt/CHA0S_AOE/releases/download/v2.0.1/checksums.txt)
- GPG signatures: [dmg.sig](https://github.com/cha0skvlt/CHA0S_AOE/releases/download/v2.0.1/CHA0S-AOE-2.0.1-macos.dmg.sig), [checksums.txt.sig](https://github.com/cha0skvlt/CHA0S_AOE/releases/download/v2.0.1/checksums.txt.sig) — key `C981 2C7E 5860 44E2 3779  B828 72AC 40D1 A81F 144C`, verify per [SECURITY.md](https://github.com/cha0skvlt/CHA0S_AOE/blob/main/SECURITY.md)

## Try it

3-day demo key, free: talk to [@piniqai_bot](https://t.me/piniqai_bot) on Telegram → `/key`. Full license: **$149 for 1 year (365 days)** — [piniq.ai/cha0s](https://piniq.ai/cha0s).

Full changelog: [CHANGELOG.md](https://github.com/cha0skvlt/CHA0S_AOE/blob/main/CHANGELOG.md)
