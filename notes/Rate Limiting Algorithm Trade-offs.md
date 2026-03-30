**Title:** Rate Limiting Algorithm Trade-offs

**Idea:** Three primary algorithms: fixed window (simple, but gameable at window boundaries), sliding window (more accurate, no boundary exploits), and token bucket (allows short bursts while enforcing a long-run average rate). The right choice depends on whether burst traffic from legitimate callers is acceptable.

**Why it matters:** Choosing the wrong algorithm can create exploitable gaps (fixed window boundary attacks) or unnecessarily penalize legitimate burst traffic (strict sliding window with no burst allowance).

**Connections:**

- [[Rate Limiting Covers Both Attacks and Accidents]]
- [[Anomaly Detection from Traffic Baselines]]
- [[API security 101]]

Up: [[Security & auth]]

## Tags
#security