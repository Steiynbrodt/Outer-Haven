# Outer Haven

**A place outside centralized control.**

Outer Haven is a community chat platform inspired by the usability of modern tools like Discord, but built on a fundamentally different foundation:

- **Cryptographic identity instead of accounts**
- **Privacy enforced by architecture instead of policy**
- **Decentralized deployment without requiring centralized control**

Outer Haven introduces a **two-lane communication model**:

- **Realtime Mode (default)** – low-latency, highly usable communication.
- **Mix Mode (opt-in)** – higher-latency, text-only communication designed to reduce metadata leakage and raise the cost of traffic analysis.

The goal is not to evade moderation or law, but to build a system where communities can function normally **without requiring centralized user identity, personal data collection, or platform-level control**.

---

## Motivation

Modern communication platforms increasingly require:

- Centralized accounts
- Permanent identifiers (email, phone number, government ID)
- Invasive verification mechanisms
- Trust in operators not to misuse collected data

Outer Haven explores a different approach:

> If a system does not collect sensitive data, it cannot be abused, leaked, or demanded.

Rather than promising privacy, Outer Haven aims to **enforce it by design**.

---

## Core Ideas

- **No global accounts** (no email, phone number, or real-world identity)
- **Pseudonymous but stable identity** via cryptographic keys
- **Multi-device support** without central login systems
- **End-to-end encrypted direct messages (DMs)** delivered via opt-in relay nodes
- **Self-hostable servers**, with optional federation
- **Compliance through technical enforcement**, not data collection

Outer Haven distinguishes between public server channels and private communication:

- All traffic is encrypted in transit.
- Direct messages are end-to-end encrypted by default.
- Server channels are readable by the hosting server (for moderation and usability).
- End-to-end encrypted server channels are planned as an optional feature for private channels.

---

# Two-Lane Communication Model

Outer Haven separates usability-focused communication from anonymity-focused communication.

## Realtime Mode (Default)

Designed for usability and low latency.

Supports:
- Text chat
- Direct messages
- Voice (planned)
- Federation (planned)

Characteristics:
- Immediate message propagation
- Presence indicators (optional)
- Typing indicators (optional)
- Read states (optional)

Privacy properties:
- Transport encryption
- End-to-end encryption for DMs
- Not designed to defeat global traffic correlation by a state-level adversary

Realtime Mode prioritizes usability while minimizing centralized identity and data aggregation.

---

## Mix Mode (Opt-in High Anonymity)

Designed to reduce metadata leakage and raise the cost of timing and traffic correlation.

Characteristics:
- Text-only communication
- Batched or delayed message delivery
- Optional padding / cover traffic
- No presence indicators
- No typing indicators
- No read receipts
- No voice or video

Mix Mode prioritizes anonymity over immediacy.

It aims to raise the cost of large-scale traffic analysis but cannot protect against compromised endpoints or behavioral deanonymization.

---

## Project Status

Outer Haven is in early active development.

The project is documentation-first while identity, relay behavior, federation boundaries, and encryption models are refined.

Planned milestones:

- **v0.1** – Identity, sessions, device pairing  
- **v0.2** – Servers and text chat (Realtime Mode)  
- **v0.3** – Direct messages (relay-based delivery)  
- **v0.4** – Voice (Realtime Mode only)  
- **v0.5** – Federation  
- **v0.6** – Zero-knowledge claims (e.g. age verification)  
- **v0.7** – Mix Mode transport layer  

Until Mix Mode is implemented, users requiring stronger network-layer anonymity should rely on external tools such as Tor or other privacy-preserving transport systems.

---

## Threat Model Overview

Outer Haven considers multiple adversaries:

- Platform operators
- Data-aggregating service providers
- Local network observers
- State-level traffic observers

Realtime Mode prioritizes usability and decentralization.

Mix Mode prioritizes stronger resistance to metadata and traffic correlation at the cost of latency and features.

Outer Haven does not claim to defeat a fully global active adversary with endpoint compromise capability.

---

## What Outer Haven Protects You From

Outer Haven is designed to reduce:

- Centralized mass surveillance enabled by global user accounts
- Mandatory real-world identifiers (email, phone number, government ID)
- Platform-wide data aggregation and behavioral profiling
- Data breaches exposing private messages at scale
- Silent retroactive inspection of encrypted direct messages
- Single-operator control over the entire network

