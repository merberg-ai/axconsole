# AXConsole

AXConsole is a multi-platform AX.25 packet-radio workstation built around a persistent Linux backend, `axconsoled`. The daemon owns radio access, packet monitoring, history, MHEARD intelligence, and connected-mode AX.25 sessions; user interfaces attach to the daemon instead of owning RF sessions themselves.

> **Status:** alpha software. The current public-source staging baseline preserves the proven protocol-generation-1 architecture while the project is being prepared for a first GitHub release.

## Architecture

```text
Linux Textual client ── Unix socket ──┐
                                     │
Windows Textual client ── TLS/TCP ───┼── axconsoled ── Linux AX.25 stack ── RF
                                     │
Android native client ─── TLS/TCP ───┘
```

Local clients use `/run/axconsole/axconsole.sock`. Optional remote access uses authenticated TLS TCP, normally port `7310`, with observer/operator roles enforced by the daemon.

## Source tree

- `linux/` — Linux backend, Linux Textual client, native AX.25 helpers, installer, CLI tools, and tests.
- `windows/` — Windows Textual remote client.
- `android/` — Native Kotlin/Jetpack Compose Android remote client.
- `docs/` — architecture, protocol, release, and project documentation.

## Current imported checkpoints

| Component | Version |
| --- | --- |
| Linux/backend | `0.6.3-alpha` |
| Windows client | `0.1.1-alpha` |
| Android client | `0.5.1-alpha5a` |
| Remote protocol | `1` |

A later `0.6.4-alpha` backend development patch is known to have existed for MHEARD/used-digipeater duplicate suppression, but that exact source artifact has not yet been recovered into this staging tree. It should be recovered or deliberately reimplemented and requalified before the first tagged release.

## Design rules worth preserving

- Connected RF sessions belong to `axconsoled`, not a UI.
- Local Unix-socket operation remains available even when remote TLS is disabled or fails to start.
- Remote authorization is enforced in the backend, not only in clients.
- LinPac-style `//COMMAND` text is RF data; only a single leading slash selects a local Textual-client command.
- The proven native Linux AX.25 helpers should be wrapped, not casually rewritten.
- A future Dire Wolf transport should use AGWPE for full connected-mode parity rather than introducing a new internal AX.25 Layer-2 engine.

## Development

Linux/backend:

```bash
cd linux
python -m venv .venv
. .venv/bin/activate
python -m pip install -U pip
python -m pip install -e . pytest
pytest -q
```

Windows client:

```powershell
cd windows
py -3.11 -m venv .venv
.\.venv\Scripts\python -m pip install -U pip
.\.venv\Scripts\python -m pip install -e . pytest
.\.venv\Scripts\python -m pytest -q
```

Android requirements and build commands are documented in `android/README.md`.

## Security

Do not expose the AXConsole TLS listener or a Dire Wolf AGWPE listener directly to the public Internet. LAN/VPN-restricted deployments are the intended model. Never commit server private keys, authentication tokens, packet-history databases, or session transcripts. See `SECURITY.md`.

## License

GPL-3.0-or-later. See `LICENSE`.
