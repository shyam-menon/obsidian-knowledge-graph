**Title:** Query Refinement as a Pre- and Post-Retrieval Strategy

**Idea:** In Agentic RAG, query refinement operates in two stages: before retrieval (to clarify intent and decompose ambiguous queries into targeted sub-questions) and after retrieval (to reformulate if results are weak). The agent, not the user, rewrites the query.

**Why it matters:** Most search and RAG failures begin at the query layer. A slightly ambiguous or underspecified query cascades into irrelevant retrievals. Automatic refinement breaks this dependency on perfectly formed user inputs.

**Connections:**

- [[Agentic RAG Control Loop]]
- [[Standard RAG's One-Shot Problem]]
- [[Query Ambiguity in Search Systems]]

## Tags
#ai