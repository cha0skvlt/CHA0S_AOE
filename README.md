# CHA0S AOE — Agentic Operations Environment

**Your machine. Your agents. Your rules.**

A native Rust environment where agents work alongside you: your shell, your files, your data, your browser. One binary, GPU-rendered, zero telemetry. Runs on any model — local or by API.

> [!NOTE]
> **Closed-source product.** This repository is the product's public home: documentation, releases, signatures, and issues. Source code is not distributed. See [LICENSE-NOTICE.md](LICENSE-NOTICE.md).

---

## What it is

CHA0S AOE is a local-first **Agentic Operations Environment** for technical operators: infrastructure work, system administration, incident response, OSINT, authorized penetration testing, red-team engagements — first-class operations.

The operational model: **operator → objective → agent → tools + memory → live systems → result**.

The agent can write and modify code when an objective requires it, but software development is a capability of the instrument, not the product category.

## Capabilities

### The engine
A GPU-rendered Rust core. Ships as one native binary; agents run in-process with your editor, terminal, and browser. Startup is instant; the whole environment is a single application.

### Privacy
Everything stays on your machine. Files, memory, databases, and browsing live on your disk. Metrics bind to loopback — one environment variable silences them.

### Agent memory — the Phylactery
Each agent keeps persistent memory in an external Postgres/pgvector store: facts, lessons, operational knowledge — accumulated across sessions. Hybrid search, exact and semantic, retrieves it on demand. It survives restarts, model swaps, and machine migrations. Your database, your DSN, your data.

### Custom agents
As many agents as you need. Each carries its own profile: system prompt — personality, language, discipline; its own Phylactery DSN; its own tool allowlist; its own skills and playbooks. Switch between them per thread.

### Agents run the environment
The whole environment is the agent's control panel. Windows, panes, tabs, docks, settings, logs — the agent reads and drives them all as tools, in the same session you use. Turn on a solo cycle and the agent works on its own — starting from your instruction — until you turn it off. It reports as it goes; you stay the operator.

### Browser with OSINT
The agents drive the browser. Navigate, click, type, read live pages — the browser is a tool. OSINT search spans clearnet, onion, and I2P; Tor, i2pd, and Kubo run as local processes on demand. Research runs on your machine; you watch.

## Models

Runs on any model. Ollama gives a fully offline, completely private circuit. Bring your own keys to Anthropic, OpenAI, Google, Mistral, DeepSeek, xAI, OpenRouter, LM Studio, llama.cpp, OpenCode, Vercel — or any OpenAI-compatible or Anthropic-compatible endpoint. Local is the most private option, and it is always available.

## Try it

- **3-day demo key, free**: talk to [@piniqai_bot](https://t.me/piniqai_bot) on Telegram → `/key`
- **Download**: `/download` in the bot, or [Releases](releases) (GPG-signed)
- **Buy**: $149 one-time, major-version license (2.x forever). [piniq.ai/cha0s](https://piniq.ai/cha0s)

## Documentation

| Doc | What's inside |
|---|---|
| [docs/PRODUCT.md](docs/PRODUCT.md) | What the product is and does today |
| [docs/ARCHITECTURE.md](docs/ARCHITECTURE.md) | How the system is built: crates, startup, tools |
| [CHANGELOG.md](CHANGELOG.md) | Release notes |
| [ROADMAP.md](ROADMAP.md) | What's ahead |
| [SECURITY.md](SECURITY.md) | PGP key, signatures, reporting vulnerabilities |

## Links

- **Site**: [piniq.ai](https://piniq.ai) · [piniq.ai/cha0s](https://piniq.ai/cha0s)
- **Demo bot**: [@piniqai_bot](https://t.me/piniqai_bot)
- **PGP**: `C981 2C7E 5860 44E2 3779  B828 72AC 40D1 A81F 144C` ([piniq.ai/pgp.asc](https://piniq.ai/pgp.asc))

---

*The operator pulls the trigger. The agent fires. The report states the target status. That is all.*
