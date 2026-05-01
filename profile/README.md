# GoodNet

A platform for distributed networking. The kernel is minimal, the brand
is the ecosystem, and a node joins by carrying a single binary and a
keypair.

## What it is

GoodNet provides a connection fabric where the address of a participant
is its public key, every byte on the wire is encrypted by default, and
the software a participant runs decides what messages mean. The platform
itself is the kernel plus the SDK — everything else is built on top by
independent plugins, each with its own license, repository, and release
cadence.

## Repositories

- **`goodnet`** — kernel, SDK, and baseline plugins (TCP / UDP / IPC /
  WebSocket / TLS link plugins; Noise XX/IK security; GNET envelope
  framing; heartbeat handler). One binary and a keypair join two nodes
  end-to-end through Noise over a real socket.
- **`.github`** — community defaults for the organization (this
  repository).

Plugin repositories spin off as the kernel surface stabilises:
NAT-traversal, multi-path scheduler, directed-relay upgrade, address
routing (DHT), persistence (storage / sync), and language bindings
each land in their own repository with independent release cadence.
The roadmap inside `goodnet` describes the order of work.

## Status

Pre-release. The C ABI surface in `sdk/host_api.h` is open for reshape
until the first stable tag; after the tag every slot is append-only.
The kernel runs end-to-end today: two processes exchange application
envelopes over a real socket through a Noise handshake, with
backpressure, hot config reload, connection-event subscriptions, and a
dispatching router in between. The work that follows the snapshot lives
in [the roadmap](https://github.com/GoodNet-io/goodnet/blob/main/docs/ROADMAP.md).

## License

Kernel and the mandatory protocol layer are GPL-2.0 with a Linking
Exception that releases the plugin boundary from copyleft propagation;
the SDK is MIT. Plugins carry their own license — MIT, BSD, Apache 2.0,
or proprietary — provided they interface with the kernel only through
the stable C ABI in the SDK.

## Reporting

- **Vulnerabilities** — open a
  [private security advisory](https://github.com/GoodNet-io/goodnet/security/advisories/new)
  in the `goodnet` repository.
- **Conduct** — see
  [Code of Conduct](https://github.com/GoodNet-io/goodnet/blob/main/CODE_OF_CONDUCT.md).
- **Bugs and feature work** — file an issue against the relevant
  repository.
