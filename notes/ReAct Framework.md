**Title:** ReAct Framework (Reasoning + Acting)

**Idea:** ReAct is a prompting and execution framework where an LLM alternates between explicit reasoning steps ("I need to know X") and action steps ("I will search for X"). It enables multi-hop retrieval with evaluation checkpoints between each hop.

**Why it matters:** ReAct is a practical implementation pattern for Agentic RAG at intermediate complexity. It makes the agent's reasoning transparent and auditable, which is valuable for debugging and trust-building in production systems.

**Connections:**

- [[Agentic RAG Control Loop]]
- [[Multi-Agent Orchestration in RAG]]
- [[Query Refinement as a Pre- and Post-Retrieval Strategy]]