**Title:** Retrieval Routing Across Multiple Knowledge Sources

**Idea:** Agentic RAG agents can inspect the nature of a query and direct it to the most appropriate source — a SQL database for structured data, a document store for policies, an API for live data, or multiple sources in combination. Routing decisions happen dynamically, not statically.

**Why it matters:** Enterprise knowledge is rarely in one place. Any system that assumes a single retrieval pool will fail on cross-domain questions. Routing is what makes RAG viable for real-world, heterogeneous knowledge environments.

**Trade-offs:** Routing adds orchestration complexity and requires the agent to understand source capabilities, which may itself require prompt engineering or a routing model.

**Connections:**

- [[Agentic RAG Control Loop]]
- [[Multi-Agent Orchestration in RAG]]
- [[Knowledge Source Design]]

## Tags
#ai