# Architecture Overview

This document describes the high-level architecture of Outer Haven.

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

## Servers (Communities)

Servers host:
- Channels
- Roles
- Public or semi-public chat
- Voice channels

Servers:
- Never require real-world identity
- Store only public keys and minimal metadata
- Enforce rules locally

---

## Direct Messages (DMs)

- End-to-end encrypted
- Servers do not have access to plaintext
- Transported via **relay nodes**

### Relay Nodes
- Any server may optionally act as a DM relay
- Relay participation is explicit and opt-in
- Default policy: **members-only**
- Relays see only ciphertext and mailbox identifiers
- Store-and-forward is supported for offline delivery

---

## Federation (Planned)

- Optional server-to-server communication
- No central authority
- Signed events
- Global identity = cryptographic key

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
- LiveKit: self-hosted voice
- libsodium / noble: cryptographic primitives
