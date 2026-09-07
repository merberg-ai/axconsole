# AXConsole Remote Protocol

The current protocol generation is **1**. Remote clients use newline-delimited JSON over authenticated TLS.

Authentication occurs before normal commands. Roles are `observer` and `operator`, with authorization enforced by `axconsoled`.

Known command names at the imported checkpoint include:

```text
ping
send
history
search
resume
mheard
mheard_clear
conn_create
conn_send
conn_disconnect
conn_reconnect
conn_export
conn_close
conn_list
```

Resume/replay uses persistent packet-history IDs and per-session sequence numbers so reconnecting clients can request only missed data.

Protocol changes should remain backward-compatible within generation 1 or deliberately introduce and document a new generation.
