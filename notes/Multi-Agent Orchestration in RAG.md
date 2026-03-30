**Title:** Multi-Agent Orchestration in RAG

**Idea:** At the high end of the agentic spectrum, multiple specialized agents each handle distinct subtasks (retrieval, evaluation, synthesis, domain routing), coordinated by a central orchestrator agent. No single agent handles the full pipeline.

**Why it matters:** Specialization improves performance on complex tasks. An orchestrator can parallelize subqueries, combine results intelligently, and gracefully handle failures in individual agents — enabling RAG at enterprise scale for truly heterogeneous queries.

**Trade-offs:** Significant engineering overhead: agent contracts, failure handling, latency budgets across agent hops, and observability all become non-trivial concerns.

**Connections:**

- [[Agentic RAG Control Loop]]
- [[Retrieval Routing Across Multiple Knowledge Sources]]
- [[ReAct Framework]]