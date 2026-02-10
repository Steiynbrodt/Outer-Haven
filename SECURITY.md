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
- Provide perfect anonymity against a global network adversary
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

## Cryptography

- All cryptographic operations rely on well-reviewed libraries
- Custom cryptographic primitives are avoided
- Zero-knowledge proof verification will be implemented in memory-safe languages

---

## Reporting Security Issues

A responsible disclosure process will be defined once the project reaches public alpha.
