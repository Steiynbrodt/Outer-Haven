# Threat Model

This document defines the threat assumptions, adversaries, security goals, and explicit limitations of Outer Haven.

It exists to prevent overclaiming and to guide architectural decisions.

Outer Haven separates usability-focused communication (Realtime Mode) from anonymity-focused communication (Mix Mode). Threat assumptions differ between these modes.

---

# 1. Security Goals

Outer Haven aims to:

- Eliminate centralized global identity accounts
- Prevent large-scale collection of real-world identifiers
- Protect message confidentiality via end-to-end encryption (DMs)
- Limit damage from server compromise
- Provide pseudonymous but stable identity
- Reduce metadata exposure where technically feasible
- Raise the cost of traffic correlation in Mix Mode

Outer Haven does **not** aim to provide absolute anonymity.

---

# 2. Assets to Protect

## 2.1 Identity Assets
- Root private keys
- Device keys
- Delegation chains

## 2.2 Communication Assets
- Direct message content
- Private channel content (when E2EE is enabled)
- Server membership associations
- Metadata linking sender and recipient

## 2.3 Infrastructure Assets
- Relay routing behavior
- Federation event integrity
- Server trust boundaries

---

# 3. Adversary Classes

## 3.1 Curious Server Operator
Capabilities:
- Access to server-stored data
- Access to public channel messages
- Visibility into server-level metadata

Not capable of:
- Reading end-to-end encrypted DMs
- Deriving root private keys

---

## 3.2 Malicious Relay Operator
Capabilities:
- Observing ciphertext
- Observing timing and size of messages
- Attempting traffic correlation

Not capable of:
- Reading encrypted content
- Breaking modern cryptographic primitives

---

## 3.3 Local Network Observer
Capabilities:
- Observing client–server encrypted traffic
- Timing and packet size analysis

Cannot:
- Decrypt TLS-protected traffic
- Read end-to-end encrypted message content

---

## 3.4 Federation Peer
Capabilities:
- Observing cross-server metadata
- Attempting event replay or injection

Mitigations:
- Signed events
- Validation rules
- Optional federation participation

---

## 3.5 State-Level Passive Adversary
Capabilities:
- Monitoring large portions of network traffic
- Traffic timing correlation
- Statistical analysis across relays

Realtime Mode:
- Not designed to resist this adversary.

Mix Mode:
- Aims to raise the cost of correlation via batching and optional padding.
- Does not guarantee resistance against a fully global passive adversary.

---

## 3.6 State-Level Active Adversary
Capabilities:
- Traffic injection
- Relay flooding
- Sybil attacks (operating many relays)
- Blocking traffic
- Legal coercion
- Large-scale infrastructure monitoring

Outer Haven does not claim to defeat a fully global active adversary.

Mix Mode may increase the cost of correlation, but cannot eliminate it.

---

## 3.7 Compromised Endpoint
Capabilities:
- Full access to user device
- Key extraction
- Message exfiltration

Out of scope:
- Outer Haven cannot protect against a compromised endpoint.

---

# 4. Mode-Specific Assumptions

## 4.1 Realtime Mode

Prioritizes:
- Usability
- Low latency
- Interactive features

Risks:
- Timing correlation
- Presence-based metadata leakage
- Activity pattern analysis

Not designed to:
- Resist global correlation attacks
- Obfuscate traffic patterns

---

## 4.2 Mix Mode

Prioritizes:
- Reduced timing leakage
- Reduced direct sender–receiver linkability
- Increased cost of traffic analysis

Mechanisms (planned):
- Batched forwarding
- Delayed delivery
- Optional padding / cover traffic
- Removal of realtime presence indicators
- Text-only communication

Limitations:
- Cannot prevent endpoint compromise
- Cannot prevent behavioral deanonymization
- Cannot guarantee protection against a fully global adversary

---

# 5. Explicit Non-Goals

Outer Haven does NOT aim to:

- Provide perfect anonymity
- Hide long-term behavioral patterns
- Replace OS-level or device-level security
- Guarantee resistance against a global active adversary
- Prevent lawful investigation using external intelligence sources

---

# 6. Cryptographic Assumptions

- Standard, well-reviewed cryptographic libraries are used
- No custom cryptographic primitives are introduced without peer review
- Key compromise equals identity compromise
- Cryptographic strength depends on secure key storage

---

# 7. Abuse Considerations

Outer Haven acknowledges that:

- Strong anonymity can be misused
- Relay infrastructure may be abused
- Sybil attacks are possible in decentralized systems

Mitigations include:
- Rate limiting
- Relay policy restrictions
- Mode-aware restrictions
- Optional trust models (future work)

Outer Haven provides infrastructure; server operators remain responsible for governance within their communities.

---

# 8. Residual Risks

Even in Mix Mode:

- Traffic analysis may remain possible
- Global adversaries may correlate activity
- Long-term usage patterns may deanonymize users
- Relay participation may expose partial metadata

No anonymity guarantee is absolute.

---

# 9. Design Philosophy

Outer Haven aims to:

- Minimize data collection
- Reduce centralized power
- Provide clear trade-offs between usability and anonymity
- Avoid overstating security guarantees

Security claims are limited to what can be technically justified.
