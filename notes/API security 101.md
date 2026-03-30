**The 4 Core API Threat Categories**

- Unauthorized access — wrong person or wrong permissions reach data/functionality
- Malicious or malformed input — crafted or bad data exploits unguarded endpoints (e.g., SQL injection)
- Abuse and overload — too many requests, deliberate (scraping, brute-force) or accidental (runaway client)
- Information leakage — verbose errors, unfiltered responses, inconsistent access controls expose internals

**HTTPS: Channel Security Only**

- Wraps HTTP in TLS, encrypts data in transit, prevents man-in-the-middle attacks
- Does NOT authenticate or authorize — a stolen key over HTTPS is still valid
- TLS 1.2/1.3 are current standards; TLS 1.0/1.1 have known vulnerabilities and must be disabled
- "Encrypted connection" ≠ "Secure API" — this conflation is a recurring mistake

**Authentication vs. Authorization (Critical Distinction)**

- Authentication = "Who are you?" — verifies identity via API key, token, or credential
- Authorization = "What are you allowed to do?" — verifies permission on a per-resource basis
- These are independent checks; passing one does NOT imply passing the other
- Broken Object Level Authorization (BOLA): authenticated users access other users' data by changing an ID in the URL — one of the most common API vulnerabilities
- API keys are long passwords; they must be stored securely, rotated, and paired with authorization

**Role-Based Access Control (RBAC)**

- Permissions attach to roles (admin, read-only, billing manager), not individual users
- Users get assigned to roles — adding users or changing permissions becomes role-level operations
- Underpinned by Principle of Least Privilege: give every caller the minimum access actually needed
- Blast radius concept: limited permissions = limited damage when credentials are compromised
- RBAC degrades over time: roles accumulate, overlap, edge cases create one-off grants
- Attribute-Based Access Control (ABAC) is the next step: evaluates identity + resource + context together — more expressive, more complex

**Input Validation**

- Even fully authenticated, authorized callers can send harmful data
- Must validate: type, length, format, and range for every input
- Allowlisting (define valid input, reject everything else) > blocklisting (enumerate bad input, inevitably misses cases)
- Server-side validation is the only security guarantee — client-side can be bypassed entirely by sending requests directly to the API

**Rate Limiting and Throttling**

- Rate limiting: hard ceiling on requests per time window; excess requests are rejected
- Throttling: soft version — slows responses for over-limit callers without full rejection
- Protects against: brute-force attacks, deliberate scraping, AND accidental overload (misconfigured clients)
- Algorithm options: fixed window (simple, gameable at boundaries), sliding window (more accurate), token bucket (allows bursts while enforcing average rate)
- Calibration challenge: too tight breaks legitimate high-volume use; too loose renders limits useless — requires observing real traffic patterns

**Monitoring and Logging**

- Retroactive strategy: doesn't prevent attacks, but tells you what happened and when
- What to log: auth events (success + failure), authorization failures, unusual patterns, validation rejections, unexpected errors
- Enables anomaly detection once a baseline of normal traffic is established
- Trade-off: comprehensive logs may contain PII, health, or financial data — subject to privacy regulations
- Structured logging (JSON) + centralized aggregation makes logs searchable at scale
- Build logging infrastructure early — retrofitting it is expensive

---

## Cues

**Keywords:** HTTPS, TLS, Authentication, Authorization, BOLA, RBAC, ABAC, Least Privilege, Input Validation, Allowlist, Blocklist, Rate Limiting, Token Bucket, Throttling, Monitoring, Structured Logging

**Recall Questions:**

- Why does HTTPS not make an API secure on its own?
- What is the difference between authentication and authorization, and why does conflating them lead to vulnerabilities?
- What is Broken Object Level Authorization, and how is it exploited?
- Why is allowlisting preferred over blocklisting for input validation?
- Why must input validation always happen server-side?
- How does rate limiting protect against non-malicious overload?
- What makes RBAC degrade over time, and when should you move to ABAC?
- Why is monitoring often underinvested, and what does that cost during incidents?
- When would you choose a token bucket algorithm over a sliding window?

---

## Summary

API security is not a checklist — it is a threat-response mapping. Four core threats exist (unauthorized access, bad input, overload, information leakage), and each security strategy directly addresses one or more of them. The most critical and commonly misunderstood distinction is authentication vs. authorization: knowing _who_ someone is doesn't mean you know _what_ they're allowed to do, and the failure to enforce this per resource is the root cause of BOLA, one of the most widespread API vulnerabilities. Beyond access control, input validation (server-side only), rate limiting (for both attacks and accidents), and structured logging (retroactive visibility) complete the security posture. Security is an ongoing maintenance discipline, not a one-time setup.

## Related notes
- [[HTTPS secures the channel, not the caller]]
- [[Authentication and Authorization are Independent Checks]]
- [[Broken object level authorization (BOLA)]]
- [[API Keys Are Long Passwords]]
- [[Role-Based Access Control (RBAC)]]
- [[Principle of Least Privilege]]
- [[Server-Side Input Validation Is the Only Security Guarantee]]
- [[Allowlisting vs. Blocklisting for Input Validation]]
- [[Rate Limiting Covers Both Attacks and Accidents]]
- [[Rate Limiting Algorithm Trade-offs]]
- [[Monitoring and Logging for Retroactive Visibility]]
- [[Anomaly Detection from Traffic Baselines]]
- [[Attribute-Based Access Control (ABAC)]]
- [[JWT and OAuth 2.0 for Scoped Access]]

## Sources
https://blog.bytebytego.com/p/how-to-implement-api-security
## Systems
[[AIaaS Platform]]

## Tags
#security