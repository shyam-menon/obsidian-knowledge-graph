**Title:** Standard RAG's One-Shot Problem

**Idea:** Standard RAG pipelines execute a single retrieve-then-generate cycle with no feedback loop. Once retrieval happens, the system commits to whatever came back — regardless of quality, recency, or completeness.

**Why it matters:** This architecture breaks down on any query that is ambiguous, spans multiple sources, or retrieves topically similar but factually wrong content. Recognizing this as a structural flaw (not a tuning problem) is the first step toward choosing the right system.

**Trade-offs:** Simple and fast, but brittle at complexity boundaries.

**Connections:**

- [[Agentic RAG Control Loop]]
- [[Retrieval False Confidence]]
- [[Query Ambiguity in Search Systems]]