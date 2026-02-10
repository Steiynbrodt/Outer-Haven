# Identity Scope

This document defines the scope and boundaries of identity in Outer Haven.
It exists to prevent accidental expansion of identity concepts beyond their intended role.

---

## What identity is
- A stable, pseudonymous identifier based on a cryptographic root key.
- A way for the system to recognize the same participant across sessions and devices.
- Local to the system and not tied to real-world identity.

## What identity is not
- Not a real name, email address, phone number, or government-issued identifier.
- Not a global account controlled by a central authority.
- Not a guarantee of anonymity in all circumstances.

## What the server knows
- A user’s public root key (or a derived identifier).
- Which device keys are currently authorized for that identity.
- Server-local metadata such as usernames, roles, and session state.

## What the server never knows
- Private keys or key material.
- Passwords used to unlock keys on user devices.
- Real-world identity information unless explicitly disclosed by the user.

## What is deferred
- Zero-knowledge claims tied to identity (e.g. age verification).
- Cross-server identity resolution via federation.
- Network-level anonymity mechanisms such as onion routing.
