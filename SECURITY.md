# Security

## Reporting a vulnerability

CHA0S AOE is an operational tool; its security is the operator's security. We treat reports seriously and fast.

1. Encrypt your report to the PGP key below.
2. Send it to `task@piniq.ai` with `[vuln]` in the subject.
3. You will get an acknowledgment within 72 hours and a fix timeline after triage.

Please include: the version (Briefing shows it), the platform, reproduction steps, and impact. We credit reporters in the changelog unless you prefer otherwise.

## PGP key

```
C981 2C7E 5860 44E2 3779  B828 72AC 40D1 A81F 144C
```

Public key: [piniq.ai/pgp.asc](https://piniq.ai/pgp.asc)

## Verifying release binaries

Every release binary is GPG-signed. Verify before running:

```sh
curl -sO https://piniq.ai/pgp.asc
gpg --import pgp.asc
curl -sO https://github.com/cha0skvlt/CHA0S_AOE/releases/download/vX.Y.Z/CHA0S-AOE-vX.Y.Z-macos.dmg
curl -sO https://github.com/cha0skvlt/CHA0S_AOE/releases/download/vX.Y.Z/CHA0S-AOE-vX.Y.Z-macos.dmg.sig
gpg --verify CHA0S-AOE-vX.Y.Z-macos.dmg.sig CHA0S-AOE-vX.Y.Z-macos.dmg
```

A good signature shows the fingerprint above. If verification fails, do not run the binary and tell us immediately.

## Scope notes

- The product performs **no action on its own**: every operation is initiated and directed by the operator. Reports about "the agent did X when asked to do X" are behavior, not vulnerabilities.
- The filesystem lock (`local_fs_lock`) is the sandbox switch. With the lock off, the agent works in the operator's shell with the operator's rights — by explicit operator decision. That is the design, not a hole.
- License verification is offline Ed25519 — no key server, no HWID, no network call. A tampered key opens a hard gate, nothing more.
