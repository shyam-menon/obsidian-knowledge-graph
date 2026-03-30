**Title:** Retrieval False Confidence

**Idea:** A retrieval system returns results based on embedding similarity, not factual accuracy or recency. A chunk about the right topic but from a two-year-old document scores identically to a current, authoritative one — the pipeline cannot distinguish between them.

**Why it matters:** This is a subtle but dangerous failure mode. The system doesn't know it's wrong, so it generates confident responses built on stale or misleading content. Systems without evaluation steps amplify this problem.

**Connections:**

- [[Standard RAG's One-Shot Problem]]
- [[Self-Evaluation in RAG]]
- [[Evaluator Paradox]]