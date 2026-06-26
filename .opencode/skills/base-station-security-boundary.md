# Base-Station Security Boundary

Treat these as untrusted or boundary-crossing inputs:

- Air-interface or core-network protocol messages: RRC, NGAP, S1AP, X2AP, F1AP, E1AP, GTP-C, GTP-U, SCTP, UDP, TCP.
- OAM, CLI, northbound APIs, remote config, provisioning, telemetry import, upgrade packages, plugin/package loading.
- IPC from lower-privilege processes, container boundaries, driver/user boundary, simulator/test harness input when compiled into production.

High-risk bug classes:

- Length-field misuse, ASN.1/PER/TLV parsing errors, integer overflow, signed/unsigned conversion, unchecked memcpy/memmove/string formatting, allocation-size mismatch.
- State-machine bypass, unauthenticated management action, downgrade or debug mode enablement, unsafe default credentials, weak crypto or certificate validation bypass.
- Log or telemetry exposure of IMSI/SUPI/SUCI, keys, tokens, credentials, session identifiers, subscriber data, or network topology.

Usually lower severity or drop:

- Code reachable only from unit tests, fuzz harnesses, offline tools, disabled debug builds, or local admin-only maintenance commands.
- Inputs already constrained by authenticated trusted provisioning and validated before this module boundary.
- Paths missing a concrete call chain from entrypoint to sink.
