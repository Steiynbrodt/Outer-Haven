# Glossary

This glossary defines terms as used within the Outer Haven project.
Definitions are intentionally concise and architectural rather than implementation-specific.

---

**Root Key**  
A long-lived cryptographic key that represents a user’s pseudonymous identity.

**Device Key**  
A cryptographic key associated with a specific device, delegated by the root key.

**Identity**  
A pseudonymous representation of a user based on cryptographic keys, not real-world identifiers.

**Session**  
A short-lived authorization state created after successful authentication.

**Server**  
A self-hosted community instance that manages channels, roles, and public communication.

**Relay**  
An opt-in service used to transport encrypted direct messages without access to their contents.

**Direct Message (DM)**  
A private, end-to-end encrypted message between two users.

**End-to-End Encryption (E2EE)**  
A communication model where only the communicating endpoints can read message contents.

**Transport Encryption (TLS)**  
Encryption used to protect data while it is transmitted over the network.

**Federation**  
Optional communication between independent servers without a central authority.

**Onion Routing**  
A routing technique that obscures the network path of messages by passing them through multiple relays.

**Structural Anonymity**  
An anonymity property where no single infrastructure component can reliably link sender and recipient.

**Pseudonymity**  
The use of stable identifiers that are not directly tied to real-world identity.