Mix Mode additionally aims to reduce:

- Timing correlation risk
- Observable message pattern leakage
- Direct linkability between sender and recipient at the transport level

---

## What Outer Haven Does Not Protect You From

Outer Haven is not designed to protect you from:

- Malware or compromise on your own devices
- Self-disclosure of identifying information
- Targeted investigation using external intelligence sources
- Behavioral deanonymization (e.g., writing style, activity timing)
- Correlation by a fully global adversary observing the entire network in Realtime Mode
- The need to trust communities and servers you voluntarily join

---

## Non-Goals

- No advertising or tracking
- No real-name policies
- No global moderation authority
- No mandatory central services
- No claim of absolute anonymity

---

## Documentation-First Approach

Outer Haven is currently in a research and design phase.

This repository intentionally starts with documentation to lock down:

- Identity model
- Relay boundaries
- Federation assumptions
- Encryption layers
- Threat model

Code will be introduced incrementally once the identity and security model are considered stable.

---

## Platform Support

Outer Haven targets cross-platform support.

Initial focus:
- Web client

Planned:
- Android
- Windows
- Linux

iOS and macOS support possible but not planned yet.

---

## Docs

- Architecture: `docs/ARCHITECTURE.md`
- Threat model: `SECURITY.md`
- Terminology: `docs/GLOSSARY.md`

---
## Key Architecture

Outer Haven separates long-term identity from message encryption.

Each user possesses a persistent identity key that represents their stable pseudonymous identity.
This key is used only for authentication and establishing secure sessions.

Actual message encryption uses short-lived, rotating session keys that are periodically replaced.

This design provides forward secrecy and limits the impact of any key compromise, while keeping identities portable and independent of servers.
---
## Project Role

Outer Haven is distributed as open-source software.

The project does not operate:

- A centralized communication service
- A global identity provider
- A mandatory relay network

Communities operating servers are responsible for their own governance, moderation, and legal compliance within their jurisdiction.

The purpose of this project is to provide privacy-preserving, decentralized communication infrastructure — not to control how independent communities choose to use it.

---
## Why not Matrix?

Outer Haven and Matrix share several goals: decentralization, end-to-end encryption, and user autonomy.  
However, they differ fundamentally in how identity and communities are structured.

### Identity Model

**Matrix**
- Identity = account on a homeserver (`@user:server`)
- Homeserver manages identity and devices
- Accounts are server-bound
- Migration between servers is complex

**Outer Haven**
- Identity = cryptographic root key
- No global accounts or identity providers
- Identity is independent of any server
- Users can move freely between communities

 Outer Haven identities are self-authenticating and portable.

---

### Community Ownership

**Matrix**
- Rooms exist within the federation graph
- Homeservers retain structural influence
- Moderation spans multiple servers

**Outer Haven**
- Communities are self-hosted servers
- No global namespace dependency
- Moderation is purely local
- Communities remain autonomous

 Communities belong to their hosts, not the network.

---

### Identity–Server Relationship

**Matrix**
- Servers store accounts, devices, and membership graphs
- Identity continuity depends on server availability
- Servers act as identity providers

**Outer Haven**
- Servers store only public keys and minimal metadata
- Identity continuity is user-held
- Servers cannot issue or revoke identities

Servers do not control users.

---

### Encryption Model

**Matrix**
- Device-centric E2EE (Olm/Megolm)
- Accounts manage key hierarchies
- Session rotation varies by context

**Outer Haven**
- Root identity keys + rotating session keys
- Identity keys never encrypt messages
- Sessions are ephemeral and regularly rotated

Encryption is identity-independent and server-agnostic.

---

### Network Philosophy

**Matrix**
- Global federated communication fabric
- Interoperability across servers by default

**Outer Haven**
- Community-centric architecture
- Federation optional and minimal
- Designed for autonomous groups first

Outer Haven prioritizes community sovereignty over global connectivity.

---

### Summary

Matrix is a federated messaging network with server-managed accounts.  
Outer Haven is a community-owned communication model with server-independent identities.

They are complementary approaches with different priorities:

- Matrix → global federation and interoperability  
- Outer Haven → autonomous communities and portable identity
## License

MIT
