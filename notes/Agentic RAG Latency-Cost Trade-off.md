**Title:** Agentic RAG Latency-Cost Trade-off

**Idea:** Every loop iteration in Agentic RAG requires additional LLM calls, retrieval steps, and evaluations — each adding latency and token cost. A 3–4 loop query can take 10x longer and cost 3–10x more than a single-pass standard RAG query.

**Why it matters:** This is the primary reason Agentic RAG should not be a default architectural choice. For high-volume or latency-sensitive systems, the overhead is disproportionate to the benefit unless the query complexity genuinely demands it.

**Trade-offs:** Can be partially mitigated with semantic caching, early exit conditions, or hybrid routing (simple queries bypass the agent loop entirely).

**Connections:**

- [[Agentic RAG Control Loop]]
- [[When to Use Agentic RAG vs. Standard RAG]]
- [[Semantic Caching in RAG]]

## Tags
#ai