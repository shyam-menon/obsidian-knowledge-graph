**Title:** Webhooks vs. Polling

**Idea:** Polling has a client repeatedly querying the server for updates at fixed intervals — wasteful when updates are infrequent. Webhooks invert this: the server pushes a notification to the client's registered URL the moment an event occurs. This is event-driven and near-real-time.

**Why it matters:** Webhooks reduce latency, CPU, and bandwidth compared to polling. They are the foundational pattern for event-driven integrations and reactive systems.

**Trade-offs:** Webhooks require the client to expose a public endpoint and handle delivery reliability (retries, deduplication). Polling is simpler to implement but wasteful at scale.

**Connections:**

- [[OAuth 2.0 — Delegated Authorization]]
- [[Bulk Data Transfer Pattern]]
- [[Event-Driven Architecture]]