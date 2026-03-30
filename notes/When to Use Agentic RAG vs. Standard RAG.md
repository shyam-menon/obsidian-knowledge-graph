**Title:** When to Use Agentic RAG vs. Standard RAG

**Idea:** The decision between standard and agentic RAG should be driven by three diagnostic questions: Does the system retrieve from the right source? Can it evaluate whether what it retrieved is good enough? Can it retry if not? If all three answers are "no" and queries are complex, agentic is warranted. For simple, high-volume queries against clean data, standard RAG is preferable.

**Why it matters:** Treating Agentic RAG as a universal upgrade leads to over-engineered, costly, slow systems. Treating it as a targeted solution leads to appropriate architectural decisions. Engineering fitness-for-purpose, not feature maximalism.

**Connections:**

- [[Agentic RAG Latency-Cost Trade-off]]
- [[Standard RAG's One-Shot Problem]]
- [[Agentic RAG Control Loop]]