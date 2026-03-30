**Title:** JWT and OAuth 2.0 for Scoped Access

**Idea:** JWT (JSON Web Tokens) and OAuth 2.0 extend basic authentication by introducing token expiry and scoped access (limiting what a token can do). JWTs are self-contained, signed tokens that carry claims. OAuth 2.0 is a delegation framework enabling third-party access without sharing raw credentials.

**Why it matters:** API keys have no built-in expiry or scope. JWTs and OAuth 2.0 reduce the window of exposure for leaked tokens and enable fine-grained delegation — essential for third-party integrations and microservices architectures.

**Trade-offs:** More complex to implement than API keys. Token lifecycle management (refresh, revocation) introduces new failure modes. Worth the complexity as systems grow and third-party integrations multiply.

**Connections:**

- [[API Keys Are Long Passwords]]
- [[Authentication and Authorization are Independent Checks]]
- [[Principle of Least Privilege]]
- [[OAuth 2.0 — Delegated Authorization]]