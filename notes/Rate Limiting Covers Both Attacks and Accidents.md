**Title:** Rate Limiting Covers Both Attacks and Accidents

**Idea:** Rate limiting caps the number of requests a caller can make within a time window. It protects against deliberate threats (brute-force, scraping) but equally handles accidental overload (misconfigured clients, runaway jobs). Throttling is a softer variant that degrades rather than blocks service for over-limit callers.

**Why it matters:** Rate limiting is often framed purely as a security tool, but its resilience value for operational stability (preventing accidental overload) is equally important. It's both a security and reliability mechanism.

**Trade-offs:** Calibration is the hard problem: thresholds set too aggressively break legitimate high-volume use cases (e.g., data pipelines); too loose and protection is meaningless. Requires observing real traffic before tuning.

**Connections:**

- [[Rate Limiting Algorithm Trade-offs]]
- [[API Threat Model]]
- [[Monitoring and Logging for Retroactive Visibility]]

## Tags
#security