# Security Policy

AXConsole is alpha software and should be deployed on trusted LAN/VPN networks.

## Sensitive material

Never commit or attach real:

- observer/operator tokens
- TLS private keys
- packet-history databases
- connected-session transcripts
- exported client credential bundles
- Android signing material

The server certificate may be distributed to clients; the server private key must remain on the backend host.

## Network exposure

The optional AXConsole TLS listener is intended for LAN/VPN access. Dire Wolf AGWPE, if added as a transport, should likewise remain restricted to a trusted network. Do not expose either listener directly to the public Internet.

## Reporting a vulnerability

Please use GitHub's private security-advisory mechanism for vulnerabilities involving authentication, authorization, TLS, credential handling, or remote command execution. Avoid opening a public issue with exploit details or live credentials.
