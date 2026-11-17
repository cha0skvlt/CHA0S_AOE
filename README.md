# CHA0S AOE

**Agentic Operations Environment** — a native desktop environment where AI agents work on real systems.

[![Version](https://img.shields.io/badge/version-2.0.1-blue?style=flat-square)](https://github.com/cha0skvlt/CHA0S_AOE/releases)
[![License](https://img.shields.io/badge/license-EULA-orange?style=flat-square)](LICENSE-NOTICE.md)
![macOS](https://img.shields.io/badge/macOS-primary-000000?style=flat-square&logo=apple&logoColor=white)
![Rust](https://img.shields.io/badge/Rust-2024-000000?style=flat-square&logo=rust&logoColor=white)

<!-- Screenshots go here. Drop docs/shot-*.png into the repo and uncomment.
![Workspace](docs/shot-workspace.png)
![OSINT](docs/shot-osint.png)
-->

CHA0S is one application: an editor, a terminal, a browser, and a memory store, with agents running inside it. The agent is not a chat sidebar — it drives the same windows, panes and shells you do, and it can be handed a task and left to work.

It is built for operators: infrastructure, system administration, incident response, OSINT, authorized security work. Writing code is one of the things it does, not the thing it is.

## The model

```
operator → objective → agent → tools + memory → live systems → result
```

The operator states the task and reviews the result. The agent operates tools and systems, reads and writes memory, and reports. Two names, nothing else.

## Inside

**Five lanes.** Every window has one centre lane at a time: Editor, Browser, Log, Search, Console. The agent switches them as tools.

**Terminal.** Each console tab is a real PTY shared by you and the agent — the same shell, the same privileges, SSH sessions included. Your keystrokes always win; Ctrl-C aborts the agent's command and the shell survives.

**Browser.** Multi-tab, in the centre lane. The address bar takes `http(s)`, bare `.onion`, bare `.i2p`, `ipfs://` and CIDs, and picks the network exit itself. Tor, i2pd and Kubo run as local processes on demand. Take control hands the mouse and keyboard back to you.

**Memory.** Every agent keeps a persistent store in Postgres with pgvector: facts, lessons, operational knowledge, accumulated across sessions. Exact and semantic search over it. It survives restarts, model swaps and machine moves. Your database, your DSN.

**Agents.** As many as you need. Each has its own profile — system prompt, memory DSN, tool allowlist. Skills are `SKILL.md` playbooks in three tiers: project, machine, built-in.

**Solo.** Turn it on and the agent works on its own from your instruction until you turn it off. The composer locks, Stop aborts at once, and a loop guard closes a tool that keeps repeating itself.

**The lock.** One switch. On: file tools and terminal confined to the open project, OS-level sandbox on local commands. Off: the agent works in your shell with your rights — the whole machine and its remote sessions. Your call, your risk.

**26 tools.** `read_file` `write_file` `edit_file` `copy_path` `move_path` `delete_path` `create_directory` `list_directory` `find_path` `grep` `terminal` `wait` `browser` `fetch` `search_clearnet` `search_onion` `search_i2p` `state` `actions` `settings` `logs` `open_url` `database` `skill` `create_plan` `solo`.

## What it is not

- **Not a cloud service.** Files, memory, databases and browsing stay on your disk. The binary runs offline: launch, keys, files, threads and the local-model agent need no network.
- **Not a code assistant with extra buttons.** No extension marketplace, no language-server zoo, no debugger. The editor is a working surface, not the product.
- **Not autonomous.** Nothing happens that you did not ask for. With the lock off, an agent's error is your order executed by the machine.

## Models

Any model. Ollama gives a fully offline circuit; your own keys cover Anthropic, OpenAI, Google, Mistral, DeepSeek, xAI, OpenRouter, LM Studio, llama.cpp, or any OpenAI- or Anthropic-compatible endpoint.

## Open components

The shell is closed source. The tools around it are not:

| Repository | What it is |
| --- | --- |
| [phylactery-mcp](https://github.com/cha0skvlt/phylactery-mcp) | the memory server: four circuits, typed graph, pgvector |
| [downloader-mcp](https://github.com/cha0skvlt/downloader-mcp) | media engine: fetch, trim, convert, join, normalize |
| [avatar-media-mcp](https://github.com/cha0skvlt/avatar-media-mcp) | avatar and media pipeline |
| [single-vm-web-platform](https://github.com/cha0skvlt/single-vm-web-platform) | single-VM web deployment |
| [single-vm-mail-platform](https://github.com/cha0skvlt/single-vm-mail-platform) | single-VM mail deployment |

## Get it

- **Demo, 3 days, free** — [@piniqai_bot](https://t.me/piniqai_bot), `/key`
- **Download** — `/download` in the bot, or [Releases](https://github.com/cha0skvlt/CHA0S_AOE/releases), GPG-signed
- **Buy** — $149 for a 365-day key, [piniq.ai/cha0s](https://piniq.ai/cha0s)

The key is signed offline and checked on your machine. No key server, no hardware ID, no network call. Expiry opens the Briefing gate until a new key is applied.

## Verify the binary

```sh
curl -sO https://piniq.ai/pgp.asc && gpg --import pgp.asc
gpg --verify CHA0S-AOE-vX.Y.Z-macos.dmg.sig CHA0S-AOE-vX.Y.Z-macos.dmg
```

Fingerprint: `C981 2C7E 5860 44E2 3779  B828 72AC 40D1 A81F 144C`

## Docs

[SECURITY.md](SECURITY.md) · [LICENSE-NOTICE.md](LICENSE-NOTICE.md)

Built on the GPUI engine, with code derived from Zed under AGPL-3.0. See [LICENSE-NOTICE.md](LICENSE-NOTICE.md).
