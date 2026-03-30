**Title:** Semantic Caching in RAG

**Idea:** Semantic caching stores prior retrieval results and associates them with the semantic meaning of past queries. Future queries with similar meaning can retrieve cached results instead of triggering a full retrieval cycle.

**Why it matters:** In high-volume systems, many queries are semantically equivalent even if worded differently. Caching these results reduces latency and cost while preserving answer quality — especially beneficial in agentic systems where retrieval is expensive.

**Connections:**

- [[Agentic RAG Latency-Cost Trade-off]]
- [[Standard RAG's One-Shot Problem]]
- [[Query Refinement as a Pre- and Post-Retrieval Strategy]]