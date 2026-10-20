# License Notice

## The product

**CHA0S AOE** is a closed-source product by piniq.ai. The product is distributed as a signed binary under the terms of the End User License Agreement delivered with it (and mirrored at [piniq.ai](https://piniq.ai)). The EULA grants a right to use the delivered binary. It is not a source license.

Paid access keys are issued for **1 year (365 days)**; the demo key is 3 days. A key is checked offline and expires at its signed `expires_utc`; expiry opens the hard Briefing gate until a new key is applied. There is no auto-renewal and no key server.

This repository contains **no source code**. It is the product's public home: documentation, release binaries, GPG signatures, and the issue tracker.

## Engine foundation and AGPL-3.0

CHA0S AOE is built on the **GPUI engine and includes code derived from Zed (AGPL-3.0)**. The Zed-derived part is the engine and editor foundation: `gpui*`, `editor`, `language*`, `text`, `rope`, `sum_tree`, `workspace`, `theme`, `client`, `proto`, and related components. Everything built on top of it — the agent runtime, OSINT metasearch, live browser, knowledge base, observability, sandbox, and the app shell — is original CHA0S code by piniq.ai.

The EULA covers the delivered product, not the code base: it grants a right to use the sold binary and says nothing about, and is not a license for, the Zed-derived foundation. The foundation keeps its upstream AGPL-3.0 terms. This notice documents where it lives; it does not relicense it.

AGPL-3.0 §13 (network interaction) applies to users interacting with the covered code over a network. CHA0S AOE is a local application: the binary runs on the operator's machine, and no covered code is offered as a network service.

## Vendored upstream components

The build includes vendored upstream trees (terminal, rendering, event-loop, HTTP, and grammar components). Their original open-source licenses (MIT / Apache-2.0, per each tree's own `LICENSE*` files) continue to apply to them. They are consumed as workspace excludes or patched crates.io entries and are not part of the CHA0S first-party code. The per-tree inventory stays in the private tree.

## Trademarks

"CHA0S", "CHA0S AOE", "Agentic Operations Environment", and the CHA0S mark are product names of piniq.ai. Third-party names (Zed, Tor, Ollama, and others) belong to their owners and are used here only to describe compatibility and provenance.

## Questions

Licensing questions: `task@piniq.ai` (PGP: see [SECURITY.md](SECURITY.md)).
