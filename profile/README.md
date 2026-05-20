# GoodNet

[![Live demo](https://img.shields.io/badge/live%20demo-goodnet--io.github.io-cba6f7?style=for-the-badge&logo=githubpages&logoColor=white)](https://goodnet-io.github.io/)

A networking integrator kernel — composer pattern, multi-path
strategies, peer-key addressing, NAT traversal, real SSH replacement.
The kernel knows about logical connections, typed messages, public-key
addresses, and registered handlers. Every transport, every cipher,
every wire format lives in a plugin loaded through a dynamic / static /
remote runtime over a stable C ABI.

## Repos

### Core

- **[goodnet](https://github.com/GoodNet-io/goodnet)** — kernel, SDK,
  bundled plugin shims.
- **[goodnetd](https://github.com/GoodNet-io/goodnetd)** —
  operator-facing daemon + multicall CLI (`run`, `version`,
  `config validate`, `plugin hash`, `manifest gen`, `identity
  gen|show|import-hsm`, `doctor`, `quickstart`).
- **[gssh](https://github.com/GoodNet-io/gssh)** — native SSH-2.0
  server + client. Host identity is the GoodNet device pubkey; vanilla
  openssh clients connect; two `gssh` peers also negotiate a custom
  `gn.handler-ext@goodnet.io` subsystem channel for file transfer +
  port forwarding.

### Plugin family — links (transport carriers)

- [link-tcp](https://github.com/GoodNet-io/link-tcp) ·
  [link-udp](https://github.com/GoodNet-io/link-udp) ·
  [link-tls](https://github.com/GoodNet-io/link-tls) ·
  [link-ws](https://github.com/GoodNet-io/link-ws) ·
  [link-ipc](https://github.com/GoodNet-io/link-ipc) —
  single-protocol carriers.
- [link-ice](https://github.com/GoodNet-io/link-ice) — NAT traversal
  (RFC 8445 + STUN + TURN + Trickle ICE + mDNS + auto-restart on
  consent loss).
- [link-quic](https://github.com/GoodNet-io/link-quic) — QUIC over
  UDP/ICE (OpenSSL 3.6 native QUIC, composer pattern).

### Plugin family — security

- [security-noise](https://github.com/GoodNet-io/security-noise) —
  Noise XX handshake provider on libsodium primitives.
- [security-null](https://github.com/GoodNet-io/security-null) —
  loopback / IntraNode pass-through.
- [security-pkcs11](https://github.com/GoodNet-io/security-pkcs11) —
  hardware-backed signing via YubiKey / SoftHSM / enterprise HSM
  (`gn.identity.pkcs11` + `gn.security.pkcs11` dual-expose).

### Plugin family — handlers

- [handler-store](https://github.com/GoodNet-io/handler-store) —
  distributed key-value store (Memory + SQLite backends, first-writer-wins ACL).
- [handler-dns](https://github.com/GoodNet-io/handler-dns) — DNS
  over GoodNet (typed RR storage on `gn.store` + three-tier resolver
  with c-ares upstream).
- [handler-heartbeat](https://github.com/GoodNet-io/handler-heartbeat) —
  peer liveness + RTT measurement; feeds the strategy chain.
- [handler-ssh-modern](https://github.com/GoodNet-io/handler-ssh-modern) —
  native remote-shell handler (`SHELL_*` envelopes, peer-pubkey ACL,
  no openssh wire).
- [handler-web-api-proxy](https://github.com/GoodNet-io/handler-web-api-proxy) —
  browser-as-thin-client WebSocket gateway (JSON-RPC over gnet
  envelopes).

### Plugin family — strategies

- [strategy-float-send-rtt](https://github.com/GoodNet-io/strategy-float-send-rtt) —
  RTT-optimal multi-path picker (EWMA + 0.75 hysteresis +
  EncryptedPath tie-break).

### Bridges (language wrappers over `sdk/core.h`)

- [bridges-rust](https://github.com/GoodNet-io/bridges-rust) —
  `goodnet-sys` raw FFI + safe `goodnet` crate; ships the
  `WireSchema` trait.
- [bridges-python](https://github.com/GoodNet-io/bridges-python) —
  cffi ABI mode, `pip install`-able, no C compiler.
- [bridges-js](https://github.com/GoodNet-io/bridges-js) — TypeScript /
  JS client for the goodnetd WS gateway (talks to
  `handler-web-api-proxy`).

## Direction

The full roadmap with the per-feature livedoc badge table lives at
[`docs/ROADMAP.en.md`](https://github.com/GoodNet-io/goodnet/blob/dev/docs/ROADMAP.en.md)
in the kernel repo. Contracts that govern the public surface are in
[`docs/contracts/`](https://github.com/GoodNet-io/goodnet/tree/dev/docs/contracts).

## License

Strategic baseline (kernel + gnet protocol + the GPL-bundled link /
security / handler plugins) is GPL-2.0 with a linking exception —
out-of-tree plugins ship under any license; the boundary is the C ABI,
not the license. Periphery plugins are MIT. OpenSSL-tied plugins (TLS,
QUIC) and the reference strategy are Apache-2.0. See each repo's
`LICENSE` file.

## Reporting

Security reports go through the kernel repo's [`SECURITY.md`](https://github.com/GoodNet-io/goodnet/blob/dev/SECURITY.md).
General issues land in each sub-repo's tracker; cross-repo discussions
go to the kernel repo.
