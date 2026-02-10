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
- Provide perfect anonymity against a global network adversary not because we dont want to but because its physically impossible :(
- Replace operating system security

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
- opt-in participation
- policy restrictions (e.g. members-only)
- rate limiting and TTLs

---

## Federation Risks

Federation introduces:
- additional metadata exposure
- trust decisions between servers

Federation is optional and disabled by default.

---

### Security boundaries and limitations

Outer Haven is designed to significantly reduce centralized surveillance and mass data collection.
It does not claim to make users invisible or untouchable.

Specifically:

- The system is not designed to defeat a hypothetical all-seeing global observer.
  Instead, it removes the single points of control and data aggregation that make mass surveillance easy today.

- Some metadata (such as timing or message size) may still exist, particularly without optional onion-style routing.
  This metadata is decentralized and fragmented across servers rather than centrally collected.

- If a user’s own device is compromised, local data may be exposed.
  This is true for all secure communication systems and is outside the scope of server-side protections.

- By default, community servers can read messages in their own public channels,
  similar to existing community platforms.
  End-to-end encrypted private channels are planned as an opt-in feature.

- Federation increases interoperability but also increases the number of independent parties involved.
  No single entity gains a complete view of user activity.


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

## Cryptography

- All cryptographic operations rely on well-reviewed libraries
- Custom cryptographic primitives are avoided
- Zero-knowledge proof verification will be implemented in memory-safe languages

---

## Reporting Security Issues

A responsible disclosure process will be defined once the project reaches public alpha.
