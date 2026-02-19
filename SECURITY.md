# Security Model and Threat Assumptions

This document describes the security goals, threat model, and limitations of Outer Haven.

---

## Security Goals

Outer Haven aims to:
- Prevent centralized collection of sensitive user identity data
- Protect message confidentiality via end-to-end encryption
- Limit the damage caused by server compromise
- Provide strong protection against impersonation
- Enable multi-device use without weakening identity security

---

## Non-Goals

Outer Haven does NOT attempt to:
- Prevent all metadata leakage
- Hide participation from local device compromise
- Provide perfect anonymity against a global active adversary
- Replace operating system security

Global active adversary resistance is considered beyond the scope of current Mix Mode; it may only raise the cost of correlation.

---

## Threat Model

### Trusted Components
- User devices (while uncompromised)
- Cryptographic primitives and libraries

### Untrusted Components
- Community servers
- Relay nodes
- Network transport
- Federation peers

---

## Identity Security

- Identity is based on cryptographic keys, not credentials
- Servers never receive passwords
- Authentication is done via signed challenges
- Impersonation without key compromise is infeasible

### Local Key Protection
- Root private keys are encrypted at rest
- Decryption requires:
  - a local password, and/or
  - OS-level biometrics or secure enclave
- Passwords are never transmitted or stored server-side

---

## Device Compromise

If a device is compromised:
- The attacker may impersonate the user from that device
- Other devices remain secure
- The compromised device can be revoked

---

## Server Compromise

If a server is compromised:
- Public chat data may be exposed
- Private messages remain encrypted
- User identities cannot be resolved to real-world identity
- Passwords and private keys are not exposed

---

## Relay Nodes

Relays:
- Do not have access to plaintext messages
- Do not manage user identities
- May observe limited traffic metadata

Relay abuse is mitigated via:
- Opt-in participation
- Policy restrictions (e.g. members-only)
- Rate limiting and TTLs
- Mode-aware behavior (Realtime vs. Mix Mode)

---

## Federation Risks

Federation introduces:
- Additional metadata exposure
- Trust decisions between servers

Federation is optional and disabled by default.

---

## Metadata and Correlation

Outer Haven cannot prevent all metadata leakage.
Specifically:

- Some metadata (such as timing, message size, and activity patterns) may still exist, particularly in Realtime Mode.
- Mix Mode aims to reduce observable metadata via batching, padding, and delayed delivery.
- A global passive or active adversary with widespread observation cannot be fully defeated by either mode.
- Behavioral deanonymization (e.g., schedules, writing style) remains out of scope.

---

## Cryptography

- All cryptographic operations rely on well-reviewed libraries
- Custom cryptographic primitives are avoided
- Zero-knowledge proof verification will be implemented in memory-safe languages

---

## What Outer Haven Protects You From

Outer Haven is designed to protect you from:
- Centralized mass surveillance enabled by global user accounts
- Mandatory real-world identifiers (email, phone number, government ID)
- Platform-wide data aggregation and behavioral profiling
- Data breaches exposing private messages at scale
- Silent, retroactive inspection of private communications by servers
- Single-operator control over the entire network

Mix Mode additionally aims to reduce:
- Timing correlation risk
- Observable message pattern linkage

---

## What Outer Haven Does Not Protect You From

Outer Haven is not designed to protect you from:
- Malware or compromise on your own devices
- Self-disclosure of identifying information
- Targeted investigation of a specific individual using external means
- Correlation attacks by a global adversary with full network visibility
- Behavioral deanonymization
- The need to trust communities and servers you voluntarily join

---

## Reporting Security Issues

A responsible disclosure process will be defined once the project reaches public alpha.
