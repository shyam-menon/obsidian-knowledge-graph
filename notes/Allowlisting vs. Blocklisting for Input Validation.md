**Title:** Allowlisting vs. Blocklisting for Input Validation

**Idea:** Allowlisting defines exactly what valid input looks like and rejects anything that doesn't match. Blocklisting enumerates known bad inputs and rejects those. Allowlisting is generally more robust because blocklists are inherently incomplete — attackers can always find new attack strings that weren't anticipated.

**Why it matters:** Security controls that rely on enumerating bad patterns are structurally weak. A positive-definition model (allowlist) is more future-proof and harder to bypass.

**Connections:**

- [[Server-Side Input Validation Is the Only Security Guarantee]]
- [[API Threat Model]]

## Tags
#security