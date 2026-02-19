# Architecture Overview

This document describes the high-level architecture of Outer Haven.
Terminology used in this document is defined in `docs/GLOSSARY.md`.

---

## Identity Model

### Cryptographic Identity
- Each user has a **root key pair** (pseudonymous identity)
- No global usernames, emails, or phone numbers
- Identity is proven by cryptographic signatures, not credentials

### Devices
- Each device has its own **device key**
- Devices are authorized via **delegation from the root key**
- Delegation is typically done via **QR-based pairing**
- Devices can be revoked independently

### Usernames
- Usernames are **local to a server**
- Bound to the root public key
- Displayed globally as `@username@server`

---

## Authentication

- Challenge–response signatures
- No passwords sent over the network
- No server-side password storage

### Local Protection
Passwords and biometrics are used **only locally**:
- To encrypt/decrypt the root private key at rest
- To lock/unlock the application on a device

Passwords never identify a user and never leave the device.

---

## Communication Modes (Two-Lane Architecture)

Outer Haven separates transport behavior into two modes:

### Realtime Mode (Default)
Goal: Usability and low latency.

- WebSocket/QUIC-based delivery
- Immediate message propagation
- Supports:
  - Text chat
  - Direct messages
  - Voice (Realtime Mode only)
  - Federation (planned)
- Presence and typing indicators may be supported

Privacy properties:
- Transport encryption
- End-to-end encryption for DMs
- Not designed to defeat global traffic correlation

---

### Mix Mode (Opt-in High Anonymity)
Goal: Raise the cost of timing and metadata analysis.

Characteristics:
- Text-only messaging
- Batched or delayed message delivery
- Optional padding / cover traffic
- No presence indicators
- No typing indicators
- No voice or video
- No realtime presence

Mix Mode prioritizes anonymity over immediacy. It aims to reduce metadata leakage but cannot protect compromised endpoints.

---

## Servers (Communities)

Servers host:
- Channels
- Roles
- Public or semi-public chat

Servers:
- Never require real-world identity
- Store only public keys and minimal metadata
- Enforce rules locally
- May optionally act as relays (see DM Relays)

Voice and other realtime features are part of **Realtime Mode only**.

---

## Direct Messages (DMs)

- End-to-end encrypted
- Servers do not have access to plaintext
- Transported via **relay nodes**

### Relay Nodes
- Any server may optionally act as a DM relay
- Relay participation is explicit and opt-in
- Default policy: **members-only**
- Relays see only ciphertext and opaque mailbox identifiers
- Store-and-forward is supported for offline delivery
- Realtime vs. Mix delivery depends on communication mode

---

## Federation (Planned)

- Optional server-to-server communication
- No central authority
- Signed events
- Global identity = cryptographic key

Federation increases interoperability but also expands metadata exposure.

---

## Message Confidentiality Model

Outer Haven separates transport security from end-to-end encryption.

### Transport Encryption
All client–server and server–server communication is encrypted in transit using TLS.
This protects against network observers but does not hide data from hosting servers.

### Direct Messages
Direct messages are end-to-end encrypted.
Servers and relay nodes cannot read message contents.

### Server Channels (Default)
By default, server channels are not end-to-end encrypted.
Messages are readable by the hosting server to allow moderation, indexing, and usability.

### Private Channels (Planned)
End-to-end encrypted server channels are planned as an optional per-channel mode.
In this mode, only channel members can read message contents, and the server stores only encrypted data.

---

## Zero-Knowledge Proofs (Planned)

Used for **claims**, not identity:
- Age verification (e.g. 18+)
- Rate-limiting
- Membership proofs

Servers verify proofs without learning personal data.

---

## Technology Stack (Planned)

- TypeScript: core services and clients
- Rust (later): security-critical components and ZKP verification
- WebSockets: realtime communication
- PostgreSQL / Redis: minimal state
- LiveKit: self-hosted voice (Realtime Mode only)
- libsodium / noble: cryptographic primitives
- Mix Mode relay and batching engines
