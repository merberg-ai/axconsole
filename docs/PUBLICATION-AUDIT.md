# Publication Audit

This staging tree was prepared from the following recovered source archives:

- Linux/backend `0.6.3-alpha`
- Windows `0.1.1-alpha`
- Android `0.5.1-alpha5a`

Cleanup performed without intentional product-behavior changes:

- removed `.pytest_cache`, Python bytecode caches, and the prebuilt Windows wheel
- removed release-only Android paste/build note
- changed public runtime/example callsign defaults to `N0CALL`
- changed example TLS hostname to `packet-host.local`
- changed example remote-operator label to a generic value
- retained Android application ID/package namespace `net.kj6ywd.axconsoleandroid` to preserve upgrade identity
- aligned the Linux Textual dependency range with the known Windows Textual compatibility band (`>=8.2,<9`)
- added root ignore rules for credentials, runtime databases/logs, build outputs, and IDE artifacts
- added root README, contribution, security, architecture, and protocol documentation

## Known source-lineage gap

A Linux/backend `0.6.4-alpha` development build was made after the recovered `0.6.3-alpha` archive to suppress duplicate MHEARD counting associated with used-digipeater copies. The exact `0.6.4-alpha` source archive was not found in the available uploaded-file library during this audit. The first GitHub tag should not claim that patch until it is recovered or cleanly reimplemented and qualified from this source baseline.
