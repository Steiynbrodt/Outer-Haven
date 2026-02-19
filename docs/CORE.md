# Core Architecture Commitments

This document defines the non-negotiable architectural foundations of Outer Haven.

The purpose of this file is to prevent architectural drift and to clarify which components are considered stable core versus flexible implementation detail.

Changes to Core require:
- Threat model review
- Explicit documentation update
- Careful backward compatibility consideration

---

# 1. Cryptographic Identity

Outer Haven identity is based on cryptographic keys, not credentials.

Core properties:

- Each user has a **root key pair**
- Each device has a **device key**
- Device keys are delegated from the root key
- Delegation can be revoked independently
- Authentication is performed via signed challenge–response
- No passwords are transmitted or stored server-side

Compromise of a root private key equals identity compromise.

This model is non-negotiable.

---

# 2. Event and Message Model

All communication is based on signed events.

Every event must include:

- Sender root public key (or key identifier)
- Device key identifier
- Timestamp or nonce
- Target (channel / DM / system event)
- Cryptographic signature
- Payload (plaintext or ciphertext depending on context)

Core guarantees:

- Replay protection
- Signature verification before processing
- Versioned event format
- Deterministic validation rules

Transport mechanisms must not alter event integrity.

---

# 3. Communication Mode Separation

Outer Haven defines two communication modes:

## Realtime Mode (Default)
- Low latency
- Interactive features allowed
- Not designed to resist global traffic correlation

## Mix Mode (Opt-in)
- Text-only
- Batched or delayed forwarding
- Optional padding / cover traffic
- No presence indicators
- No typing indicators
- No read receipts
- No voice or video

Mode differences are architectural, not cosmetic.

Mix Mode prioritizes anonymity over immediacy.

---

# 4. Encryption Boundaries

Outer Haven separates transport encryption from end-to-end encryption.

Core commitments:

- All transport links use TLS or equivalent secure transport
- Direct messages are end-to-end encrypted
- Servers cannot read DM plaintext
- Public server channels are readable by the hosting server
- End-to-end encrypted server channels are optional and explicitly defined

Encryption boundaries must remain explicit and documented.

---

# 5. Trust Boundaries

Outer Haven assumes:

Untrusted:
- Community servers
- Relay nodes
- Federation peers
- Network transport

Trusted (while uncompromised):
- User devices
- Local key storage

Core principle:
Minimize the amount of sensitive data exposed to any single infrastructure component.

---

# 6. Threat Model Alignment

The Core must remain consistent with:

- `docs/THREAT_MODEL.md`
- Explicit non-goals
- Explicit limitations

Outer Haven does not claim:

- Perfect anonymity
- Immunity against a global active adversary
- Protection against endpoint compromise

Security claims must remain proportional to technical guarantees.

---

# 7. What Is Not Core

The following components are flexible and may evolve:

- Client UI implementations
- Server implementation language
- Relay routing algorithms
- Federation mechanisms
- Voice and media systems
- Rate limiting strategies
- Zero-knowledge proof integrations
- Performance optimizations

These may change without redefining the Core, provided they do not violate the commitments above.

---

# 8. Architectural Stability Principle

Outer Haven prioritizes:

- Coherent identity design
- Clear cryptographic boundaries
- Explicit threat assumptions
- Mode-aware behavior
- Minimal data collection

Feature additions must not weaken these foundations.

If a proposed feature conflicts with Core principles, the Core prevails.
