# Outer Haven

**A place outside centralized control.**

Outer Haven is a community chat platform inspired by the usability of modern tools like Discord, but built on a fundamentally different foundation: **cryptographic identity instead of accounts, privacy by architecture instead of policy, and decentralization without sacrificing usability**.

The goal is not to evade moderation or law, but to build a system where communities can function normally **without requiring centralized user identity, personal data collection, or platform-level control**.



---

## Motivation

Modern communication platforms increasingly require:
- centralized accounts
- permanent identifiers (email, phone number, government ID)
- invasive verification mechanisms
- trust in operators not to misuse collected data

Outer Haven explores a different approach:

> If a system does not collect sensitive data, it cannot be abused, leaked, or demanded.

Rather than promising privacy, Outer Haven aims to **enforce it by design**.

---

## Core Ideas

- **No global accounts** (no email, phone number, or real-world identity)
- **Pseudonymous but stable identity** via cryptographic keys
- **Multi-device support** without central login systems
- **End-to-end encrypted private messages(DM)**, delivered via opt-in relay nodes (any server can optionally act as a relay)
- **Self-hostable servers**, with optional federation
- **Compliance through technical enforcement**, not data collection
- **Outer Haven distinguishes between public server channels and private communication.
All traffic is encrypted in transit. Direct messages are end-to-end encrypted by default.
End-to-end encrypted server channels are planned as an optional feature for private channels,
while public channels remain readable by the hosting server for moderation and usability.**

---

## Project Status

Outer Haven is in early active development.
Outer Haven’s initial design prioritizes privacy and decentralization.
Optional onion-style routing is planned for later stages of development to further reduce
network-level linkability and increase resistance to traffic analysis.
Until onion routing is implemented, users who require stronger network-level anonymity
should rely on external network-layer tools (such as Tor or a trusted VPN),
which operate independently of Outer Haven and might have diffrent principles and values.





Planned milestones:
- **v0.1** – Identity, sessions, device pairing
- **v0.2** – Servers and text chat
- **v0.3** – Direct messages (1-hop relay)
- **v0.4** – Voice
- **v0.5** – Federation
- **v0.6** – Zero-knowledge claims (e.g. age verification)

---
## Why this repository is documentation-first (for now)

Outer Haven is currently in a research and design phase. This repository intentionally starts with documentation to lock down the core architecture and threat model before implementation.

The author is currently learning TypeScript (previous work has been primarily in C/C++ and Python) and is validating a few design assumptions (identity, relays, federation, and encryption boundaries) before writing production code. also this is the largest most organized and thought through Project the author has done up to this point
Code will be introduced incrementally once the identity and security model
are considered stable.
---
## Platform support

Outer Haven targets cross-platform support. Early development will focus on a web client (and later Android/Windows/Linux).
iOS and macOS support possible but not planned (yet) 

## Docs
- Architecture: `docs/ARCHITECTURE.md`
- Threat model: `SECURITY.md`

---

## What Outer Haven protects you from / what it doesn’t

### Outer Haven is designed to protect you from:
- Centralized mass surveillance enabled by global user accounts
- Mandatory real-world identifiers (email, phone number, government ID)
- Platform-wide data aggregation and behavioral profiling
- Data breaches exposing private messages at scale
- Silent, retroactive inspection of private communications by servers
- Single-operator control over the entire network

### Outer Haven is not designed to protect you from:
- Yourself, if you choose to share identifying information
- Malware or compromise on your own devices
- Targeted investigation of a specific individual using external means
- Metadata exposure inherent to any online communication (reduced further with optional onion routing)
- The need to trust the communities and servers you voluntarily join
- Correlation attacks performed by a powerful observer monitoring large portions of the network
- Anonymity loss caused by long-term behavior patterns (e.g. consistent activity schedules, writing style)

## Non-Goals

- No advertising or tracking
- No real-name policies
- No global moderation authority
- No mandatory central services

---
## Optional turnkey deployments (future idea not planned yet just idea stage no concept just an idea and depends on how big this gets)

In the future, Outer Haven may offer optional prebuilt, self-hostable servers/relays for people who want a simple “plug it in and it works” setup.
These would remain fully under the user’s control (no mandatory central hosting), and are intended to be affordable and accessible.



## License

MIT

