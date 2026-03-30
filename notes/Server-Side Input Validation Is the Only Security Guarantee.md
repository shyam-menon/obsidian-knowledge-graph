**Title:** Server-Side Input Validation Is the Only Security Guarantee

**Idea:** Input validation must occur on the server, not just the client. Client-side validation (browser or mobile app) can be bypassed by sending requests directly to the API endpoint. Server-side validation — checking type, length, format, and range before acting on any input — is the only enforceable gate.

**Why it matters:** SQL injection and other injection attacks exploit unvalidated inputs. No access control mechanism prevents an authorized user from sending malicious data. Validation is a separate, necessary attack surface.

**Trade-offs:** Client-side validation improves UX (immediate feedback without a round trip) but must never be the sole layer. Both can coexist, but only server-side counts for security.

**Connections:**

- [[Allowlisting vs. Blocklisting for Input Validation]]
- [[API Threat Model]]
- [[Authentication and Authorization are Independent Checks]]

## Tags
#security