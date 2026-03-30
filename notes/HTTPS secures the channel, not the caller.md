**Title:** HTTPS Secures the Channel, Not the Caller

**Idea:** TLS/HTTPS encrypts data in transit between client and server, preventing interception and tampering. It does not verify the identity of the caller or whether they are permitted to perform an action. A stolen credential used over HTTPS is indistinguishable from a legitimate one at the transport layer.

**Why it matters:** Teams often treat HTTPS as a complete security solution. Understanding its scope prevents over-reliance on transport-layer encryption while neglecting identity and permission controls.

**Trade-offs:** TLS 1.3 has a minor performance overhead vs. plain HTTP, but this is negligible compared to the risk of not using it.

**Connections:**

- [[Authentication vs. Authorization]]
- [[API Threat Model]]
- [[Man-in-the-Middle Attack]]

## References
https://gemini.google.com/share/34fff59675e4
