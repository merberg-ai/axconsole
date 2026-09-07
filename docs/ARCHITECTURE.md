# Architecture

`axconsoled` is the persistent owner of radio-facing state. It owns packet monitoring, UNPROTO/UI transmission, SQLite history, MHEARD, connected-mode AX.25 sockets, connected-session scrollback/state, session logs/exports, the local Unix API, and optional remote TLS API.

The key consequence is that UI detach/restart does not intentionally drop live RF sessions. RF sessions do not survive an `axconsoled` restart because the operating-system AX.25 sockets belong to that daemon process.

## Current radio implementation

- UNPROTO/UI transmit: `AF_AX25 + SOCK_DGRAM`
- Connected mode: `AF_AX25 + SOCK_SEQPACKET`
- Monitoring: local `axlisten`
- Native helpers: `linux/native/axconsole_tx.c` and `linux/native/axconsole_conn.c`

## Planned transport direction

The proven Linux implementation should eventually sit behind a transport interface without changing RF behavior. A second full-function transport can then target Dire Wolf AGWPE TCP. Raw KISS may be useful later for monitor/UNPROTO-only use, but AXConsole should not grow its own connected-mode AX.25 Layer-2 engine merely to support KISS.
