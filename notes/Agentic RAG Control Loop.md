**Title:** Agentic RAG Control Loop

**Idea:** Agentic RAG transforms retrieval from a one-shot pipeline into an iterative loop: retrieve → evaluate → decide → retry or respond. Decision points are injected between retrieval and generation, giving the system the ability to self-correct.

**Why it matters:** This loop is the entire value proposition of agentic systems. Without decision points, RAG has no mechanism to detect or recover from retrieval failures. The loop converts a passive pipeline into an active reasoning process.

**Trade-offs:** Each loop iteration adds latency and token cost. Systems with mostly simple queries pay a disproportionate overhead.

**Connections:**

- [[Standard RAG's One-Shot Problem]]
- [[Self-Evaluation in RAG]]
- [[ReAct Framework]]
- [[Multi-Agent Orchestration in RAG]]

## Tags
#ai