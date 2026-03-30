**Title:** Monitoring and Logging for Retroactive Visibility

**Idea:** Monitoring and logging are the only API security strategies that work retroactively. They don't prevent attacks but enable detection during an incident and forensic reconstruction after. Without logs, you cannot know what an attacker accessed. Key signals include auth events, authorization failures, unusual request patterns, and validation rejections.

**Why it matters:** Teams systematically underinvest in logging because it has no visible immediate payoff. This gap is most painful during and after incidents, when logs are the primary source of truth about what happened.

**Trade-offs:** Comprehensive logs may capture PII, health, or financial data, creating privacy regulation obligations. Structured logging (JSON) and centralized aggregation must be built early — retrofitting at scale is significantly harder.

**Connections:**

- [[Anomaly Detection from Traffic Baselines]]
- [[API Threat Model]]
- [[Rate Limiting Covers Both Attacks and Accidents]]